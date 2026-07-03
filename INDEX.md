---
project: MANGARROSA
owner: Moixo (Maurício Pereira)
type: index
---

# Index | MANGARROSA

## Recursos do projecto

- **Repo:** `moixocreative/mangarrosa` (branch `development`)
- **Supabase project ID:** `pevjaqrftqnstcjwdtfk`
- **Domínio:** `www.mangarrosa.com` · **Deploy:** `matcha-app.lovable.app`
- **Notion (origem):** página *BUILD* `31c4ecfa132680898ac1f7f7c81d45ad`
- Detalhe técnico: [[00_OVERVIEW/02_Stack_e_Identificadores]]

## Índice de documentos

### Changelog
- [[CHANGELOG]]

### Overview
- [[00_OVERVIEW/01_Estado_Actual|Estado actual (Sessão 17)]]
- [[00_OVERVIEW/02_Stack_e_Identificadores|Stack e identificadores]]

### Pipeline
- [[70_PIPELINE/00_Roadmap_Retoma|Roadmap de retoma (Julho 2026)]] — ordem de trabalho acordada
- [[70_PIPELINE/Pipeline_Actual|Pipeline actual (fases A–M)]]
- [[70_PIPELINE/Fase_K_Emails|Fase K — Emails (activo)]]

### Integrações
- [[40_INTEGRATIONS/00_Integrations_Overview|Integrações & Serviços (índice)]]
- [[40_INTEGRATIONS/Stripe_Pagamentos|Stripe — Pagamentos (PRO + Amadurecer)]]
- [[40_INTEGRATIONS/Faturacao_InvoiceXpress|Faturação — InvoiceXpress + NIF + IVA]]

### Nomenclatura & Copy
- [[50_NOMENCLATURA_COPY/Regra_Definitiva_EN_PT|Regra definitiva (código EN / UI PT)]] — canónico
- [[50_NOMENCLATURA_COPY/Mapa_Nomenclatura|Mapa completo de nomenclatura]]
- [[50_NOMENCLATURA_COPY/Copy_Universo_MANGARROSA|Copy do universo + tom de voz (Fase L)]]

### Financeiro
- [[85_FINANCEIRO/01_Registo_Despesas|Registo de despesas]]
- [[85_FINANCEIRO/02_Registo_Tempo|Registo de tempo (fases A–M)]]
- [[85_FINANCEIRO/03_Investimento_Rentabilidade|Investimento & rentabilidade]]

### Portefólio
- [[95_CASE_STUDY|Case Study — MANGARROSA]] — narrativa curada de portefólio (draft; fonte de texto, publicação visual no projecto de portefólio)

### Por migrar (checklist até apagar o Notion)
- `30_SYSTEMS` — mensagens, notificações, briefs, stories, explore, favoritos, eliminação de conta
- `10_ARCHITECTURE` / `20_SETUP` — arquitectura, grid/breakpoints, feed, setup Supabase
- `80_PRODUCT` — Free vs PRO, modelo de pagamento, backlog
- `90_LEGAL` — termos, privacidade (RGPD), cookies
- `95_BRAND` — identidade visual
- `99_SESSIONS` — condensar sessões 6–16 numa nota única de histórico
- `50_NOMENCLATURA_COPY` — histórico *Rename MATCHA → MANGARROSA*

## Decisões chave

- **Renomeação:** MATCHA → MANGARROSA (nome final do projecto).
- **Nomenclatura:** código e tabelas em **inglês**; URLs, UI e copy em **português MANGARROSA**.
- **Termos consolidados (Fase J):** Cultivar/Cultivadores (seguir), Colher (favoritar), A Colheita (analytics), Polinizar (referral) — superam Fruir/Apanhar/Polinização.
- **Modelo de pagamento:** Stripe só carrega A Cesta; PRO e Amadurecer debitam da Cesta. 1 Semente = €1, mínimo 5🌱.
- **Criativos:** PRO + Amadurecer + Polinizar. **Clientes:** só Cesta.
- **Emails (Fase K):** Opção A (Edge Functions directas) para MVP; Opção B (DB triggers + queue) pós-lançamento.
- **Botão Stripe test mode:** não ocultar via CSS (quebra o payment form); desaparece em `pk_live_`.
- **Faturação:** InvoiceXpress (AT-certificado), preços com IVA 23% incluído; Stripe invoicing não é legal em PT.
- **Camada financeira (2026-07):** adicionada `85_FINANCEIRO` (despesas, tempo, investimento) do modelo do vault-template, adaptada a produto próprio — foco em investimento acumulado, não em lucro.
- **Camada de portefólio (2026-07):** adicionado [[95_CASE_STUDY]] a partir do `95_CASE_STUDY_TEMPLATE` do vault-template — narrativa curada, fonte de texto; publicação visual vive no projecto de portefólio.
- **Roadmap de retoma (2026-07):** ordem acordada em [[70_PIPELINE/00_Roadmap_Retoma]] — docs → J → K → B → I → M → **N (design system)**. Sessões 6–16 condensadas numa nota de histórico (não migradas verbatim). Notion só se apaga após export + push + checklist.

## Decisões em aberto

- Auditoria Fase J: aplicar os termos consolidados em `FloatingNav`, `PostCard`, `OwnProfile`, `FeedAuth`, `Settings`.
- Case study: preencher timeframe, métricas pós-lançamento e refs visuais quando existirem.
- Integrações: reconciliar os flows Stripe-directos (PRO/Amadurecer) com o modelo da Cesta.
