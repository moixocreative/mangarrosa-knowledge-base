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
- Migração dos restantes clusters (nomenclatura, integrações, systems, legal, brand, sessões) em curso.

## v0.2 — 17 Junho 2026

Alinhamento à convenção dos restantes vaults + cluster de nomenclatura.

**Alterado:**
- Ficheiros `README`, `CLAUDE`, `INDEX`, `CHANGELOG` movidos para a raiz do vault (convenção `beyond-vision`); removido `00_OVERVIEW/00_README.md` e a nota default `Bem-vindo.md`.

**Adicionado:**
- `50_NOMENCLATURA_COPY/Regra_Definitiva_EN_PT.md` — regra canónica (código EN / UI PT; tabelas mantêm-se EN).
- `50_NOMENCLATURA_COPY/Mapa_Nomenclatura.md` — mapa completo, com divergência de termos assinalada.
- `50_NOMENCLATURA_COPY/Copy_Universo_MANGARROSA.md` — terminologia consolidada + guia de tom de voz.

**Notas:**
- Resolvida a divergência de nomenclatura: prevalecem Cultivar/Cultivadores/Colher/Polinizar (Fase L, 21 Abr) sobre Fruir/Apanhar/Polinização (Mapa, 13 Abr).

## v0.3 — 3 Julho 2026

Camadas financeira e de portefólio, roadmap de retoma, e cluster de integrações.

**Adicionado:**
- `85_FINANCEIRO/` — registo de despesas, tempo (fases A–M) e investimento/rentabilidade (do modelo do vault-template, adaptado a produto próprio).
- `95_CASE_STUDY.md` — narrativa curada de portefólio (do `95_CASE_STUDY_TEMPLATE`), pré-preenchida em PT-PT.
- `70_PIPELINE/00_Roadmap_Retoma.md` — sequência acordada: docs → J → K → B → I → M → N (design system).
- `40_INTEGRATIONS/00_Integrations_Overview.md` — índice do cluster de integrações.
- `40_INTEGRATIONS/Stripe_Pagamentos.md` — infra Stripe (webhook, edge functions, SQL, price IDs); secret redigido; flow directo assinalado como superado pelo modelo da Cesta.
- `40_INTEGRATIONS/Faturacao_InvoiceXpress.md` — faturação AT-certificada (NIF, IVA 23%, SAF-T, código do webhook).

**Notas:**
- Emails (Resend) permanecem documentados em `70_PIPELINE/Fase_K_Emails.md` (não duplicados no cluster de integrações).
- Segredos de todos os serviços (Stripe, InvoiceXpress, Resend) mantidos fora do vault — só nos secrets do Supabase.
- Sessões 6–16: decidido condensar numa nota única de histórico (não migrar verbatim).
