---
projecto: MANGARROSA
tipo: produto
estado: implementado
data-origem: 2026-04-08
migrado: 2026-07-03
fonte: Notion — "FREE vs PRO — Diferenciação de planos"
tags: [product, free, pro, planos]
---

# Free vs PRO — Diferenciação de Planos

> Diferenciação implementada em código. Nota: os destaques (Amadurecer) agora **debitam da Cesta** (modelo consolidado), não via Stripe directo.

## Matriz

| Funcionalidade | Free | PRO | Onde |
|---|---|---|---|
| Portfólio público | ✅ Ilimitado | ✅ Ilimitado | — |
| Mostrar interesse em briefs | ✅ | ✅ | — |
| Candidaturas a vagas | ✅ | ✅ | — |
| Amadurecer (destacar) | ✅ (a todos) | ✅ | `ModalHighlight.tsx` |
| Receber mensagens | ✅ | ✅ | — |
| **Iniciar conversas** | ❌ só responde | ✅ | `Profile.tsx` → modal PRO |
| **Histórias** | 1/dia | Ilimitadas | `CreateStory.tsx` (count diário) |
| **Badge PRO (Crown)** | ❌ | ✅ | `OwnProfile.tsx`, `PostCard.tsx` |
| **Prioridade em briefs/vagas** | Normal | Aparece primeiro | `BriefDetailClient`/`JobDetailClient` (sort `is_pro`) |
| **Visibilidade prioritária no feed** | Normal | Prioridade | Algoritmo de feed (pós-MVP) |
| **Analytics — posts destacados** | ✅ | ✅ | `ModalHighlightAnalytics.tsx` |
| **Analytics — todos os posts** | ❌ | ✅ | `ModalPostAnalytics.tsx` (novo) |
| **Featured work no perfil** | ❌ | ✅ 3 posts fixos | `OwnProfile.tsx` + `featured_post_ids` |
| Suporte prioritário | ❌ | ✅ | Manual |

## Implementação por ficheiro

- **`CreateStory.tsx`:** Free com ≥1 story hoje → erro + CTA upgrade; PRO sem verificação.
- **`ModalPostAnalytics.tsx`** (novo): impressões, aberturas, likes, taxa de abertura; dados de `post_views` (rastreado para todos os posts); badge PRO no header.
- **`PostCard.tsx`:** `useTrackView` rastreia **todos** os posts; botão `BarChart2` (posts próprios) → analytics (só com `onAnalyticsClick`); botão `Pin` → fixa/desfixa Featured Work; prop `isFeatured` (Pin verde quando fixo).
- **`OwnProfile.tsx`:** estado `featuredPostIds` (até 3); `toggleFeatured` → `users.featured_post_ids`; secção "Featured work" (só PRO); `onAnalyticsClick={isPro ? … : undefined}`.
- **`BriefDetailClient.tsx` + `JobDetailClient.tsx`:** select inclui `is_pro`; lista PRO primeiro; badge Crown nos PRO.
- **`Profile.tsx`:** `viewerIsPro`; `handleMessageClick` → Free abre modal "Funcionalidade PRO" (CTA `/settings`); PRO abre `openMessages`.

## SQL
```sql
-- featured_posts_migration.sql
ALTER TABLE users ADD COLUMN IF NOT EXISTS featured_post_ids uuid[] DEFAULT '{}';
```

## Notas de decisão

- **Destaques (Amadurecer) para todos:** disponíveis a Free e PRO. A diferenciação PRO está na visibilidade orgânica do feed, não no destaque pago — remove fricção e permite receita de qualquer utilizador. (Pagamento via Cesta.)
- **Limite de posts/mês (Free):** **NÃO** implementado no MVP (risco de fricção em crescimento). Reconsiderar pós-MVP com escala.
- **Visibilidade prioritária no feed:** pós-MVP; requer ordenar por `is_pro` + `is_highlighted` no query do feed.
- **Mensagens — Free só responde:** implementado em `Profile.tsx`. Free responde a conversas iniciadas por outros, não inicia. Incentiva upgrade sem bloquear comunicação.
