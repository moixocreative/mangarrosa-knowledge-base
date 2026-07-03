---
projecto: MANGARROSA
tipo: sistema
sistema: notificações
estado: implementado-cron-pendente
data-origem: 2026-04-08
migrado: 2026-07-03
fonte: Notion — "NOTIFICAÇÕES — Lista completa de eventos e mensagens"
tags: [systems, notificacoes]
---

# Sistema de Notificações

> Todas as notificações são **in-app**. Emails transacionais vivem em [[70_PIPELINE/Fase_K_Emails]].

## Notificações para CLIENTES / RECRUTADORES

| Tipo | Trigger | Link |
|---|---|---|
| `follow` | Alguém começou a seguir | `/profile/:username` |
| `brief_interest` | Criativo mostrou interesse no brief | `/briefs/:id/manage` |
| `job_application` | Criativo candidatou-se à vaga | `/jobs/:id/manage` |
| `message` | Nova mensagem recebida | `/messages` |
| `new_post_followed` | Criativo seguido publicou trabalho | `/post/:id` |
| `brief_expiring_7` | Brief expira em 7 dias (cron) | `/briefs/:id/manage` |
| `brief_expiring_1` | Brief expira amanhã (cron) | `/briefs/:id/manage` |

## Notificações para CRIATIVOS / AGÊNCIAS

| Tipo | Trigger | Link |
|---|---|---|
| `follow` | Alguém começou a seguir | `/profile/:username` |
| `like` | Like num post | `/post/:id` |
| `brief` | Novo brief nas disciplinas do criativo | `/briefs/:id` |
| `brief_closed` | Brief com interesse foi fechado | `/briefs/:id` |
| `brief_reopened` | Brief com interesse foi reaberto | `/briefs/:id` |
| `job` | Nova vaga publicada | `/jobs/:id` |
| `job_closed` | Vaga com candidatura encerrada | `/jobs/:id` |
| `job_reopened` | Vaga com candidatura reaberta | `/jobs/:id` |
| `new_story` | Utilizador seguido publicou história | `/feed` |
| `message` | Nova mensagem recebida | `/messages` |
| `highlight_expiring_2` | Destaque expira em 2 dias (cron) | `/post/:id` |
| `highlight_expiring_1` | Destaque expira amanhã (cron) | `/post/:id` |

> Mensagens usam **negrito** no ator/objecto (ex. "**Ana Costa** começou a seguir-te"). Nomenclatura a alinhar com o universo MANGARROSA na Fase J/L.

## Inserção no código

Implementado ✅: `follow` (`useFollows.ts`), `like` (`PostCard`/`PostDetail`), `brief_interest` (`BriefDetail`), `brief` (`CreateBrief`), `brief_closed`/`brief_reopened` (`BriefDetailClient`), `job_application` (`JobDetail`), `job` (`CreateJob`), `job_closed`/`job_reopened` (`JobDetailClient`), `new_post_followed` (`CreatePost`), `new_story` (`CreateStory`).

Pendente ⬜ (cron, pós-MVP): `brief_expiring_7/1`, `highlight_expiring_2/1`.

## Ícones (NotificationsPanel + Notifications)

`follow` UserPlus/verde · `like` Heart/red-400 · `brief_interest` FileText/#F5C542 · `brief` FileText/primary · `brief_closed` XCircle/muted · `brief_reopened` FileText/primary · `job_application` Briefcase/#F5C542 · `job` Briefcase/primary · `job_closed` XCircle/muted · `job_reopened` Briefcase/primary · `new_story` Camera/primary · `new_post_followed` ImageIcon/primary · `message` MessageCircle/primary.

## Tabela `notifications` (Supabase)

```sql
id uuid PK
user_id uuid → users
type text
actor_id uuid → users
post_id uuid → posts (nullable)
brief_id uuid → briefs (nullable)
job_id uuid → jobs (nullable)   -- via notifications_job_migration.sql
read boolean DEFAULT false
created_at timestamptz
```
