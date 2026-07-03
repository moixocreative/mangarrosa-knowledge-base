---
projecto: MANGARROSA
tipo: setup
tópico: git-workflow
criado: 2026-07-03
tags: [setup, git, branching, workflow, boas-práticas]
---

# Convenção de Branching & PRs

> Boa prática acordada (2026-07-03). Candidata a subir ao `workflow-template`.

## Regra geral

Não commitar features directamente no `development`. Para cada trabalho: **criar branch → PR → merge para `development`**.

## Caveat específico deste projecto

O **Lovable está ligado ao `development` e commita aí directamente** a cada prompt. Logo, o `development` anda constantemente. Consequências práticas:

- **Ramificar sempre do `development` mais recente:** `git pull` antes de criar o branch.
- **Branches curtos:** feature pequena, merge rápido (quanto mais tempo vivo, mais diverge do que o Lovable vai commitando).
- **Antes do merge, trazer o `development` para o branch** (`git merge origin/development` ou rebase) — resolver conflitos no branch, não no `development`.
- Assim, conflitos (ex. dois branches a mexer no botão de seguir) aparecem no **PR com review**, não num merge local às cegas.

## Nomenclatura de branches

Prefixos convencionais:
- `feat/` — nova funcionalidade
- `fix/` — correcção de bug
- `refactor/` — reestruturação sem mudar comportamento
- `chore/` — manutenção, deps, config
- `docs/` — documentação

Exemplos: `feat/emails-resend`, `fix/conditionally-render-seguir-button`, `refactor/nomenclatura-cultivar`.

## Fluxo típico

```bash
git checkout development && git pull        # base actualizada
git checkout -b refactor/nome-descritivo    # branch
# ... trabalho + commits ...
git merge origin/development                 # trazer o que o Lovable commitou
# ... resolver conflitos se houver ...
git push -u origin refactor/nome-descritivo  # publicar
# → abrir PR para development no GitHub → review → merge
```

## Nota histórica
A Fase J (nomenclatura Cultivar/Cultivando) foi commitada **directamente** no `development` — funcionou, mas o correcto teria sido `refactor/nomenclatura-cultivar` + PR. Fica como referência do que fazer a partir daqui.
