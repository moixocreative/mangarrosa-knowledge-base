---
projecto: MANGARROSA
tipo: sistema
sistema: favoritos
estado: por-implementar
data-origem: 2026-03-23
migrado: 2026-07-03
fonte: Notion — "FAVORITES — Access and Privacy"
tags: [systems, favoritos, colher, privacidade]
---

# Favoritos — Acesso e Privacidade

> Nomenclatura MANGARROSA: guardar/favoritar = **Colher**; favoritos = Mangas colhidas.

## Decisão
Favoritos (posts guardados) são **privados** — só o dono os vê. Outros utilizadores a visitar um perfil **não** vêem a secção de guardados.

## Pontos de entrada
1. **Perfil próprio (`/profile/me`):** link/tab "Guardados" visível **só** ao dono. Não aparece em `/profile/:username` de outros.
2. **Dropdown do FloatingNav:** "Guardados" como terceira opção no dropdown Perfil (Ver perfil → `/profile/me`, Notificações → `/notifications`, Guardados → `/favorites`). Ícone bookmark #F5C542 se houver guardados.
3. **URL directo `/favorites`:** só autenticado; senão redirect para `/`.

## O que outros vêem num perfil
`/profile/:username` mostra: avatar, nome, bio, disciplina, links, grelha de posts públicos. **Sem acesso aos guardados** — completamente ocultos.

## Status
⬜ A implementar no Lovable.
