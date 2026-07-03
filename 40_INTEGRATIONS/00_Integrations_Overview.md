---
projecto: MANGARROSA
tipo: índice-cluster
migrado: 2026-07-03
tags: [integrations, overview]
---

# Integrações & Serviços

Índice do cluster de integrações externas do MANGARROSA.

## Serviços

| Serviço | Função | Doc |
|---|---|---|
| **Stripe** | Pagamentos (carregar A Cesta; PRO/Amadurecer debitam da Cesta) | [[40_INTEGRATIONS/Stripe_Pagamentos]] |
| **InvoiceXpress** | Faturação certificada AT (NIF + IVA 23% + SAF-T) | [[40_INTEGRATIONS/Faturacao_InvoiceXpress]] |
| **Resend** | Emails transacionais e de ciclo de vida | [[70_PIPELINE/Fase_K_Emails]] |
| **Supabase** | BD, Auth, Edge Functions, Storage | [[00_OVERVIEW/02_Stack_e_Identificadores]] |

## Encadeamento

```
Pagamento (Stripe) → stripe-webhook →
  ├─ activa PRO / Amadurecer (ou credita A Cesta)
  ├─ emite fatura (InvoiceXpress) → email com PDF
  └─ dispara email transacional (Resend) → ver Fase K
```

## Notas transversais

- **Segredos** (`STRIPE_SECRET_KEY`, `STRIPE_WEBHOOK_SECRET`, `INVOICEXPRESS_API_KEY`, `RESEND_API_KEY`) vivem **apenas** nos secrets do Supabase Edge Functions. Nunca no vault.
- **Modelo de pagamento:** o Stripe serve para carregar A Cesta; PRO e Amadurecer debitam Sementes. Rever os flows Stripe-directos do doc de Stripe à luz disto (assinalado lá).
- **Chaves públicas** (`pk_`, `VITE_STRIPE_PUBLISHABLE_KEY`) vão no frontend via Lovable env vars — não são segredo.
