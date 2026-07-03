---
projecto: MANGARROSA
tipo: sistema
sistema: explore
estado: implementado
data-origem: 2026-03-26
migrado: 2026-07-03
fonte: Notion — "EXPLORE — Search Behaviour"
tags: [systems, explore, descobrir, pesquisa]
---

# Explore — Comportamento de Pesquisa

> Nomenclatura MANGARROSA: Explore = **Descobrir**.

## Campos de pesquisa
- **Criativos:** nome + array de disciplinas
- **Publicações (Mangas):** título + descrição + array de disciplinas + nome do criativo

## Filtro de disciplina + pesquisa (lógica AND)
- Botão "Branding" activo **E** pesquisa "Tiago" → criativos com Branding **E** "Tiago" no nome; publicações com Branding **E** "Tiago" no título/descrição/criador.
- Só botão "Branding" (sem pesquisa) → todos com Branding.
- Só pesquisa "Terra" (sem filtro) → procura em nomes, títulos, descrições.

## Implementação
- Pesquisa automática **debounced (400ms)**, mínimo 2 caracteres.
- Pesquisa no Supabase completo (não só dados já carregados).
- Filtro de disciplina aplica-se **client-side** sobre os resultados do Supabase.
- Indicador "A pesquisar…" durante loading.

## Status
✅ Implementado em `Explore.tsx`
