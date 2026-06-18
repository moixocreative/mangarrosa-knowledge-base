---
projecto: MANGARROSA
tipo: copy
fase: L
estado: parcial
data-origem: 2026-04-21
migrado: 2026-06-17
fonte: Notion — "FASE L — Copy universo MANGARROSA"
tags: [copy, fase-l, tom-de-voz, nomenclatura]
---

# Copy do Universo MANGARROSA (Fase L)

> Auditar e ajustar toda a linguagem ao universo criativo tropical do MANGARROSA.
> Não é tradução de termos — é voz, tom e coerência narrativa em cada ecrã.
>
> [!note] Esta página resolve a divergência de nomenclatura
> A "Terminologia definitiva" abaixo (21 Abr) é a versão consolidada: **Cultivar / Cultivadores / Colher**.
> Supera os termos *Fruir / Apanhar* do [[50_NOMENCLATURA_COPY/Mapa_Nomenclatura|Mapa de 13 Abr]].

## Páginas institucionais ✅ concluídas

| Ficheiro | O que mudou |
|---|---|
| `AboutPage.tsx` | MATCHA → MANGARROSA, "Pomar" no hero, Cesta/Sementes/Amadurecer nos preços, tabela de funcionalidades, secção para clientes |
| `TermsPage.tsx` | MATCHA → MANGARROSA, emails legais, Secção 2 (Definições) com nomenclatura, Secção 5 (Pagamentos) reescrita |
| `PrivacyPage.tsx` | MATCHA → MANGARROSA, emails, referências à Cesta e histórico de Sementes na retenção |
| `CookiesPage.tsx` | MATCHA → MANGARROSA, `matcha_cookie_consent` → `mangarrosa_cookie_consent`, `matcha_welcome_*` → `mangarrosa_welcome_*` |

> [!important] Placeholder legal
> Ficheiros legais têm `[Entidade Legal — a preencher]` → substituir pelo nome legal correcto antes do lançamento.
> Emails legais: `legal@mangarrosa.com` e `privacy@mangarrosa.com` — confirmar que existem e estão activos.

## Páginas de produto — a auditar

| Componente | Prioridade | Estado |
|---|---|---|
| `FloatingNav.tsx` — labels de navegação | Alta | ⬜ |
| `PostCard.tsx` — acções (Guardar, Partilhar, Amadurecer) | Alta | ⬜ |
| `OwnProfile.tsx` — "Publicações", "Favoritos", "Seguidores", "A seguir" | Alta | ⬜ |
| `FeedAuth.tsx` — "Descobrir", "A Seguir" | Alta | ⬜ |
| `Settings.tsx` — labels gerais, erros | Alta | ⬜ |
| `CreditsWallet.tsx` — verificar se já em MANGARROSA | Média | ⬜ |
| `ModalHighlight.tsx` | — | ✅ |
| `StoriesBar.tsx` — CTA "Criar história" | Média | ⬜ |
| Empty states (todas as páginas) | Média | ⬜ |
| Mensagens de erro e validação | Baixa | ⬜ |
| Tooltips e helpers | Baixa | ⬜ |

## Terminologia definitiva (referência canónica)

| Termo genérico | MANGARROSA |
|---|---|
| Publicação / Post | Manga 🥭 |
| Feed de Descoberta | Pomar 🌿 |
| Seguir | Cultivar 🌱 |
| A seguir | Cultivando |
| Seguidores | Cultivadores |
| Guardar / Favoritar | Colher |
| Analytics | A Colheita |
| Destacar | Amadurecer |
| Post em Destaque | Manga Madura |
| Wallet de créditos | A Cesta 🧺 |
| Créditos / Sementes | Sementes 🌱 |
| Convite / Referral | Semente (convite) |

## Tom de voz — guia rápido

- **Quente, directo, sem arrogância.** Fala como um criativo, não como um departamento de marketing.
- **Tropical, mas não kitsch.** Metáforas do pomar com naturalidade — não em cada frase.
- **Português de Portugal como base.** Evitar construções BR artificiais; vocabulário reconhecível em ambos os mercados.
- **CTAs accionáveis e específicos.** "Plantar a minha primeira Manga" em vez de "Começar"; "Explorar o Pomar" em vez de "Ver mais".
- **Erros humanos, não robóticos.** "Algo não correu bem — tenta de novo." em vez de "Error 500".

## Próximos passos
1. Auditar `FloatingNav`, `PostCard`, `OwnProfile` (labels de secção)
2. Auditar `FeedAuth` e `Settings`
3. Rever empty states e CTAs
4. Rever copy da landing `/join` com o mesmo tom
5. Alinhar copy dos emails (Fase K) com o mesmo universo
