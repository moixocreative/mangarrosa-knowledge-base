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
- [[95_CASE_STUDY|Case Study — MANGARROSA]] — narrativa curada de portefólio (draft; fonte de texto, publicação visual no projecto de portefólio)

### Histórico
- [[99_SESSIONS/Historico_Sessoes|Histórico de sessões 6–17 (condensado)]]

## Migração do Notion — quase completa

Clusters principais migrados ✅. **Antes de apagar o Notion** (ver [[70_PIPELINE/00_Roadmap_Retoma]]):
1. Export do Notion em Markdown (rede de segurança).
2. Push do vault no GitHub.
3. Revisão página-a-página do que ficou por migrar (abaixo) — migrar ou descartar conscientemente.

**Extras opcionais ainda no Notion** (só migrar se tiverem valor de referência): Seed Data Plan, i18n (PT→BR→EN), Onboarding roles/Role selection, Performance, Admin Dashboard prompt, Lovable Build Guide, Segurança, PostCard v2 design, Payment Element Multibanco/MB Way (detalhe — já resumido em Stripe), Mangas & Fundadores.

## Decisões chave

- **Renomeação:** MATCHA → MANGARROSA (nome final do projecto).
- **Nomenclatura:** código e tabelas em **inglês**; URLs, UI e copy em **português MANGARROSA**.
- **Termos consolidados (Fase J):** Cultivar/Cultivadores (seguir), Colher (favoritar), A Colheita (analytics), Polinizar (referral) — superam Fruir/Apanhar/Polinização.
- **Modelo de pagamento:** Stripe só carrega A Cesta; PRO e Amadurecer debitam da Cesta. 1 Semente = €1, mínimo 5🌱.
- **Criativos:** PRO + Amadurecer + Polinizar. **Clientes:** só Cesta.
- **Amadurecer (destaques):** disponível a Free e PRO (pago via Cesta); a diferenciação PRO está na visibilidade orgânica, não no destaque.
- **Mensagens:** benefício PRO — Free só responde, não inicia conversas.
- **Emails (Fase K):** Opção A (Edge Functions directas) para MVP; Opção B (DB triggers + queue) pós-lançamento.
- **Botão Stripe test mode:** não ocultar via CSS (quebra o payment form); desaparece em `pk_live_`.
- **Faturação:** InvoiceXpress (AT-certificado), preços com IVA 23% incluído; Stripe invoicing não é legal em PT.
- **Legal:** T&C, Privacidade (RGPD) e Cookies são rascunhos que carecem de revisão jurídica; entidade legal e domínio por definir.
- **Feed:** cronológico puro no MVP; boost selectivo (destaque +7d, engagement +1h/like máx +24h nas primeiras 48h) via RPC `get_feed_posts`; scoring editorial pós-MVP.
- **Cor:** primary passa de verde (#00C896) para mango (#F6B73C); verde fica só para estados de sucesso; destaques em rose→coral; nunca flat fills.
- **Camada financeira (2026-07):** `85_FINANCEIRO` (despesas, tempo, investimento) — foco em investimento acumulado, não em lucro.
- **Camada de portefólio (2026-07):** [[95_CASE_STUDY]] a partir do template — fonte de texto; publicação visual no projecto de portefólio.
- **Roadmap de retoma (2026-07):** docs → J → K → B → I → M → **N (design system)**. Sessões 6–16 condensadas (não migradas verbatim). Notion só se apaga após export + push + checklist.

## Decisões em aberto

- Auditoria Fase J: aplicar os termos consolidados em `FloatingNav`, `PostCard`, `OwnProfile`, `FeedAuth`, `Settings`.
- Case study: preencher timeframe, métricas pós-lançamento e refs visuais quando existirem.
- Integrações: reconciliar os flows Stripe-directos (PRO/Amadurecer) com o modelo da Cesta.
- Legal: definir entidade legal, domínio de emails (legal@ / privacy@), sede/foro, e agendar revisão jurídica.
- Notion: rever os extras opcionais e decidir migrar vs. descartar antes de apagar.
