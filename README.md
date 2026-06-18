---
project: MANGARROSA
owner: Moixo (Maurício Pereira)
type: readme
---

# MANGARROSA — Knowledge Base

Marketplace criativo português de dois lados (Criativos + Clientes).
Este vault é a base de conhecimento do projecto, migrada do Notion (página *BUILD*)
e mantida em coerência com os restantes vaults (`webuddhist`, `beyond-vision`, `humanmindlab`).

## Como sincroniza

Vault Obsidian local ligado via **Local REST API MCP**.
Porta no MacBook Air: **27150**. O bearer token é específico desta máquina —
nunca copiar tokens entre máquinas (Mac Studio terá porta e token próprios).

## Estrutura de pastas

| Pasta | Conteúdo |
|---|---|
| `00_OVERVIEW/` | Estado actual, stack e identificadores |
| `10_ARCHITECTURE/` | Arquitectura, grid/breakpoints, feed, responsivo |
| `20_SETUP/` | Setup do projecto, guia de integração Supabase |
| `30_SYSTEMS/` | Mensagens, notificações, briefs, stories, explore, favoritos, eliminação de conta |
| `40_INTEGRATIONS/` | Stripe, faturação (InvoiceXpress), emails (Resend) |
| `50_NOMENCLATURA_COPY/` | Mapa de nomenclatura, regra EN/PT, copy do universo, rename |
| `60_BUILD/` | Guia de build Lovable, prompts |
| `70_PIPELINE/` | Pipeline actual + docs das fases (C, D, F, I, K, L) |
| `80_PRODUCT/` | Free vs PRO, modelo de pagamento, backlog pós-MVP |
| `90_LEGAL/` | Termos, privacidade (RGPD), cookies |
| `95_BRAND/` | Identidade visual |
| `99_SESSIONS/` | Resumos de progresso (sessões 6–17) |

Ficheiros de raiz: `README.md` (este), `CLAUDE.md` (instruções para agentes),
`INDEX.md` (índice de documentos + decisões), `CHANGELOG.md` (registo de alterações).

## Por onde começar

- [[INDEX]] — índice completo de documentos e decisões
- [[00_OVERVIEW/01_Estado_Actual|Estado actual]] — onde o projecto está
- [[70_PIPELINE/Pipeline_Actual|Pipeline]] — roadmap canónico (fases A–M)
- [[70_PIPELINE/Fase_K_Emails|Fase K — Emails]] — trabalho activo

## Vocabulário que vais ver em todo o lado

| Termo MANGARROSA | Significado |
|---|---|
| Manga 🥭 | Publicação / post |
| Cultivador | Criativo |
| Cliente | Cliente / contratante |
| Semente 🌱 | Moeda interna (1 Semente = €1) |
| A Cesta 🧺 | Carteira de créditos |
| Amadurecer | Destacar uma Manga |
| Manga Madura | Post em destaque |
| O Pomar 🌿 | Feed / feed de descoberta |
| Cultivar | Seguir |
| Polinizar | Referral / convite |
| Chamada | Brief |
| Vaga | Oferta de emprego |

## Convenções de ficheiros

- Documentos em **português europeu (PT-PT)** — convenção do projecto.
- Frontmatter YAML no topo de cada ficheiro (`projecto`, `tipo`, `tags`, `actualizado`).
- Pastas numeradas; nomes de ficheiro sem espaços (usar `_`).
- Wikilinks internos `[[pasta/ficheiro|texto]]`.

## Nota sobre agentes de IA

Ver [[CLAUDE]] para as regras de trabalho neste vault.
A fonte de verdade era o Notion (página *BUILD*); este vault passa a ser a referência
de trabalho a partir da migração de Junho 2026.
