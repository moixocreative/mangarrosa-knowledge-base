---
projecto: MANGARROSA
tipo: nomenclatura
estado: canónico
data-origem: 2026-04-13
migrado: 2026-06-17
fonte: Notion — "NOMENCLATURA — Regra definitiva (código EN / UI PT)"
tags: [nomenclatura, regra, código]
---

# Regra Definitiva — Código EN / UI PT

> Regra canónica de nomenclatura. Resolve a ambiguidade do [[50_NOMENCLATURA_COPY/Mapa_Nomenclatura|Mapa]]:
> **as tabelas mantêm-se em inglês** (`credits_balance`), não são renomeadas para `sementes_*`.
> O princípio "código EN, UI PT" prevalece.

## A regra

| Camada | Língua | Exemplos |
|---|---|---|
| Ficheiros React | Inglês | `PostCard.tsx`, `ReferralBlock.tsx`, `CreditsWallet.tsx` |
| Tabelas Supabase | Inglês | `credits_balance`, `credits_transactions`, `referrals` |
| Hooks / variáveis | Inglês | `useCredits`, `feedPosts`, `isHighlighted` |
| URLs | Português MANGARROSA | `/pomar`, `/manga/:id`, `/descobrir` |
| UI / Copy / Labels | Português MANGARROSA | "Sementes", "A Cesta", "Polinizar", "O Pomar" |

## Ordem de implementação

1. ✅ SQL: tabelas `credits_balance`, `credits_transactions` (migradas de `mangas_balance`/`mangas_transactions`)
2. ✅ Hook `useCredits.ts` (substitui `useMangas.ts`)
3. ⬜ `CreditsWallet.tsx` (A Cesta de Sementes)
4. ⬜ Settings: integrar `CreditsWallet` + preços em Sementes
5. ⬜ `ReferralBlock.tsx`: usar `useCredits`
6. ⬜ Fase F — Stripe Webhook
7. ⬜ Fase J — URLs em português + redirects
