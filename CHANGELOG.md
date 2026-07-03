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
- `30_SYSTEMS/` — índice, Mensagens (Realtime + guard PRO), Notificações (lista completa + ícones + tabela), Briefs/Chamadas ("Tenho Interesse"), Stories (efémeras 24h), Explore/Descobrir, Favoritos/Colher, Eliminação de conta (graça 7 dias RGPD).

**Notas:**
- Emails de notificação continuam em `Fase_K_Emails` (não duplicados).

## v0.6 — 3 Julho 2026

Cluster de arquitectura e setup.

**Adicionado:**
- `10_ARCHITECTURE/Grid_Breakpoints_Feed.md` — grid/breakpoints, destaques na grid, algoritmo de feed (MVP com boost selectivo + RPC `get_feed_posts`, scoring editorial pós-MVP), infinite scroll.
- `20_SETUP/Supabase_Integration_Guide.md` — esquema completo da BD (10 tabelas + RLS), trigger de perfil, buckets, auth.

## v0.7 — 3 Julho 2026

Clusters produto, brand e histórico — migração principal do Notion concluída.

**Adicionado:**
- `80_PRODUCT/Free_vs_PRO.md` — matriz Free vs PRO + implementação por ficheiro.
- `95_BRAND/Identidade_Visual.md` — brand system (cor, tipografia, linguagem gráfica, interação); base para a Fase N.
- `99_SESSIONS/Historico_Sessoes.md` — histórico condensado das sessões 6–17 (não verbatim).

**Notas:**
- Todos os clusters principais migrados.

## v0.8 — 3 Julho 2026

Consolidação — eliminar duplicação de estado (uma fonte de verdade por assunto).

**Removido:**
- `00_OVERVIEW/01_Estado_Actual.md` — a tabela de pipeline e o "próximo passo" duplicavam o `Pipeline_Actual`. Conteúdo único absorvido: decisão Stripe test-mode → `Pipeline_Actual`; detalhe da Sessão 17 → `Historico_Sessoes`.
- `70_PIPELINE/00_Roadmap_Retoma.md` — doc de "como retomar", já cumprido; a ordem do roadmap passou para o topo do `Pipeline_Actual`.
- `70_PIPELINE/Fase_J_Nomenclatura.md` — fase fechada; o resultado vive no `Pipeline_Actual` (o código está no commit `3b78133`).

**Alterado:**
- `70_PIPELINE/Pipeline_Actual.md` — **fonte única** do estado das fases, próximo passo, ordem do roadmap e decisões técnicas. Fase J marcada ✅.
- `INDEX`, `CLAUDE`, `README` — backlinks corrigidos; decisões de pipeline/pagamento deixam de ser duplicadas (apontam para o `Pipeline_Actual`).
- `20_SETUP/Git_Workflow_Branching.md` — nova convenção de branches + PRs.

**Notas:**
- Princípio adoptado: **uma fonte de verdade por assunto**. Estado → `Pipeline_Actual`; história → `CHANGELOG`; mapa/decisões de referência → `INDEX`; detalhe → docs de cluster/fase.
