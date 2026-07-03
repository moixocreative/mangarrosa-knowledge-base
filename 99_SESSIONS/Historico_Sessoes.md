---
projecto: MANGARROSA
tipo: histórico
estado: condensado
migrado: 2026-07-03
fonte: Notion — sessões 6–17 (condensadas)
tags: [sessions, historico]
---

# Histórico de Sessões (6–17)

> Nota condensada. As sessões do Notion **não** foram migradas verbatim (decisão do roadmap) — ficam aqui os marcos de cada uma. O estado presente do projecto vive em [[70_PIPELINE/Pipeline_Actual]]. O projecto chamava-se MATCHA durante estas sessões.

## Arco de desenvolvimento

| Sessão | Data | Marcos |
|---|---|---|
| **6** | 26 Mar 2026 | Plano de implementação Briefs + Notifications; sistema de Mensagens; UX dos Slide Panels (mensagens/notificações). |
| **10** | Abr 2026 | Design decisions PostCard v2; UX de posts destacados; prompt do Admin Dashboard (Lovable); arquitectura de grid/breakpoints e algoritmo de feed. |
| **11/12** | Abr 2026 | Onboarding com roles expandidos + faturação no perfil; features futuras (Stories, Vagas, FloatingNav v2); análise de discrepâncias Briefs vs Vagas. |
| **13** | 8 Abr 2026 | Stories; lista completa de notificações; páginas legais (T&C, Privacidade, Cookies); página Acerca; notas de performance; decisões Free vs PRO; fluxo pós-autenticação contextual (pending action). |
| **15** | 10 Abr 2026 | **Rename MATCHA → MANGARROSA**; sistema de identidade visual (brand system); bugs & pendentes. |
| **16** | 11 Abr 2026 | Splash/loading (decisão de design); estratégia Mangas & Fundadores + implicações técnicas. |
| **17** | 22 Abr 2026 | *UI polish* intensivo (30+ componentes); decisão do botão Stripe test mode; fixes de Manga Madura (detalhe abaixo). |

## Detalhe — Sessão 17 (22 Abr 2026)

Última sessão registada no Notion antes da migração. *UI polish* intensivo (tipografia, cores, layout de cards, páginas institucionais, fluxos de perfil).

**Fixes:**
- Badge stale após "Estender" Manga Madura (`ModalHighlightAnalytics.tsx`, `OwnProfile.tsx`): prop `onExtended`; reload 600ms após extensão.
- Modal "Amadurecer" mais largo (`ModalHighlight.tsx`): `maxWidth 480 → 560`.

**Componentes revistos:** `Button.tsx` (novo size `xs`), `SegmentedControl.tsx`, `DisciplinePills.tsx`, `SlidePanel.tsx` (520→580px), `PostCard.tsx` (MADURA → MANGA MADURA), `CreativeCard.tsx`, `FloatingNav.tsx` (dropdown 180→220px); páginas `Profile.tsx`, `JobDetail.tsx`, `Jobs.tsx` ("Ver brief" → "Ver chamada"); `Explore*.tsx` (pills → `text-fluid-xs`); institucionais `FeedbackPage.tsx`, `PrivacyPage.tsx` (`CINAP-CIC, Lda.`), `RegisterContent.tsx` (role lock).

> A decisão durável do Stripe test mode vive em [[70_PIPELINE/Pipeline_Actual]] (Decisões técnicas em vigor).

## Onde o conteúdo destas sessões vive agora

O material substantivo foi migrado para os clusters temáticos, não como sessões:
- Briefs, Notificações, Mensagens, Stories → [[30_SYSTEMS/00_Systems_Overview]]
- Grid/feed → [[10_ARCHITECTURE/Grid_Breakpoints_Feed]]
- Legal → [[90_LEGAL/Termos_Condicoes]] e afins
- Free vs PRO → [[80_PRODUCT/Free_vs_PRO]]
- Identidade visual → [[95_BRAND/Identidade_Visual]]
- Nomenclatura/rename → [[50_NOMENCLATURA_COPY/Mapa_Nomenclatura]]

## Docs de sessão não migrados (descartados conscientemente)

Prompts de continuação de sessão, listas de bugs datadas (23 Mar, Sessão 13, Sessão 15), e estados intermédios (Sessões 10, 11/12, 13, 16) — superados pelo [[70_PIPELINE/Pipeline_Actual]]. Continuam no Notion até este ser apagado; se algum for necessário, recuperar antes do delete.
