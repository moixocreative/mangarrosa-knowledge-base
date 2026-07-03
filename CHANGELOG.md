---
owner: Moixo (Maurício Pereira)
project: MANGARROSA
type: changelog
tags: [changelog]
---

# — CHANGELOG — MANGARROSA Knowledge Base

## v0.1 — 17 Junho 2026

Criação do vault e início da migração do Notion → Obsidian.

**Adicionado:**
- Ficheiros de raiz: `README.md`, `CLAUDE.md`, `INDEX.md`, `CHANGELOG.md` (convenção alinhada com os restantes vaults).
- `00_OVERVIEW/01_Estado_Actual.md` — Sessão 17 (22 Abr 2026).
- `00_OVERVIEW/02_Stack_e_Identificadores.md` — repo, Supabase, domínio, Stripe Price IDs.
- `70_PIPELINE/Pipeline_Actual.md` — roadmap canónico (fases A–M, modelo de pagamento, bugs).
- `70_PIPELINE/Fase_K_Emails.md` — plano completo de emails (triggers, arquitectura, K1–K8, templates).

**Notas:**
- Estrutura de pastas estabelecida (`00`–`99`) coerente com `beyond-vision` / `humanmindlab`.
- Fonte de verdade transferida do Notion para este vault.

## v0.2 — 17 Junho 2026

Alinhamento à convenção dos restantes vaults + cluster de nomenclatura.

**Alterado:**
- Ficheiros `README`, `CLAUDE`, `INDEX`, `CHANGELOG` movidos para a raiz do vault; removido `00_OVERVIEW/00_README.md` e a nota default `Bem-vindo.md`.

**Adicionado:**
- `50_NOMENCLATURA_COPY/` — regra definitiva (EN/PT), mapa completo, copy do universo + tom de voz.

**Notas:**
- Resolvida a divergência de nomenclatura: prevalecem Cultivar/Cultivadores/Colher/Polinizar (Fase L, 21 Abr) sobre Fruir/Apanhar/Polinização (Mapa, 13 Abr).

## v0.3 — 3 Julho 2026

Camadas financeira e de portefólio, roadmap de retoma, e cluster de integrações.

**Adicionado:**
- `85_FINANCEIRO/` — despesas, tempo (fases A–M), investimento/rentabilidade.
- `95_CASE_STUDY.md` — narrativa curada de portefólio (do `95_CASE_STUDY_TEMPLATE`), PT-PT.
- `70_PIPELINE/00_Roadmap_Retoma.md` — sequência: docs → J → K → B → I → M → N (design system).
- `40_INTEGRATIONS/` — índice, Stripe (secret redigido; flow directo assinalado superado), Faturação InvoiceXpress.

**Notas:**
- Segredos de todos os serviços mantidos fora do vault (só nos secrets do Supabase).
- Sessões 6–16: decidido condensar numa nota única de histórico.

## v0.4 — 3 Julho 2026

Cluster legal.

**Adicionado:**
- `90_LEGAL/` — Termos e Condições, Política de Privacidade (RGPD), Política de Cookies (todos rascunhos, carecem revisão jurídica; chaves `matcha_*` → `mangarrosa_*`).

## v0.5 — 3 Julho 2026

Cluster de sistemas.

**Adicionado:**
- `30_SYSTEMS/00_Systems_Overview.md` — índice dos sistemas.
- `30_SYSTEMS/Mensagens.md` — Realtime + guard PRO (por implementar).
- `30_SYSTEMS/Notificacoes.md` — lista completa in-app (clientes + criativos), ícones, tabela.
- `30_SYSTEMS/Briefs_Tenho_Interesse.md` — fluxo "Tenho Interesse" + decisões.
- `30_SYSTEMS/Stories.md` — histórias efémeras 24h (expiração por query, sem cron).
- `30_SYSTEMS/Explore_Search.md` — pesquisa (AND logic, debounce 400ms).
- `30_SYSTEMS/Favorites.md` — favoritos privados (Colher).
- `30_SYSTEMS/Account_Deletion.md` — período de graça 7 dias (RGPD).

**Notas:**
- Emails de notificação continuam em `Fase_K_Emails` (não duplicados).

## v0.6 — 3 Julho 2026

Cluster de arquitectura e setup.

**Adicionado:**
- `10_ARCHITECTURE/Grid_Breakpoints_Feed.md` — grid/breakpoints, comportamento dos destaques na grid, algoritmo de feed (MVP com boost selectivo + RPC `get_feed_posts`, e scoring editorial pós-MVP), infinite scroll.
- `20_SETUP/Supabase_Integration_Guide.md` — **esquema completo da BD** (10 tabelas + RLS), trigger de auto-criação de perfil, storage buckets, ligação Lovable, auth no frontend.

**Notas:**
- Faltam à checklist "até apagar o Notion": `80_PRODUCT`, `95_BRAND`, sessões (nota única) — mais extras opcionais (seed data, i18n, onboarding, performance).
