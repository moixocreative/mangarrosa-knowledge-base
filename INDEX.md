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
- [[70_PIPELINE/Pipeline_Actual|Pipeline actual (fases A–M)]]
- [[70_PIPELINE/Fase_K_Emails|Fase K — Emails (activo)]]

### Nomenclatura & Copy
- [[50_NOMENCLATURA_COPY/Regra_Definitiva_EN_PT|Regra definitiva (código EN / UI PT)]] — canónico
- [[50_NOMENCLATURA_COPY/Mapa_Nomenclatura|Mapa completo de nomenclatura]]
- [[50_NOMENCLATURA_COPY/Copy_Universo_MANGARROSA|Copy do universo + tom de voz (Fase L)]]

### Por migrar (próximos lotes)
- `50_NOMENCLATURA_COPY` — falta: *Rename MATCHA → MANGARROSA* (histórico)
- `40_INTEGRATIONS` — Stripe, faturação (InvoiceXpress), emails (Resend)
- `30_SYSTEMS` — mensagens, notificações, briefs, stories, explore, favoritos, eliminação de conta
- `10_ARCHITECTURE` / `20_SETUP` — arquitectura, grid/breakpoints, feed, setup Supabase
- `80_PRODUCT` — Free vs PRO, modelo de pagamento, backlog
- `90_LEGAL` — termos, privacidade (RGPD), cookies
- `95_BRAND` — identidade visual
- `99_SESSIONS` — sessões 6–16

## Decisões chave

- **Renomeação:** MATCHA → MANGARROSA (nome final do projecto).
- **Nomenclatura:** código e tabelas em **inglês**; URLs, UI e copy em **português MANGARROSA**.
- **Termos consolidados (Fase J):** Cultivar/Cultivadores (seguir), Colher (favoritar), A Colheita (analytics), Polinizar (referral) — superam Fruir/Apanhar/Polinização.
- **Modelo de pagamento:** Stripe só carrega A Cesta; PRO e Amadurecer debitam da Cesta. 1 Semente = €1, mínimo 5🌱.
- **Criativos:** PRO + Amadurecer + Polinizar. **Clientes:** só Cesta.
- **Emails (Fase K):** Opção A (Edge Functions directas) para MVP; Opção B (DB triggers + queue) pós-lançamento.
- **Botão Stripe test mode:** não ocultar via CSS (quebra o payment form); desaparece em `pk_live_`.

## Decisões em aberto

- Quais das sessões 6–16 migrar na íntegra vs. arquivar como superadas.
- Auditoria Fase J: aplicar os termos consolidados em `FloatingNav`, `PostCard`, `OwnProfile`, `FeedAuth`, `Settings`.
