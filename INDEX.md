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
- **Estado & próximo passo:** [[70_PIPELINE/Pipeline_Actual]] (fonte única)
- **Identificadores técnicos:** [[00_OVERVIEW/02_Stack_e_Identificadores]]

## Índice de documentos

### Raiz
- [[CHANGELOG]] — histórico versionado

### Overview
- [[00_OVERVIEW/02_Stack_e_Identificadores|Stack e identificadores]]

### Arquitectura & Setup
- [[10_ARCHITECTURE/Grid_Breakpoints_Feed|Grid, breakpoints e algoritmo de feed]]
- [[20_SETUP/Supabase_Integration_Guide|Supabase — guia de integração (schema BD)]]
- [[20_SETUP/Git_Workflow_Branching|Convenção de branching & PRs]]

### Pipeline
- [[70_PIPELINE/Pipeline_Actual|Pipeline actual]] — estado, roadmap e fases (fonte única)
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

### Produto
- [[80_PRODUCT/Free_vs_PRO|Free vs PRO — diferenciação de planos]]

### Legal
- [[90_LEGAL/Termos_Condicoes|Termos e Condições]] — rascunho, carece revisão advogado
- [[90_LEGAL/Politica_Privacidade_RGPD|Política de Privacidade (RGPD)]] — rascunho, carece revisão DPO
- [[90_LEGAL/Politica_Cookies|Política de Cookies]] — rascunho

### Brand
- [[95_BRAND/Identidade_Visual|Identidade Visual — Brand System]] — base para a Fase N

### Financeiro
- [[85_FINANCEIRO/01_Registo_Despesas|Registo de despesas]]
- [[85_FINANCEIRO/02_Registo_Tempo|Registo de tempo (fases A–M)]]
- [[85_FINANCEIRO/03_Investimento_Rentabilidade|Investimento & rentabilidade]]

### Portefólio
- [[95_CASE_STUDY|Case Study — MANGARROSA]] — narrativa curada (draft; publicação visual no projecto de portefólio)

### Histórico
- [[99_SESSIONS/Historico_Sessoes|Histórico de sessões 6–17 (condensado)]]

## Migração do Notion — quase completa

Clusters principais migrados ✅. **Antes de apagar o Notion:**
1. Export do Notion em Markdown (rede de segurança).
2. Push do vault no GitHub.
3. Revisão página-a-página dos extras (abaixo) — migrar ou descartar conscientemente.

**Extras opcionais ainda no Notion** (só migrar se tiverem valor de referência): Seed Data Plan, i18n (PT→BR→EN), Onboarding roles, Performance, Admin Dashboard prompt, Lovable Build Guide, Segurança, PostCard v2 design, Payment Element Multibanco/MB Way (já resumido em Stripe), Mangas & Fundadores.

## Decisões chave

> Estado das fases, ordem do roadmap e modelo de pagamento vivem no [[70_PIPELINE/Pipeline_Actual]]. Aqui ficam só decisões transversais de referência.

- **Renomeação:** MATCHA → MANGARROSA (nome final).
- **Nomenclatura:** código e tabelas em **inglês**; URLs, UI e copy em **português MANGARROSA**.
- **Termos consolidados (Fase J):** Cultivar/Cultivadores (seguir), Colher (favoritar), A Colheita (analytics), Polinizar (referral) — superam Fruir/Apanhar/Polinização.
- **Mensagens:** benefício PRO — Free só responde, não inicia conversas.
- **Emails (Fase K):** Opção A (Edge Functions directas) para MVP; Opção B (DB triggers + queue) pós-lançamento.
- **Faturação:** InvoiceXpress (AT-certificado), preços com IVA 23% incluído; Stripe invoicing não é legal em PT.
- **Legal:** T&C, Privacidade (RGPD) e Cookies são rascunhos que carecem de revisão jurídica; entidade legal e domínio por definir.
- **Feed:** cronológico puro no MVP; boost selectivo via RPC `get_feed_posts`; scoring editorial pós-MVP.
- **Cor:** primary de verde (#00C896) → mango (#F6B73C); verde só para sucesso; destaques rose→coral; nunca flat fills.
- **Camada financeira / portefólio (2026-07):** `85_FINANCEIRO` (investimento acumulado, não lucro); [[95_CASE_STUDY]] (fonte de texto, publicação no portefólio).
- **Git:** feature branch + PR → `development`; ver [[20_SETUP/Git_Workflow_Branching]].

## Decisões em aberto

- Case study: preencher timeframe, métricas pós-lançamento e refs visuais quando existirem.
- Integrações: reconciliar os flows Stripe-directos (PRO/Amadurecer) com o modelo da Cesta.
- Legal: definir entidade legal, domínio de emails (legal@ / privacy@), sede/foro, e agendar revisão jurídica.
- Notion: rever os extras opcionais e decidir migrar vs. descartar antes de apagar.
