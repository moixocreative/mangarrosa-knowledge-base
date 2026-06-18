---
projecto: MANGARROSA
tipo: referência-técnica
actualizado: 2026-06-17
tags: [overview, stack, infra]
---

# Stack e Identificadores

> Ficheiro de referência rápida. Contém IDs de teste/desenvolvimento.
> **Não colocar aqui chaves de produção nem secrets.**

## Stack

- **Frontend:** React + Vite + Tailwind
- **Backend / BD:** Supabase
- **Prototipagem / build:** Lovable
- **Versionamento:** GitHub

## Identificadores

| Item | Valor |
|---|---|
| Repo | `moixocreative/mangarrosa` (branch `development`) |
| Supabase project ID | `pevjaqrftqnstcjwdtfk` |
| Domínio | `www.mangarrosa.com` |
| Deploy actual | `matcha-app.lovable.app` (ex-MATCHA) |

## Stripe — Price IDs (test)

| Produto | Price ID |
|---|---|
| PRO 30 dias — €5 | `price_1TG5FID4FCL29KwL9CfyZubp` |
| PRO 180 dias — €25 | `price_1TG5SkD4FCL29KwLvXfTgPMW` |
| PRO 365 dias — €50 | `price_1TG5TzD4FCL29KwLx6EmhPlh` |
| Amadurecer 3 dias | `price_1TCin5D4FCL29KwLhpInW2lZ` |
| Amadurecer 7 dias | `price_1TGe4iD4FCL29KwLeENv4CfM` |
| Amadurecer 14 dias | `price_1TGe5ND4FCL29KwLeyGwehSl` |

## Emails (Fase K)

- **Envio:** Resend + Supabase SMTP, configurados com `mangarrosa.com`
- **Estado:** templates existem com placeholder `MATCHA` → actualizar para `MANGARROSA`
- Ver [[70_PIPELINE/Fase_K_Emails|Fase K — Emails]]

## Documentação de origem (Notion)

- Raiz: *Docs - MATCHA* — `31c4ecfa13268018aa4fc3aaac3fa06e`
- BUILD (página principal, ~80 sub-páginas): `31c4ecfa132680898ac1f7f7c81d45ad`
- Pasta Google Drive (migração incompleta): `1hnRtu1cntdiISz4JaFd7w5xChvhm80BC`

> O Notion foi a fonte de verdade durante o desenvolvimento. Este vault passa a ser a
> referência de trabalho a partir da migração.
