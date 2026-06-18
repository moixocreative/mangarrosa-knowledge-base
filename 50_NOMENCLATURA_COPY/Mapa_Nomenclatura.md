---
projecto: MANGARROSA
tipo: nomenclatura
estado: a-consolidar
data-origem: 2026-04-13
migrado: 2026-06-17
fonte: Notion — "NOMENCLATURA — Mapa completo MANGARROSA"
tags: [nomenclatura, fase-j, copy]
---

# Mapa de Nomenclatura MANGARROSA

> [!warning] Divergência de termos a resolver na auditoria Fase J
> Este mapa (13 Abr) propõe termos que foram **revistos** em fontes mais recentes.
> Onde houver conflito, **prevalecem as fontes mais recentes**:
> | Conceito | Mapa (13 Abr) | Pipeline 22 Abr / Brief Jun (canónico) |
> |---|---|---|
> | Seguir | Fruir | **Cultivar** |
> | Seguidores | Fruidores | **Cultivadores** |
> | Favoritar | Apanhar | **Colher** |
> | Referido/Convite | Polinização | **Polinizar** |
> | Analytics | A Colheita | A Colheita (consistente) |
>
> Decisão final pendente — ver [[70_PIPELINE/Pipeline_Actual|Fase J]].

## Decisão estratégica

Mercado-alvo: CPLP (sobretudo Brasil). **Regra definitiva:**

| Camada | Língua | Exemplos |
|---|---|---|
| Ficheiros React | Inglês | `PostCard.tsx`, `usePosts.ts`, `ReferralBlock.tsx` |
| Tabelas Supabase | Inglês | `posts`, `users`, `credits_balance`, `referrals` |
| Variáveis/hooks internos | Inglês | `feedPosts`, `useCredits`, `isHighlighted` |
| URLs | Português MANGARROSA | `/pomar`, `/manga/:id`, `/descobrir` |
| UI/Copy/Labels | Português MANGARROSA | "O Pomar", "Manga", "Sementes" |

**Vantagem:** código universalmente legível; se a plataforma migrar para inglês, muda-se só o copy da UI e as rotas — o código técnico fica intacto.

## Mapa completo (conceito → MANGARROSA → URL)

| Conceito | Nome MANGARROSA | URL actual | URL novo |
|---|---|---|---|
| Feed | O Pomar | `/feed` | `/pomar` |
| Post / Projecto | Manga 🥭 | `/post/:id` | `/manga/:id` |
| Criar post | Plantar Manga | `/post/create` | `/manga/plantar` |
| Explorar | Descobrir | `/explore` | `/descobrir` |
| Explorar posts | Descobrir Mangas | `/explore/posts` | `/descobrir/mangas` |
| Explorar criativos | Descobrir Cultivadores | `/explore/creatives` | `/descobrir/cultivadores` |
| Perfil próprio | O Meu Pomar | `/profile/me` | `/perfil/meu` |
| Perfil de outro | Pomar de @username | `/profile/:username` | `/perfil/:username` |
| Seguir | Fruir ⚠️→ Cultivar | — | — |
| Seguindo | Fruindo ⚠️→ Cultivando | — | — |
| Seguidores | Fruidores ⚠️→ Cultivadores | — | — |
| Guardar / Favoritar | Apanhar ⚠️→ Colher | — | — |
| Favoritos | Mangas Apanhadas | `/favorites` | `/apanhadas` |
| Destacar post | Amadurecer Manga | — | — |
| Post destacado | Manga Madura | — | — |
| Stories | Histórias | `/stories/create` | `/historias/criar` |
| Briefs | Chamadas | `/briefs` | `/chamadas` |
| Criar brief | Nova Chamada | `/briefs/create` | `/chamadas/criar` |
| Vagas | Oportunidades | `/jobs` | `/oportunidades` |
| Mensagens | Mensagens | `/messages` | `/mensagens` |
| Notificações | Notificações | `/notifications` | `/notificacoes` |
| Settings | Definições | `/settings` | `/definicoes` |
| Moeda interna | Semente 🌱 | — | — |
| Wallet | A Cesta | — | — |
| Referido | Polinização ⚠️→ Polinizar | — | — |
| Quem refere | Polinizador 🐝 | — | — |
| Analytics | A Colheita | — | — |
| Landing fundadores | Entra no Pomar | `/join` | `/juntar` |

## Implicações técnicas

1. **Rotas (`App.tsx`):** todas actualizadas; rotas antigas → redirect 301 (SEO + links externos).
2. **Código interno:** ficheiros/variáveis podem manter nomes EN (`usePosts.ts`, `PostCard.tsx`). Ficheiros novos podem já usar nomenclatura PT (`useSementes.ts`, `CestaSementes.tsx`).
3. **Tabelas Supabase:** migrar `mangas_balance`/`mangas_transactions`/`referrals` → `sementes_balance`/`sementes_transactions`/`polinizacoes`.
4. **Muda:** URLs, copy UI, labels, placeholders, notificações, emails. **Não muda:** nomes internos React/TS. **Muda gradualmente:** tabelas DB.

## ⚠️ Notas antes do lançamento
- Rotas antigas → redirect 301 para as novas.
- Supabase Auth callback URLs actualizados quando as URLs mudarem.
- Google OAuth redirect URLs actualizados no Google Console.
