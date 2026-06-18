---
projecto: MANGARROSA
tipo: estado-actual
sessão: 17
data-origem: 2026-04-22
migrado: 2026-06-17
fonte: Notion — "ESTADO ACTUAL — Sessão 17"
tags: [overview, estado, sessão-17]
---

# Estado Actual — Sessão 17 (22 Abr 2026)

> Última sessão registada no Notion antes da migração. Sessão de *UI polish* intensivo:
> 30+ componentes revistos (tipografia, cores, layout de cards, páginas institucionais, fluxos de perfil).

## Estado do pipeline após Sessão 17

| Fase | Estado |
|---|---|
| A–H + I1+I2 + L | ✅ Concluídas |
| **J** (Nomenclatura) | 🔄 Parcial — MANGA MADURA ✅, alguns badges ✅; auditoria completa Seguir/Cultivar pendente |
| **K** (Emails) | ⬜ Pendente — *próxima etapa* |
| **B** (pendentes) | ⬜ Stripe business name/descriptor/webhook + Supabase email templates |
| **I** (QA pré-lançamento) | ⬜ Mobile, desktop, Stripe real |

> Nota: a numeração de fases no brief de Junho consolidou A–H, L, J como concluídas e
> mantém K em curso. Ver [[70_PIPELINE/Pipeline_Actual]] para o estado canónico.

## Decisões técnicas chave

### Botão Stripe em test mode
O botão flutuante do Stripe (canto inferior direito) é renderizado pelo SDK em modo de teste
(`pk_test_...`). A tentativa de o ocultar via CSS (`iframe[src*="elements-inner-easel"]`)
**quebrou o formulário de pagamento**, por esconder iframes que o Stripe usa internamente.

**Decisão:** não ocultar via CSS. O botão desaparece automaticamente ao migrar para
`pk_live_...` na Fase B. O `index.css` foi arquivado sem quaisquer regras Stripe.

## Fixes pós-Sessão 17

- **Badge stale após "Estender" Manga Madura** (`ModalHighlightAnalytics.tsx`, `OwnProfile.tsx`): prop `onExtended` adicionada; após extensão via modal de analytics, dispara reload 600ms depois.
- **Modal "Amadurecer" mais largo** (`ModalHighlight.tsx`): `maxWidth 480 → 560`.

## Falta na Fase J (nomenclatura UI)

- `FeedAuth.tsx` — "Descobrir" / "A Seguir"
- `PostCard.tsx` — labels de acções
- `OwnProfile.tsx` — "Publicações", "Favoritos", "Seguidores", "A seguir"
- `FloatingNav.tsx` — labels de navegação restantes
- Empty states e mensagens de erro
- Substituição global na UI: "Seguir" → **Cultivar**, "A Seguir" → **Cultivando**

## Componentes revistos na sessão (referência)

Núcleo: `Button.tsx` (novo size `xs`), `SegmentedControl.tsx`, `DisciplinePills.tsx`,
`SlidePanel.tsx` (520→580px), `PostCard.tsx` (badge MADURA → MANGA MADURA),
`CreativeCard.tsx` (props opcionais, fontes reduzidas), `FloatingNav.tsx` (dropdown 180→220px).

Páginas: `Profile.tsx`, `JobDetail.tsx`, `Jobs.tsx` (badges de interesse/candidatura,
"Ver brief" → "Ver chamada", modais fullscreen com `BriefDetail`/`JobDetail`).

Explore: `Explore.tsx`, `ExploreCreatives.tsx`, `ExplorePosts.tsx` (discipline pills → `text-fluid-xs`).

Institucionais/legais: `FeedbackPage.tsx` (novo tipo "Política de privacidade", grid 3→4 col),
`PrivacyPage.tsx` (`CINAP-CIC, Lda.`, links internos), `RegisterContent.tsx`
(role lock implícito — sub-tipo só dentro do mesmo role, `role` não editável).
