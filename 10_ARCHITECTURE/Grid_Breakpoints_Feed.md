---
projecto: MANGARROSA
tipo: arquitectura
estado: actual-cronológico
data-origem: 2026-04-03
migrado: 2026-07-03
fonte: Notion — "ARQUITECTURA — Grid, Breakpoints e Algoritmo de Feed"
tags: [architecture, grid, breakpoints, feed, algoritmo]
---

# Arquitectura — Grid, Breakpoints e Algoritmo de Feed

## Grid — Breakpoints e colunas

| Viewport | Breakpoint Tailwind | Feed / Explore Posts | Briefs |
|---|---|---|---|
| < 600px | default | 1 col | 1 col |
| ≥ 600px | `min-[600px]` | 2 cols | 2 cols |
| ≥ 900px | `min-[900px]` | 3 cols | 3 cols |
| ≥ 1400px | `min-[1400px]` | 4 cols | 4 cols |
| ≥ 1920px | `xl2` (custom) | 6 cols | — (máx 4) |

- **Altura de linha:** `grid-auto-rows: 360px`.
- **`xl2`** definido em `tailwind.config.ts`: `screens: { xl2: '1920px' }`.
- **Briefs** máximo 4 colunas (cards com texto ficam ilegíveis com mais).

## Posts destacados (Manga Madura) na grid

Post com `is_highlighted = true` ocupa `col-span-2` (2 colunas) × `row-span-2` (720px). O `grid-flow-dense` no container preenche os gaps à volta com os cards seguintes. **Os destacados aparecem na sua posição cronológica** — não são movidos para o topo.

```
[  DESTACADO 2×2  ] [N] [N]
[  DESTACADO 2×2  ] [N] [N]
[N] [N] [N]
```

## Algoritmo do feed — estado actual

**Cronológico puro** (`usePosts`):

```sql
SELECT posts.*, users.*
FROM posts JOIN users ON posts.user_id = users.id
ORDER BY posts.created_at DESC
LIMIT 20 OFFSET n  -- paginação via .range()
```

Sem scoring por engagement, boost por followers, decay temporal, personalização, nem posicionamento forçado de destacados. **Feed "A Seguir"** (`useFollowingPosts`): filtra `user_id IN (following_ids)`, ordena `created_at DESC`. **ExplorePosts**: `usePosts(24)` com filtros de disciplina e `is_highlighted` no cliente.

## Paginação — infinite scroll

`IntersectionObserver` com **callback ref** (sem race conditions): sentinel div (1px) com `rootMargin: 300px` dispara `loadMore()` → `.range(offset, offset+pageSize-1)` → concatena. Botão "Carregar mais" como fallback. Ficheiros: `Feed.tsx`, `FeedAuth.tsx`, `ExplorePosts.tsx`, `Briefs.tsx`.

## Algoritmo de feed — MVP (a implementar)

Simples, sem infra adicional (sem Redis/queues), como RPC no Supabase, observável e calibrável.

**Filosofia: cronológico com boost selectivo.** Dois boosts sobre o feed cronológico:
1. **Boost de destaque** — `is_highlighted` + `highlight_until > now()` → boost temporal.
2. **Boost de engagement inicial** — muitos likes nas primeiras 48h → ligeira promoção.

Parece cronológico, mas destacados e posts com tração surgem mais cedo. Transparente e não penaliza criativos novos.

### Fórmula

```
score = created_at_unix + boost_destacado + boost_engagement
boost_destacado  = 7 * 86400  (se is_highlighted e highlight_until > now) → +7 dias
boost_engagement = MIN(likes_count * 3600, 86400)  → +1h/like, máx +24h, só primeiras 48h
```

### RPC Supabase

```sql
CREATE OR REPLACE FUNCTION get_feed_posts(p_limit int DEFAULT 20, p_offset int DEFAULT 0)
RETURNS TABLE(
  id uuid, title text, description text, media_urls text[], is_highlighted boolean,
  created_at timestamptz, user_id uuid, user_name text, user_username text,
  user_avatar text, user_discipline text[], user_is_pro boolean
) AS $$
SELECT p.id, p.title, p.description, p.media_urls, p.is_highlighted,
       p.created_at, p.user_id, u.name, u.username, u.avatar_url, u.discipline, u.is_pro
FROM posts p
JOIN users u ON p.user_id = u.id
LEFT JOIN (SELECT post_id, COUNT(*) AS likes_count FROM likes GROUP BY post_id) lc ON lc.post_id = p.id
ORDER BY (
  EXTRACT(EPOCH FROM p.created_at)
  + CASE WHEN p.is_highlighted = true AND (p.highlight_until IS NULL OR p.highlight_until > NOW())
         THEN 7 * 86400 ELSE 0 END
  + CASE WHEN NOW() - p.created_at < INTERVAL '48 hours'
         THEN LEAST(COALESCE(lc.likes_count, 0) * 3600, 86400) ELSE 0 END
) DESC
LIMIT p_limit OFFSET p_offset;
$$ LANGUAGE sql STABLE;
```

### Activação no frontend
```typescript
// Actual: supabase.from('posts').select('...').order('created_at',{ascending:false}).range(from,to)
// Com algoritmo:
supabase.rpc('get_feed_posts', { p_limit: 20, p_offset: from })
```

### Calibração dos pesos

| Parâmetro | Valor | Significado |
|---|---|---|
| Boost destacado | +7 dias | Compete com posts dos últimos 7 dias |
| Boost por like | +1 hora | 24 likes = +1 dia de recência |
| Boost engagement máx | +24 horas | Post viral não domina para sempre |
| Janela de engagement | 48 horas | Depois cai para posição cronológica |

Ajustáveis na SQL sem alterar o frontend. (Modelo semelhante ao LinkedIn mas mais simples — capta early signal + destacados sem a infra restante.)

## Algoritmo de feed — Pós-MVP (scoring editorial)

```sql
-- score = decay temporal + likes + boost destacado
(
  EXTRACT(EPOCH FROM (NOW() - posts.created_at)) * -0.001  -- decay
  + likes_count * 2.0                                       -- engagement
  + CASE WHEN is_highlighted THEN 50.0 ELSE 0 END           -- destacados
) AS feed_score
-- ORDER BY feed_score DESC
```
Pesos sugeridos: likes ×2.0; destacado +50; decay −0.001/seg (posts com 1 dia perdem ~86 pontos).

## Estado
- **Actual:** ✅ Cronológico puro, infinite scroll por callback ref
- **Pós-MVP:** 🔜 RPC com scoring editorial
