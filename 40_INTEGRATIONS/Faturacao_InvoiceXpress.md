---
projecto: MANGARROSA
tipo: integração
serviço: InvoiceXpress
estado: implementado-aguarda-séries
data-origem: 2026-04-05
migrado: 2026-07-03
fonte: Notion — "FATURAÇÃO — InvoiceXpress + NIF + IVA"
tags: [integrations, faturacao, invoicexpress, iva, legal]
---

# Faturação — InvoiceXpress + NIF + IVA

> [!important] Segredos
> `INVOICEXPRESS_API_KEY` vive **apenas** nos secrets do Supabase Edge Functions — nunca neste vault.

## Contexto legal

Faturas em Portugal têm de cumprir o Decreto-Lei n.º 28/2019 e ser geradas por **software certificado pela AT**. O Stripe emite invoices internacionais que **não cumprem** a legislação fiscal portuguesa (serve só como recibo informal, nunca como fatura primária).

Regras B2C:
- **Fatura simplificada:** obrigatória para montantes > €1, mesmo sem NIF.
- **Fatura completa:** quando o cliente fornece NIF (permite dedução de IVA).
- **Comunicação à AT:** via SAF-T mensal, automático pelo software certificado.

## Solução — InvoiceXpress

Software de faturação certificado AT, API REST simples (~€9/mês plano básico). [invoicexpress.com](https://www.invoicexpress.com) · [API v2 docs](https://invoicexpress.com/api-v2/documentation).

### Fluxo

```
Utilizador paga → Stripe confirma (payment_intent.succeeded)
→ stripe-webhook → API InvoiceXpress
→ Fatura criada + finalizada + enviada por email (PDF)
→ AT notificada via SAF-T mensal (automático)
```

### NIF
Recolhido no `ModalPayment.tsx` antes do formulário Stripe, guardado nos metadados do PaymentIntent, usado pelo webhook:
- **Sem NIF** → fatura simplificada (série `FATURA-SIMPLIFICADA`)
- **Com NIF** → fatura completa (série `FATURA`)

### IVA
Serviços digitais a consumidores PT: **IVA 23%**. Decisão: **preços com IVA incluído** (ex. €5 = €4.07 base + IVA), discriminado na fatura. Base calculada como `amount / 1.23`.

## Implementação técnica

### Variáveis de ambiente (secrets Supabase)
- `INVOICEXPRESS_API_KEY` — Configurações → API
- `INVOICEXPRESS_ACCOUNT` — subdomínio da conta (ex. `account.app.invoicexpress.com`)

### Campo NIF (`ModalPayment.tsx`)
```typescript
const [nif, setNif] = useState('');
// no body do invoke:
body: { price_id: priceId, user_id: userId, type, post_id: postId, nif: nif || null }
```
```tsx
<div className="space-y-1.5">
  <label className="text-[11px] uppercase tracking-widest text-muted-foreground">
    NIF (opcional — para fatura com NIF)
  </label>
  <input type="text" inputMode="numeric" placeholder="000000000"
    value={nif}
    onChange={e => setNif(e.target.value.replace(/\D/g, '').slice(0, 9))}
    className="w-full px-3 py-2.5 rounded-lg bg-[rgba(255,255,255,0.04)] border border-[rgba(255,255,255,0.12)] text-sm text-foreground placeholder:text-muted-foreground focus:outline-none focus:border-primary transition-colors" />
</div>
```

### `create-payment-intent` — nif nos metadados
```typescript
const { price_id, user_id, post_id, type, nif } = await req.json();
metadata: { user_id, price_id, type, days: String(plan.days), nif: nif ?? '', ...(post_id ? { post_id } : {}) }
```

### `stripe-webhook` — emitir fatura
```typescript
async function emitirFatura(params: {
  userName: string; userEmail: string; nif: string | null;
  planLabel: string; amount: number; // cêntimos
}) {
  const ACCOUNT = Deno.env.get('INVOICEXPRESS_ACCOUNT')!;
  const API_KEY = Deno.env.get('INVOICEXPRESS_API_KEY')!;

  const total = params.amount / 100;
  const base = parseFloat((total / 1.23).toFixed(2)); // IVA 23% incluído
  const tipo_doc = params.nif ? 'invoices' : 'simplified_invoices';
  const serie = params.nif ? 'FATURA' : 'FATURA-SIMPLIFICADA';

  const body = {
    invoice: {
      date: new Date().toLocaleDateString('pt-PT', { day: '2-digit', month: '2-digit', year: 'numeric' }),
      due_date: new Date().toLocaleDateString('pt-PT', { day: '2-digit', month: '2-digit', year: 'numeric' }),
      sequence_id: serie,
      client: {
        name: params.userName || 'Consumidor Final',
        email: params.userEmail,
        ...(params.nif ? { fiscal_id: params.nif, country: 'PT' } : {}),
      },
      items: [{
        name: params.planLabel,
        description: 'Serviço digital — plataforma MANGARROSA',
        quantity: '1', unit_price: String(base), unit: 'Serviço', tax_name: 'IVA23',
      }],
      tax_exemption: null,
    },
  };

  const res = await fetch(`https://${ACCOUNT}.app.invoicexpress.com/${tipo_doc}.json?api_key=${API_KEY}`,
    { method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify(body) });
  if (!res.ok) { console.error('InvoiceXpress error:', await res.text()); return; }

  const { invoice } = await res.json();
  // Finalizar
  await fetch(`https://${ACCOUNT}.app.invoicexpress.com/${tipo_doc}/${invoice.id}/change-state.json?api_key=${API_KEY}`,
    { method: 'PUT', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify({ invoice: { state: 'finalized' } }) });
  // Enviar por email
  await fetch(`https://${ACCOUNT}.app.invoicexpress.com/${tipo_doc}/${invoice.id}/email-document.json?api_key=${API_KEY}`,
    { method: 'PUT', headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ message: { client: { email: params.userEmail, save: '0' }, cc: '', subject: 'A tua fatura MANGARROSA', body: 'Segue em anexo a tua fatura. Obrigado!' } }) });
}
```

> Nota: strings de copy (`MATCHA` → `MANGARROSA`) a actualizar no código ao aplicar.

## Passos de setup (InvoiceXpress)

1. Criar conta (trial 30 dias) → Configurações → Dados da empresa (nome, NIF, morada, email).
2. **Séries de documentos:** criar `FATURA` (com NIF) e `FATURA-SIMPLIFICADA` (sem NIF) → **comunicar à AT** (botão no InvoiceXpress).
3. **Impostos:** confirmar taxa `IVA23` (23%), definir como padrão.
4. **API:** gerar API Key + guardar Account Name → adicionar aos secrets Supabase.
5. Aplicar alterações de código (ModalPayment, create-payment-intent, stripe-webhook).
6. **Testar em sandbox** (Configurações → Sandbox): pagamento teste Stripe (4242…) → verificar fatura criada + email com PDF → desactivar sandbox → teste real.
7. **SAF-T:** Configurações → Comunicações AT (activo por defeito).

## Estado

- **Decisão:** ✅ InvoiceXpress (AT-certificado)
- **IVA:** ✅ Preços com IVA 23% incluído, discriminado
- **Conta:** ✅ Criada — account name `cinapcentrodeinfo`
- **Secrets Supabase:** ✅ `INVOICEXPRESS_API_KEY` e `INVOICEXPRESS_ACCOUNT` adicionados
- **Código:** ✅ Ficheiros entregues (aguardam séries para deploy final)
- **Séries de documentos:** 🔜 criar `FATURA` + `FATURA-SIMPLIFICADA` → comunicar à AT
- **Taxa IVA23:** 🔜 verificar em Definições → Impostos
