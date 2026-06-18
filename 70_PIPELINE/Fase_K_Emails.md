---
projecto: MANGARROSA
tipo: fase
fase: K
estado: em-curso
data-origem: 2026-04-22
migrado: 2026-06-17
fonte: Notion — "FASE K — Plano de execução de emails"
tags: [pipeline, fase-k, emails, resend, supabase]
---

# Fase K — Emails (plano de execução)

> Resend e Supabase SMTP já configurados com o domínio `mangarrosa.com`.
> Templates existentes têm placeholder **MATCHA** — primeiro passo: actualizar para **MANGARROSA**.

## Triggers de email — lista completa

### 1. Supabase Auth (automáticos, geridos pelo Supabase)

| # | Trigger | Assunto | Conteúdo | Estado |
|---|---|---|---|---|
| A1 | Registo com email | Confirma a tua conta — MANGARROSA 🥭 | Link de confirmação (expira 24h) | ✅ template criado (actualizar MATCHA→MANGARROSA) |
| A2 | Reset de password | Repõe a tua password — MANGARROSA | Link de reset (expira 1h) | ✅ template criado (actualizar) |
| A3 | Alteração de email | Confirma o teu novo email — MANGARROSA | Link de confirmação do novo endereço | ✅ template criado |
| A4 | Magic Link (login sem password) | O teu link de acesso — MANGARROSA | Link directo (expira 1h) | ✅ template criado |

### 2. Transacionais via Resend

**2a. Cesta** — disparado pelo `stripe-webhook` (infra já existe)

| # | Trigger | Assunto | Conteúdo | Anexo | Estado |
|---|---|---|---|---|---|
| T1 | Carregamento Cesta (qualquer valor) | A tua Cesta foi carregada — MANGARROSA | Valor carregado + saldo actual | Fatura PDF (InvoiceXpress) | ⬜ |

**2b. PRO** — disparado por Edge Function após RPC `activate_pro_with_credits`

| # | Trigger | Assunto | Estado |
|---|---|---|---|
| T2 | PRO activado (30 dias) | PRO activo — boas-vindas ao clube 🌟 | ⬜ |
| T3 | PRO activado (180 dias) | PRO activo — boas-vindas ao clube 🌟 | ⬜ |
| T4 | PRO activado (365 dias) | PRO activo — boas-vindas ao clube 🌟 | ⬜ |

> PRO é debitado da Cesta (RPC), **não via Stripe** — o `stripe-webhook` não é chamado.
> O email deve disparar dentro da Edge Function `activate-pro` (a criar) ou via DB trigger.

**2c. Manga Madura** — disparado após update ao post

| # | Trigger | Assunto | Estado |
|---|---|---|---|
| T5 | Manga Madura activada (3 dias) | A tua Manga está Madura ⚡ | ⬜ |
| T6 | Manga Madura activada (7 dias) | A tua Manga está Madura ⚡ | ⬜ |
| T7 | Manga Madura activada (14 dias) | A tua Manga está Madura ⚡ | ⬜ |

> O destaque é processado client-side no `ModalHighlight.tsx`. O email deve sair da `handlePay`
> (via Edge Function `send-email`) ou de um DB trigger em `posts.is_highlighted`.

### 3. Alertas (cron Supabase — pg_cron)

| # | Trigger | Para quem | Assunto | Estado |
|---|---|---|---|---|
| C1 | PRO expira em 7 dias | Criativo PRO | A tua subscrição PRO expira em breve | ⬜ |
| C2 | Manga Madura expira em 2 dias | Criativo | O teu destaque expira em breve | ⬜ |
| C3 | Manga Madura expira amanhã | Criativo | Último dia do teu destaque ⚡ | ⬜ |

## Decisão de arquitectura — onde disparar PRO e Manga Madura?

- **Opção A (recomendada para MVP):** Edge Functions `send-highlight-email` / `send-pro-email`, chamadas a partir de `ModalHighlight.tsx` e `Settings.tsx` após sucesso. Simples e directa; risco: se o client fechar antes da chamada terminar, o email não sai.
- **Opção B (pós-lançamento):** DB Trigger Postgres em `posts.is_highlighted` e `users.is_pro` → escreve em `email_queue` → cron lê e envia via Resend. Robusto, independente do client; mais infra.

**Decisão:** Opção A para MVP, Opção B pós-lançamento.

## Plano de execução (por ordem)

| # | Tarefa | Depende de | Estado |
|---|---|---|---|
| K1 | Actualizar templates Supabase: MATCHA → MANGARROSA + logo | Logo em URL pública | ⬜ |
| K2 | Aplicar templates no Supabase Dashboard (Auth → Email Templates) | K1 | ⬜ |
| K3 | Testar fluxo Auth: registo + confirmação + reset password | K2 | ⬜ |
| K4 | Edge Function `send-email` (genérica) que chama Resend | `RESEND_API_KEY` no Supabase | ⬜ |
| K5 | Email após Cesta carregada (stripe-webhook já existe) | K4 | ⬜ |
| K6 | Email após PRO activado (chamar K4 no `Settings.tsx` após RPC) | K4 | ⬜ |
| K7 | Email após Manga Madura activada (chamar K4 no `ModalHighlight.tsx`) | K4 | ⬜ |
| K8 | Cron alertas: PRO 7d + Manga Madura 2/1 dia | K4 | ⬜ pós-MVP |

## Templates (copy)

### T1 — Cesta carregada
```
Assunto: A tua Cesta foi carregada 🧺
Olá [Nome],
Adicionaste [X] Sementes 🌱 à tua Cesta MANGARROSA.
Saldo actual: [Y] Sementes.
Usa-as para activar o PRO ou amadurecer as tuas Mangas.
[Ver a minha Cesta → mangarrosa.com/settings]
— MANGARROSA
```

### T2/T3/T4 — PRO activado
```
Assunto: PRO activo — boas-vindas ao clube 🌟
Olá [Nome],
A tua subscrição PRO está activa.
Válido até: [data]
O que tens agora:
• Mensagens para iniciar conversas
• Post Fixado no teu perfil (até 3)
• Analytics de todas as tuas Mangas
• Badge PRO no teu perfil
[Ver o meu perfil → mangarrosa.com/profile/me]
— MANGARROSA
```

### T5/T6/T7 — Manga Madura activada
```
Assunto: A tua Manga está Madura ⚡
Olá [Nome],
É a tua vez de brilhar no Pomar.
"[Título do post]" está agora em destaque.
Duração: [X] dias • Expira em: [data]
Acompanha a exposição em tempo real nos analytics do post.
[Ver analytics → mangarrosa.com/profile/me]
— MANGARROSA
```

### C1 — PRO expira em 7 dias
```
Assunto: A tua subscrição PRO expira em 7 dias
Olá [Nome],
O teu PRO expira a [data]. Renova para não perderes acesso às funcionalidades.
[Renovar PRO → mangarrosa.com/settings]
— MANGARROSA
```

### C2/C3 — Manga Madura expira
```
Assunto: O teu destaque expira [amanhã / em 2 dias]
Olá [Nome],
"[Título do post]" sai do destaque [amanhã / em 2 dias].
Estende mais [X] dias para manter a Manga Madura no topo do Pomar.
[Estender destaque → mangarrosa.com/profile/me]
— MANGARROSA
```

## Emails adicionais (decisão 22 Abr 2026)

### D1 — Digest quinzenal (→ semanal em velocidade cruzeiro)
Enviado a **todos os utilizadores registados** (criativos e clientes). Secções por ordem:
1. **Novos Cultivadores** — criativos registados nos últimos 15 dias (avatar + nome + disciplina)
2. **No Pomar esta semana** — novas Mangas: 🥭 Maduras primeiro → de criativos que o utilizador segue → restante por data
3. **Novas Chamadas** — briefs dos últimos 15 dias (título + cliente + disciplina + orçamento)
4. **Novas Vagas** — vagas dos últimos 15 dias (título + empresa + regime + salário)

- **Personalização:** gerado dinamicamente por utilizador → Edge Function `send-digest`
- **Periodicidade:** lançamento quinzenal (`0 9 1,15 * *`); cruzeiro semanal (`0 9 * * 1`)
- **Opt-out (RGPD):** link no rodapé + coluna `email_digest` em `users`

### N1 — Notificação PRO: novo brief publicado
- **Para:** criativos PRO (`is_pro = true`)
- **Trigger:** DB trigger em `briefs` (INSERT, status `open`) → `notify-pro-new-brief`
- **Assunto:** `Nova Chamada no Pomar — [Título do Brief]`
- **Opt-out:** `email_notify_briefs` em `users`

### N2 — Notificação PRO: nova vaga publicada
- **Para:** criativos PRO (`is_pro = true`)
- **Trigger:** DB trigger em `jobs` (INSERT, status `open`) → `notify-pro-new-job`
- **Assunto:** `Nova Vaga no Pomar — [Título da Vaga]`
- **Opt-out:** `email_notify_jobs` em `users`

> N1/N2 são **benefício exclusivo PRO** — devem aparecer na tabela comparativa em `/about`.

## Primeiro passo imediato
1. Upload do logo MANGARROSA (PNG 40px altura) para Supabase Storage → obter URL pública
2. Actualizar `supabase-email-templates.html`: MATCHA → MANGARROSA + logo + cores `#F6B73C` / `#D6456B`
3. Aplicar no Supabase Dashboard e testar com email real
