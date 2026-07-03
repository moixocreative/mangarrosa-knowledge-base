---
projecto: MANGARROSA
tipo: pipeline
estado: activo
actualizado: 2026-07-03
fonte: Notion — "PIPELINE MANGARROSA — Abril/Maio 2026"
tags: [pipeline, roadmap, estado]
---

# Pipeline MANGARROSA

> **Fonte única do estado do projecto:** onde estamos, o que se segue, e o estado de todas as fases. Detalhe da fase activa em [[70_PIPELINE/Fase_K_Emails]]. Histórico versionado em [[CHANGELOG]].

## Onde estamos (3 Jul 2026)

- **Migração Notion → vault:** ✅ completa. Falta só rever/descartar extras opcionais antes de apagar o Notion — checklist no [[INDEX]].
- **Fase J (nomenclatura):** ✅ aplicada no `development` (commit `3b78133`, em push).
- **Próximo passo:** **Fase K — Emails** (branch `feat/emails-resend`).

## Ordem do roadmap

docs ✅ → **J ✅** → **K (activa)** → B → I → M → N (design system).

Sessões 6–17 condensadas em [[99_SESSIONS/Historico_Sessoes]] (não verbatim). Antes de apagar o Notion: export Markdown + push GitHub + revisão dos extras opcionais.

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

## Fase J — Nomenclatura ✅ (aplicada 3 Jul 2026)

> Aplicada no `development` (commit `3b78133`). O verbo de seguir foi consolidado em **Cultivar/Cultivando** em toda a UI.

| Termo actual | MANGARROSA | Estado |
|---|---|---|
| Publicação / Post | Manga 🥭 | ✅ |
| Destacar | Amadurecer | ✅ ModalHighlight |
| Post em Destaque | Manga Madura | ✅ ModalHighlight |
| Feed / Descoberta | Pomar 🌿 | ✅ |
| Seguir | Cultivar 🌱 | ✅ |
| A seguir | Cultivando | ✅ |
| Seguidores | Cultivadores | ✅ |
| Guardar / Favoritar | Colher | ✅ (tab "Colhidas") |
| Analytics | A Colheita | 🔄 A confirmar nos modais de analytics |
| Referido / Convite | Semente | ✅ |
| Wallet de créditos | A Cesta 🧺 | ✅ |

**Auditados ✅:** `PostCard`, `PostDetail`, `ExploreCreatives`, `Profile`, `OwnProfile`, `FeedAuth` (já estavam ok: `FloatingNav`, `CreativeCard`, `Settings`).
**Por confirmar:** `StoriesBar.tsx` e headers dos modais de analytics (`ModalPostAnalytics`); **testar** o toggle "Descobrir/Cultivando"; **coordenar** com o branch `fix/conditionally-render-seguir-button`.
**Fora de âmbito (código, não UI):** variants `"seguir"`/`"a-seguir"`, chave `sessionStorage matcha_scroll_restore`, título "Configurações" vs "Definições".

## Fase K — Emails 📧
Próxima etapa. Ver plano detalhado em [[70_PIPELINE/Fase_K_Emails]] (triggers, arquitectura, templates, K1–K8). Arranque em `feat/emails-resend`.

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
M1 uniformizar padrões · M2 remover código morto (bloco highlight do stripe-webhook, ModalPayment dentro do ModalHighlight, `priceId` no array `durations`) · M3 remover rotas `/test*` e console.logs · M4 reduzir `as any` · M5 documentar arquitectura.
Candidatos adicionais (Fase J): renomear variants `"seguir"`/`"a-seguir"` e chave `matcha_scroll_restore`.

## Fase N — Design System 🎨 (nova)
Tokenização W3C DTCG → Figma → Tailwind, com base em [[95_BRAND/Identidade_Visual]].

## Decisões técnicas em vigor
- **Botão Stripe test mode:** não ocultar via CSS — a tentativa (`iframe[src*="elements-inner-easel"]`) **quebrou o formulário de pagamento**. Desaparece automaticamente ao migrar para `pk_live_` na Fase B. `index.css` sem regras Stripe.

## Bugs corrigidos (sessão Abril 2026)
Posts destacados como normais para clientes (`FeedAuth.tsx`) · ReferralBlock ausente para criativos (`OwnProfile.tsx`) · Badge PRO duplicado (`BriefDetailClient.tsx`, `JobDetailClient.tsx`) · build error JSX (`OwnProfile.tsx`) · saldo wallet não actualizava (`CreditsWallet.tsx`, `Settings.tsx`) · stale closure no `balance` ao renovar PRO (`Settings.tsx`) · flashes pós-pagamento (`useCredits.ts`) · TS errors (`Settings.tsx`).

## Modelo de pagamento — decisões definitivas
- **Criativos:** PRO (via Cesta) + Destaques (via Cesta) + Referrals (+5 🌱/convite)
- **Clientes:** só Cesta. Sem PRO, sem Referrals. Destaques de Briefs/Vagas pós-lançamento.
- **Stripe:** serve exclusivamente para carregar a Cesta; PRO e Destaques debitam da Cesta.
- **1 Semente = €1 · mínimo 5 🌱 por carregamento**

## Relacionado (por migrar)
- *BUGS CRÍTICOS PRÉ-LANÇAMENTO — Plano de resolução* (Notion `3404ecfa1326815ab56adc8d1968f11f`)

---

> **Como o estado é mantido:** este ficheiro é o **único** registo do estado das fases e do próximo passo — actualizado ao fecho de cada sessão. Sem tabelas de estado duplicadas noutros ficheiros. Histórico versionado em [[CHANGELOG]].
