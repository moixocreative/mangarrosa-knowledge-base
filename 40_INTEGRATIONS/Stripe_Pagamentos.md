---
projecto: MANGARROSA
tipo: integração
serviço: Stripe
estado: infra-válida-flow-superado
data-origem: 2026-03-28
migrado: 2026-07-03
fonte: Notion — "STRIPE — PRO + Highlight — Plano de Implementação"
tags: [integrations, stripe, pagamentos, pro, amadurecer]
---

# Stripe — Pagamentos (PRO + Amadurecer)

> [!warning] Flow superado pelo modelo da Cesta
> Este doc (28 Mar) descreve pagamento **Stripe-directo** para PRO e Highlight (checkout one-time por transacção). O modelo consolidado posterior é: **Stripe só carrega A Cesta**; PRO e Amadurecer **debitam Sementes da Cesta** (não chamam o Stripe). Ver [[70_PIPELINE/Pipeline_Actual|modelo de pagamento]].
> **O que continua válido:** infra do webhook, edge functions, SQL, price IDs, variáveis de ambiente. **O que mudou:** o gatilho — PRO/Amadurecer já não abrem Stripe Checkout; a UI debita da carteira.

> [!important] Segredos
> `STRIPE_SECRET_KEY` e `STRIPE_WEBHOOK_SECRET` vivem **apenas** nos secrets do Supabase — nunca neste vault. Valores redigidos abaixo de propósito.

## Contexto original

PRO **não recorrente**: o criativo paga, tem acesso por X tempo, decide se renova ao expirar. `is_pro` é derivado de `pro_expires_at > now()` (verificado no login e em Settings). Posts feitos como PRO não são suspensos ao expirar — só novos uploads voltam ao limite free.

## Price IDs — PRO (test mode)

| Plano | Preço | Dias | Price ID |
|---|---|---|---|
| Mensal | €5 | 30 | `price_1TG5FID4FCL29KwL9CfyZubp` |
| Semestral | €25 | 180 | `price_1TG5SkD4FCL29KwLvXfTgPMW` |
| Anual | €50 | 365 | `price_1TG5TzD4FCL29KwLx6EmhPlh` |

## Price IDs — Amadurecer/Highlight (test mode)

| Duração | Preço | Dias | Price ID |
|---|---|---|---|
| 3 dias | €10 | 3 | `price_1TCin5D4FCL29KwLhpInW2lZ` |
| 7 dias | €18 | 7 | `price_1TGe4iD4FCL29KwLeENv4CfM` |
| 14 dias | €30 | 14 | `price_1TGe5ND4FCL29KwLeyGwehSl` |

## SQL

```sql
-- Colunas PRO no user
ALTER TABLE public.users ADD COLUMN IF NOT EXISTS is_pro boolean DEFAULT false;
ALTER TABLE public.users ADD COLUMN IF NOT EXISTS pro_expires_at timestamptz DEFAULT null;

-- Tabela highlights
CREATE TABLE IF NOT EXISTS public.highlights (
  id uuid DEFAULT gen_random_uuid() PRIMARY KEY,
  user_id uuid REFERENCES public.users(id) ON DELETE CASCADE,
  post_id uuid REFERENCES public.posts(id) ON DELETE CASCADE,
  stripe_session_id text,
  duration_days int NOT NULL,
  price_paid numeric NOT NULL,
  starts_at timestamptz DEFAULT now(),
  expires_at timestamptz NOT NULL,
  created_at timestamptz DEFAULT now()
);
```

## Edge Functions

| Função | Estado | Notas |
|---|---|---|
| `create-checkout-pro` | ✅ Existente | Fallback — substituída pelo modal embedded / Cesta |
| `stripe-webhook` | ✅ Existente | JWT = OFF; escuta `checkout.session.completed` + `payment_intent.succeeded` |
| `create-payment-intent` | ✅ Deploy feito | JWT = ON; card + Multibanco + MB Way |

## Variáveis de ambiente

| Nome | Onde | Notas |
|---|---|---|
| `STRIPE_SECRET_KEY` | Supabase → Edge Functions → Secrets | `sk_test_` / `sk_live_` — **redigido** |
| `STRIPE_WEBHOOK_SECRET` | Supabase → Edge Functions → Secrets | `whsec_` — **redigido** |
| `SITE_URL` | Supabase → Edge Functions → Secrets | URL base da app (actualizar para produção) |
| `VITE_STRIPE_PUBLISHABLE_KEY` | Lovable → Environment Variables | `pk_` — pública, vai para o frontend |
| `SUPABASE_URL` / `SUPABASE_SERVICE_ROLE_KEY` | automático | Injectado pelo Supabase |

## Webhook endpoint (Stripe)

- URL: `https://pevjaqrftqnstcjwdtfk.supabase.co/functions/v1/stripe-webhook`
- Eventos: `checkout.session.completed`, `payment_intent.succeeded`
- Signing secret: **redigido** (só no Supabase)

> ⚠️ Produção: actualizar `SITE_URL` e o URL do endpoint no Stripe ao migrar de `pk_test`/`sk_test` para `live`.

## Pagamentos locais (Multibanco + MB Way)

`create-payment-intent` (JWT ON) e `ModalPayment.tsx` (Payment Element embedded) suportam card + Multibanco + MB Way. Activar os métodos em Stripe Dashboard → Settings → Payment Methods, e adicionar `payment_intent.succeeded` ao webhook.

## Estado (à data de origem)

Implementado ✅: produtos e price IDs, edge functions (checkout-pro, webhook, payment-intent), `ModalPayment.tsx`, secção PRO em Settings, badge PRO (OwnProfile/Profile/CreativeCard), `useAuth` expõe `is_pro`/`pro_expires_at`/`refreshProfile`, acumulação de planos no webhook, `ModalHighlight` (2 fases), `ModalHighlightAnalytics` (dados reais), `useTrackView` + `post_views_migration.sql`, testado end-to-end em test mode.

Pendente ⬜:
- Correr `post_views_migration.sql` no Supabase SQL Editor
- Deploy do `stripe-webhook` actualizado
- Teste end-to-end (PRO + Amadurecer, card + Multibanco + MB Way)
- Regenerar tipos TS: `npx supabase gen types typescript --project-id pevjaqrftqnstcjwdtfk --schema public > src/integrations/supabase/types.ts`
- Remover casts `as any` em `ModalHighlightAnalytics.tsx` e `useTrackView.ts` (após regenerar tipos)
- Emails transacionais (Resend) → [[70_PIPELINE/Fase_K_Emails]]

> [!note] Reconciliar com o modelo da Cesta
> Rever quais destes flows/edge functions ainda se aplicam sob o modelo "Stripe só carrega A Cesta". Provável: `create-payment-intent` passa a servir só o carregamento da Cesta; PRO/Amadurecer deixam de ter checkout próprio.
