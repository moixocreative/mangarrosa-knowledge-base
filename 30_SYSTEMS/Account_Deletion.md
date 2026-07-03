---
projecto: MANGARROSA
tipo: sistema
sistema: eliminação-de-conta
estado: por-implementar
data-origem: 2026-03-23
migrado: 2026-07-03
fonte: Notion — "ACCOUNT DELETION — Grace Period"
tags: [systems, conta, eliminacao, rgpd]
---

# Eliminação de Conta — Período de Graça

> **7 dias** de graça antes da eliminação permanente (prática de Google, Instagram, GitHub). Relevante para RGPD (direito ao esquecimento) — ver [[90_LEGAL/Politica_Privacidade_RGPD]].

## Fluxo

1. Utilizador clica "Eliminar conta" → confirma escrevendo `ELIMINAR`.
2. Estado passa a `pending_deletion`; eliminação agendada para `now + 7 dias`.
3. Email imediato: "A tua conta MANGARROSA será eliminada em 7 dias" + link de cancelamento (válido 7 dias).
4. **Durante 7 dias:** conta desactivada (invisível na pesquisa, posts ocultos); login ainda possível; banner "A tua conta está pendente de eliminação. Cancelar?".
5. **Após 7 dias (cron):** eliminação permanente — user, posts, briefs activos (fechados), guardados, notificações.

## Base de dados

```sql
-- users
deletion_requested_at timestamp NULL  -- null = activa, timestamp = pendente

-- Cron diário
DELETE FROM users
WHERE deletion_requested_at < NOW() - INTERVAL '7 days';
```

## UI

- **Modal OV5 (Confirmar Eliminação):** abaixo das consequências → "A tua conta ficará suspensa durante 7 dias antes de ser eliminada permanentemente. Podes cancelar a qualquer momento." (13px #777777)
- **Banner na página de login** (contas pendentes): `bg rgba(240,82,82,0.10)`, `border rgba(240,82,82,0.30)`, radius 8px, padding 12px 16px. Texto "A tua conta está pendente de eliminação (X dias restantes)." Botão "Cancelar eliminação" → repõe `deletion_requested_at` a null.

## Status
⬜ A implementar quando o Supabase estiver ligado.
