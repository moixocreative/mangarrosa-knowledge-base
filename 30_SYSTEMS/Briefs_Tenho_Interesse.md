---
projecto: MANGARROSA
tipo: sistema
sistema: briefs
estado: decisões-tomadas
data-origem: 2026-03-26
migrado: 2026-07-03
fonte: Notion — "BRIEFS — Tenho Interesse Flow"
tags: [systems, briefs, chamadas]
---

# Briefs — Fluxo "Tenho Interesse"

> Nomenclatura MANGARROSA: brief = **Chamada**; "Ver brief" → "Ver chamada". Termos a alinhar na Fase J/L.

## Fluxo (criativo autenticado clica "Tenho interesse")

1. Verifica se já mostrou interesse → se sim, botão "Interesse registado" (activo, não clicável); se não, avança.
2. Grava em `brief_interests` `{ user_id, brief_id }`.
3. Botão muda imediatamente para "Interesse registado" (feedback visual); contador "X criativos interessados" +1.
4. Notificação para o cliente: tipo `brief_interest`, "[criativo] mostrou interesse no teu brief [título]", link `/briefs/:id/manage`.

## Decisões tomadas ✅

- **Sem modal de confirmação** — feedback visual imediato no botão (verde, "Interesse registado").
- **Interesse não pode ser retirado** no MVP (lógica mais simples, mais comprometido).
- **Notificação automática** para o cliente.
- Cliente vê quem mostrou interesse em `/briefs/:id/manage` (antes de fechar o brief).

## A implementar

- [ ] Badge "Interesse registado" nos cards da página Briefs
- [ ] Botão "Publicar brief" só visível para clientes
- [ ] Tab "Os meus interesses" na página Briefs (só criativos autenticados)
- [ ] Secção "Briefs" no OwnProfile com os briefs em que o criativo mostrou interesse
