---
project: MANGARROSA
owner: Moixo (Maurício Pereira)
type: agent-instructions
---

# CLAUDE.md

Instruções para agentes de IA a trabalhar neste vault.

## O que é este vault

Base de conhecimento do **MANGARROSA** — marketplace criativo português de dois lados
(Cultivadores/Criativos + Clientes). Stack: React + Vite + Tailwind + Supabase + Lovable.
Migrado do Notion em Junho 2026.

## Estrutura de pastas

`00_OVERVIEW` (estado, stack) · `10_ARCHITECTURE` · `20_SETUP` · `30_SYSTEMS` ·
`40_INTEGRATIONS` (Stripe, faturação, emails) · `50_NOMENCLATURA_COPY` · `60_BUILD` ·
`70_PIPELINE` (fases + Fase K activa) · `80_PRODUCT` · `90_LEGAL` · `95_BRAND` · `99_SESSIONS`.

### Ficheiros de tráfego alto
- [[70_PIPELINE/Pipeline_Actual]] — estado canónico do roadmap
- [[70_PIPELINE/Fase_K_Emails]] — trabalho activo (emails)
- [[00_OVERVIEW/02_Stack_e_Identificadores]] — IDs, Stripe, Supabase

## Por onde começar
[[INDEX]] → [[70_PIPELINE/Pipeline_Actual]] (estado + roadmap) → [[70_PIPELINE/Fase_K_Emails]] (activo).

## Vocabulário do projecto
Manga (post) · Cultivador (criativo) · Cliente · Semente 🌱 (moeda, 1€) · A Cesta 🧺 (carteira) ·
Amadurecer (destacar) · Manga Madura (destaque) · O Pomar 🌿 (feed) · Cultivar (seguir) ·
Polinizar (referral) · Chamada (brief) · Vaga (emprego).

## Equipa
Projecto a solo. **Moixo (Maurício Pereira)** — fundador, product owner, design e desenvolvimento.

## Recursos do projecto
- Repo: `moixocreative/mangarrosa` (branch `development`)
- Supabase project ID: `pevjaqrftqnstcjwdtfk`
- Domínio: `www.mangarrosa.com` · Deploy: `matcha-app.lovable.app`
- Notion (origem): página *BUILD* `31c4ecfa132680898ac1f7f7c81d45ad`

## Cuidados de conteúdo
- O projecto chamou-se **MATCHA** durante o desenvolvimento; foi renomeado **MANGARROSA**.
  Há docs e templates antigos com "MATCHA" — em migração. Não assumir MATCHA como nome actual.
- Alguns docs de sessões antigas estão superados pela [[70_PIPELINE/Pipeline_Actual]].

## Ao escrever notas novas
- PT-PT. Frontmatter YAML (`projecto`, `tipo`, `tags`, `actualizado`).
- Preferir `vault_write` (ficheiro completo) a múltiplos `vault_patch` em reescritas complexas.
- Nomes de ficheiro sem espaços (`_`); colocar na pasta numerada correcta.
- Actualizar [[CHANGELOG]] e [[INDEX]] ao adicionar/mover documentos relevantes.

## Wikilinks Obsidian
Usar `[[pasta/ficheiro|texto visível]]`. Verificar que o alvo existe.

## Higiene de git
Vault sincronizado via plugin Obsidian Git (quando configurado). Commits claros e atómicos.
