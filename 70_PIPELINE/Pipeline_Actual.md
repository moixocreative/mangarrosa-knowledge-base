---
projecto: MANGARROSA
tipo: pipeline
estado: activo
data-origem: 2026-04-22
migrado: 2026-06-17
fonte: Notion — "PIPELINE MANGARROSA — Abril/Maio 2026"
tags: [pipeline, roadmap]
---

# Pipeline MANGARROSA

> Estado canónico do roadmap. Detalhe da Fase K em [[70_PIPELINE/Fase_K_Emails]].

## Fases concluídas ✅

| Fase | Descrição |
|---|---|
| A | Pendentes técnicos (posts fixados, guard PRO, stories, typography) |
| B | Domínio — Supabase URLs + repo GitHub + código *(B3–B6 pendentes, ver abaixo)* |
| C | SQL Migrations (credits, referrals, RPCs, triggers) |
| D | Landing `/join` (Fundadores) |
| E | ReferralBlock |
| F | Stripe Webhook |
| G | CreditsWallet em Settings |
| H | Welcome Modal Fundadores |
| L | Copy universo MANGARROSA — páginas institucionais, preços, links, badges, nomenclatura visual |

## Fase J — Nomenclatura 🔴 (auditoria restante)

> Parcialmente implementada: "Amadurecer", "Manga Madura", "Sementes", "Cesta", "Pomar" já no código.
> Este sprint audita e fecha o que falta.

| Termo actual | MANGARROSA | Estado |
|---|---|---|
| Publicação / Post | Manga 🥭 | 🔄 Parcial |
| Destacar | Amadurecer | ✅ ModalHighlight |
| Post em Destaque | Manga Madura | ✅ ModalHighlight |
| Feed / Descoberta | Pomar 🌿 | 🔄 Parcial |
| Seguir | Cultivar 🌱 | ⬜ |
| A seguir | Cultivando | ⬜ |
| Seguidores | Cultivadores | ⬜ |
| Guardar / Favoritar | Colher | ⬜ |
| Analytics | A Colheita | ⬜ |
| Referido / Convite | Semente | ✅ |
| Wallet de créditos | A Cesta 🧺 | ✅ |

**Ficheiros a auditar:** `FeedAuth.tsx`, `PostCard.tsx`, `OwnProfile.tsx`, `FloatingNav.tsx`,
`Settings.tsx`, `StoriesBar.tsx`, e todos os empty states / mensagens de erro.

## Fase K — Emails 📧
Em curso. Ver plano detalhado em [[70_PIPELINE/Fase_K_Emails]] (triggers, arquitectura, templates, K1–K8).

## Fase B — Pendentes de infra ⚙️
> Não bloqueiam código, mas bloqueiam lançamento. Paralelizáveis com J/K/L.

| # | Tarefa | Onde | Estado |
|---|---|---|---|
| B3 | Supabase Email templates: MATCHA → MANGARROSA | Supabase dashboard | ⬜ |
| B4 | Stripe → Business name: MANGARROSA | Stripe dashboard | ⬜ |
| B5 | Stripe → Statement descriptor: MANGARROSA | Stripe dashboard | ⬜ |
| B6 | Stripe → Webhook endpoint: actualizar URL | Stripe dashboard | ⬜ |

## Fase I — QA pré-lançamento 🧪
> Última fase antes de lançar. Só executar com J + K + L + B fechados.

| # | Tarefa | Estado |
|---|---|---|
| I1 | `highlight_until` gravado ao destacar | ✅ |
| I2 | pg_cron `expire-highlights` (horário) | ✅ |
| I3 | QA Manga Madura: débito wallet + highlight_until + visual 2×2 | ⬜ |
| I4 | QA Referral: link → registo → +5 🌱 | ⬜ |
| I5 | QA PRO: activar via Cesta + guard features | ⬜ |
| I6 | Stripe real (cartão real, €5) | ⬜ |
| I7 | QA mobile 393px — todas as páginas | ⬜ |
| I8 | QA breakpoint 1920px+ — todas as páginas | ⬜ |
| I9 | Guard PRO nas mensagens (Free só responde) | ⬜ |

## Fase M — Limpeza de código 🧹 (pós-lançamento)
M1 uniformizar padrões · M2 remover código morto (bloco highlight do stripe-webhook,
ModalPayment dentro do ModalHighlight, `priceId` no array `durations`) ·
M3 remover rotas `/test*` e console.logs · M4 reduzir `as any` · M5 documentar arquitectura.

## Bugs corrigidos (sessão Abril 2026)
Posts destacados como normais para clientes (`FeedAuth.tsx`) · ReferralBlock ausente para
criativos (`OwnProfile.tsx`) · Badge PRO duplicado (`BriefDetailClient.tsx`,
`JobDetailClient.tsx`) · build error JSX (`OwnProfile.tsx`) · saldo wallet não actualizava
(`CreditsWallet.tsx`, `Settings.tsx`) · stale closure no `balance` ao renovar PRO
(`Settings.tsx`) · flashes pós-pagamento (`useCredits.ts`) · TS errors (`Settings.tsx`).

## Modelo de pagamento — decisões definitivas
- **Criativos:** PRO (via Cesta) + Destaques (via Cesta) + Referrals (+5 🌱/convite)
- **Clientes:** só Cesta. Sem PRO, sem Referrals. Destaques de Briefs/Vagas pós-lançamento.
- **Stripe:** serve exclusivamente para carregar a Cesta; PRO e Destaques debitam da Cesta.
- **1 Semente = €1 · mínimo 5 🌱 por carregamento**

## Relacionado (por migrar)
- *BUGS CRÍTICOS PRÉ-LANÇAMENTO — Plano de resolução* (Notion `3404ecfa1326815ab56adc8d1968f11f`)
