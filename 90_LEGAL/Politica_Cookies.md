---
projecto: MANGARROSA
tipo: legal
documento: política-de-cookies
estado: rascunho-carece-revisão-advogado
versão: 1.0
data-origem: 2026-04
migrado: 2026-07-03
fonte: Notion — "POLÍTICA DE COOKIES — MATCHA"
tags: [legal, cookies, consentimento]
---

# Política de Cookies — MANGARROSA

> [!warning] Rascunho de trabalho
> Versão 1.0 · rever com advogado antes de publicar.
> **Nota de nomenclatura (Fase L):** as chaves de cookie foram renomeadas no código de `matcha_*` → `mangarrosa_*`. Este doc usa já os nomes actuais.

## O que são cookies

Pequenos ficheiros de texto guardados no dispositivo ao visitar um website, para "lembrar" informação entre visitas ou durante a sessão.

## Cookies que utilizamos

### Obrigatórios (não requerem consentimento)

| Cookie | Emissor | Finalidade | Duração |
|---|---|---|---|
| `sb-*` (session) | Supabase | Mantém a sessão autenticada | Sessão / 1 semana |
| `sb-auth-token` | Supabase | Token JWT | 1 semana |
| `mangarrosa_cookie_consent` | MANGARROSA | Guarda a preferência de cookies | 1 ano |
| `mangarrosa_welcome_*` | MANGARROSA | Controla se já viu o ecrã de boas-vindas | LocalStorage |

Estritamente necessários — não podem ser recusados sem perder funcionalidades essenciais.

### Analíticos (requerem consentimento)

| Cookie | Emissor | Finalidade | Duração |
|---|---|---|---|
| `_ga` | Google Analytics | Identifica utilizadores únicos | 2 anos |
| `_ga_*` | Google Analytics | Estado da sessão | 2 anos |
| `_gid` | Google Analytics | Distingue utilizadores | 24 horas |

Google Analytics 4 com **anonimização de IP activada**, dados agregados e anónimos. Só carregam após consentimento expresso.

### Pagamentos (activados apenas durante checkout)

| Cookie | Emissor | Finalidade | Duração |
|---|---|---|---|
| `__stripe_mid` | Stripe | Deteção de fraude | 1 ano |
| `__stripe_sid` | Stripe | Sessão de pagamento | 30 minutos |

Necessários para processamento seguro de pagamentos; activados só ao iniciar um pagamento.

## Cookie Consent Bar — implementação

Barra na primeira visita, com duas opções:
- **Aceitar todos** — activa cookies analíticos
- **Apenas essenciais** — recusa analíticos

Preferência guardada em `localStorage` na chave `mangarrosa_cookie_consent` (valor `all` ou `essential`). O GA só inicializa se o valor for `all`.

**Ficheiros:**
- `src/components/CookieConsent.tsx` — barra de consentimento
- `src/lib/analytics.ts` — inicializa GA4 só com consentimento
- Inserir `<CookieConsent />` no `App.tsx`

## Como gerir preferências

A qualquer momento em **Definições → Privacidade** ou no link "Preferências de cookies" no rodapé. Ou no browser: Chrome `chrome://settings/cookies`, Firefox `about:preferences#privacy`, Safari Preferências > Privacidade.

## Contacto

Questões sobre cookies e privacidade: **privacy@[domínio]**
