---
projecto: MANGARROSA
tipo: roadmap
estado: activo
criado: 2026-07-03
tags: [pipeline, roadmap, retoma]
---

# Roadmap de Retoma — Julho 2026

> Sequência acordada para levar o MANGARROSA do estado actual (pré-lançamento) até ao lançamento e além. Fonte de verdade para a ordem de trabalho. Detalhe de cada fase em [[70_PIPELINE/Pipeline_Actual]].

## Ordem acordada

### 1. Documentação — fechar para poder apagar o Notion
- Migrar a fundo o **evergreen** e o que se perderia se o Notion desaparecesse: `40_INTEGRATIONS`, `30_SYSTEMS`, `10_ARCHITECTURE`/`20_SETUP`, `90_LEGAL`, `95_BRAND`, `80_PRODUCT`.
- **Sessões 6–16:** NÃO migrar verbatim — condensar numa **única nota de histórico** (`99_SESSIONS/Historico_Sessoes.md`). Resolve a indefinição registada.
- **Checkpoint antes de apagar o Notion** (irreversível):
  1. Checklist de mapeamento página-a-página (migrada ✅ ou descartada conscientemente).
  2. Vault commitado + push no GitHub.
  3. **Export do Notion em Markdown** como rede de segurança (não hard-delete directo).

### 2. Fase J — Nomenclatura
Aplicar os termos consolidados (Cultivar/Cultivadores, Colher, A Colheita) em `FloatingNav`, `PostCard`, `OwnProfile`, `FeedAuth`, `Settings`, empty states e mensagens de erro. **Fechar antes da K** — o copy dos emails depende da nomenclatura final.

### 3. Fase K — Emails
K1–K8 (ver [[70_PIPELINE/Fase_K_Emails]]). **Absorve o B3** (templates de email no Supabase = K1/K2).

### 4. Fase B — Pendentes Stripe (restantes)
B4–B6: business name, statement descriptor, webhook URL. Três tarefas de dashboard (~15 min), **oportunísticas** — despachar quando já se estiver no Stripe, antes do QA do Stripe real (I6). Não é um bloco pesado.

### 5. Fase I — QA pré-lançamento
Manga Madura, referral, PRO, Stripe real (cartão real, €5), mobile 393px, desktop 1920px+, guard PRO nas mensagens. Só com J+K+B fechados.

### 6. Fase M — Limpeza de código
Remover código morto, rotas `/test*`, `console.logs`, reduzir `as any`, uniformizar padrões.

### 7. Fase N (NOVA) — Design System: tokenização + componentização
Fase autónoma, **não** um sub-ponto da M. Objectivo: design system pronto para Figma.
- Tokens W3C DTCG (`tokens.json`) → Figma Variables → Tailwind (o bridging que já usas noutros projectos).
- **Ordem interna:** tokenizar **antes** de componentizar (dá melhor resultado que o inverso).
- Pós-lançamento.

## Notas de sequência

- **J antes de K:** nomenclatura fechada evita retrabalho no copy dos emails.
- **B diluído:** B3 vive na K; B4–B6 são oportunísticos antes de I6. Não tratar B como fase-bloco.
- **Notion:** só apagar depois do checkpoint de segurança (export + push + checklist).
