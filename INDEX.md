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

### Arquitectura & Setup
- [[10_ARCHITECTURE/Grid_Breakpoints_Feed|Grid, breakpoints e algoritmo de feed]]
- [[20_SETUP/Supabase_Integration_Guide|Supabase — guia de integração (schema BD)]]

### Pipeline
- [[70_PIPELINE/00_Roadmap_Retoma|Roadmap de retoma (Julho 2026)]] — ordem de trabalho acordada
- [[70_PIPELINE/Pipeline_Actual|Pipeline actual (fases A–M)]]
- [[70_PIPELINE/Fase_K_Emails|Fase K — Emails (activo)]]

### Sistemas
- [[30_SYSTEMS/00_Systems_Overview|Sistemas (índice)]]
- [[30_SYSTEMS/Mensagens|Mensagens]] · [[30_SYSTEMS/Notificacoes|Notificações]] · [[30_SYSTEMS/Briefs_Tenho_Interesse|Briefs (Chamadas)]]
- [[30_SYSTEMS/Stories|Stories]] · [[30_SYSTEMS/Explore_Search|Explore]] · [[30_SYSTEMS/Favorites|Favoritos]] · [[30_SYSTEMS/Account_Deletion|Eliminação de conta]]

### Integrações
- [[40_INTEGRATIONS/00_Integrations_Overview|Integrações & Serviços (índice)]]
- [[40_INTEGRATIONS/Stripe_Pagamentos|Stripe — Pagamentos (PRO + Amadurecer)]]
- [[40_INTEGRATIONS/Faturacao_InvoiceXpress|Faturação — InvoiceXpress + NIF + IVA]]

### Nomenclatura & Copy
- [[50_NOMENCLATURA_COPY/Regra_Definitiva_EN_PT|Regra definitiva (código EN / UI PT)]] — canónico
- [[50_NOMENCLATURA_COPY/Mapa_Nomenclatura|Mapa completo de nomenclatura]]
- [[50_NOMENCLATURA_COPY/Copy_Universo_MANGARROSA|Copy do universo + tom de voz (Fase L)]]

### Legal
- [[90_LEGAL/Termos_Condicoes|Termos e Condições]] — rascunho, carece revisão advogado
- [[90_LEGAL/Politica_Privacidade_RGPD|Política de Privacidade (RGPD)]] — rascunho, carece revisão DPO
- [[90_LEGAL/Politica_Cookies|Política de Cookies]] — rascunho

### Financeiro
- [[85_FINANCEIRO/01_Registo_Despesas|Registo de despesas]]
- [[85_FINANCEIRO/02_Registo_Tempo|Registo de tempo (fases A–M)]]
- [[85_FINANCEIRO/03_Investimento_Rentabilidade|Investimento & rentabilidade]]

### Portefólio
- [[95_CASE_STUDY|Case Study — MANGARROSA]] — narrativa curada de portefólio (draft; fonte de texto, publicação visual no projecto de portefólio)

### Por migrar (checklist até apagar o Notion)
- `80_PRODUCT` — Free vs PRO, modelo de pagamento, backlog
- `95_BRAND` — identidade visual
- `99_SESSIONS` — condensar sessões 6–16 numa nota única de histórico
- `50_NOMENCLATURA_COPY` — histórico *Rename MATCHA → MANGARROSA*
- Extras opcionais: seed data plan, i18n, onboarding roles, performance

## Decisões chave

- **Renomeação:** MATCHA → MANGARROSA (nome final do projecto).
- **Nomenclatura:** código e tabelas em **inglês**; URLs, UI e copy em **português MANGARROSA**.
- **Termos consolidados (Fase J):** Cultivar/Cultivadores (seguir), Colher (favoritar), A Colheita (analytics), Polinizar (referral) — superam Fruir/Apanhar/Polinização.
- **Modelo de pagamento:** Stripe só carrega A Cesta; PRO e Amadurecer debitam da Cesta. 1 Semente = €1, mínimo 5🌱.
- **Criativos:** PRO + Amadurecer + Polinizar. **Clientes:** só Cesta.
- **Emails (Fase K):** Opção A (Edge Functions directas) para MVP; Opção B (DB triggers + queue) pós-lançamento.
- **Botão Stripe test mode:** não ocultar via CSS (quebra o payment form); desaparece em `pk_live_`.
- **Faturação:** InvoiceXpress (AT-certificado), preços com IVA 23% incluído; Stripe invoicing não é legal em PT.
- **Legal:** T&C, Privacidade (RGPD) e Cookies são rascunhos que carecem de revisão jurídica antes de publicar; entidade legal e domínio por definir.
- **Mensagens:** benefício PRO — Free só responde, não inicia conversas.
- **Feed:** cronológico puro no MVP; algoritmo com boost selectivo (destaque +7d, engagement +1h/like máx +24h nas primeiras 48h) via RPC `get_feed_posts`; scoring editorial pós-MVP.
- **Grid:** destaques ocupam 2×2 na posição cronológica (`grid-flow-dense`), não são movidos para o topo.
- **Camada financeira (2026-07):** adicionada `85_FINANCEIRO` (despesas, tempo, investimento) do modelo do vault-template, adaptada a produto próprio — foco em investimento acumulado, não em lucro.
- **Camada de portefólio (2026-07):** adicionado [[95_CASE_STUDY]] a partir do `95_CASE_STUDY_TEMPLATE` do vault-template — narrativa curada, fonte de texto; publicação visual vive no projecto de portefólio.
- **Roadmap de retoma (2026-07):** ordem acordada em [[70_PIPELINE/00_Roadmap_Retoma]] — docs → J → K → B → I → M → **N (design system)**. Sessões 6–16 condensadas numa nota de histórico (não migradas verbatim). Notion só se apaga após export + push + checklist.

## Decisões em aberto

- Auditoria Fase J: aplicar os termos consolidados em `FloatingNav`, `PostCard`, `OwnProfile`, `FeedAuth`, `Settings`.
- Case study: preencher timeframe, métricas pós-lançamento e refs visuais quando existirem.
- Integrações: reconciliar os flows Stripe-directos (PRO/Amadurecer) com o modelo da Cesta.
- Legal: definir entidade legal, domínio de emails (legal@ / privacy@), sede/foro, e agendar revisão jurídica.
