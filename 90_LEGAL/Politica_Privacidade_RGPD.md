---
projecto: MANGARROSA
tipo: legal
documento: política-de-privacidade
estado: rascunho-carece-revisão-advogado
versão: 1.0
conformidade: RGPD (UE) 2016/679
data-origem: 2026-04
migrado: 2026-07-03
fonte: Notion — "POLÍTICA DE PRIVACIDADE — MATCHA (RGPD)"
tags: [legal, privacidade, rgpd, dpo]
---

# Política de Privacidade — MANGARROSA (RGPD)

> [!warning] Rascunho de trabalho
> Versão 1.0 · **Conformável com RGPD (UE) 2016/679**. Deve ser revista por advogado/DPO antes de publicar. Placeholders `[…]` por preencher.

## 1. Responsável pelo tratamento

**[Nome da entidade legal]**, com sede em Portugal, é o responsável pelo tratamento dos dados recolhidos através da Plataforma MANGARROSA. Encarregado de Proteção de Dados (DPO): **privacy@[domínio]**

## 2. Dados recolhidos e finalidades

| Categoria | Exemplos | Finalidade | Base legal |
|---|---|---|---|
| Identificação | Nome, email, username | Criação e gestão de conta | Execução de contrato |
| Perfil | Avatar, bio, portefólio, disciplina, localização | Apresentação do perfil público | Execução de contrato |
| Pagamento | Token Stripe (não o nº de cartão), histórico de compras | Processamento de pagamentos, faturas | Contrato + obrigação legal |
| Atividade | Posts, likes, bookmarks, histórias, mensagens | Funcionamento da plataforma | Execução de contrato |
| Navegação | IP, browser, páginas visitadas, tempo de sessão | Segurança, diagnóstico, analytics | Interesse legítimo / Consentimento |
| Cookies | Ver Política de Cookies | Ver Política de Cookies | Consentimento |

## 3. Partilha de dados com terceiros

A MANGARROSA **não vende dados pessoais**. Subcontratantes:

| Serviço | Finalidade | País | Garantias |
|---|---|---|---|
| Supabase | BD, autenticação, armazenamento | UE (AWS Frankfurt) | Cláusulas contratuais tipo |
| Stripe | Processamento de pagamentos | UE/EUA | SCCs |
| Resend | Emails transacionais | EUA | SCCs |
| InvoiceXpress | Faturas fiscais | Portugal | RGPD |
| Google Analytics (se activo) | Analytics | EUA | SCCs + anonimização de IP |
| Cloudflare | CDN, DDoS, OG tags | EUA/UE | SCCs |

## 4. Direitos dos titulares

Ao abrigo do RGPD: **acesso**, **rectificação**, **apagamento** (direito ao esquecimento), **portabilidade** (JSON/CSV), **oposição** (marketing/analytics), **limitação**, e **reclamação à CNPD**. Para exercer: **privacy@[domínio]** — resposta em até 30 dias.

## 5. Retenção de dados

| Tipo | Período |
|---|---|
| Conta (activa) | Enquanto a conta existir |
| Conta (eliminada) | 30 dias após eliminação (backups) |
| Histórias | 24 horas (expiração automática) |
| Pagamento / faturas | 10 anos (obrigação fiscal) |
| Logs de acesso / segurança | 90 dias |
| Analytics | 26 meses (Google Analytics) |

## 6. Segurança

Medidas técnicas e organizacionais: encriptação em trânsito (HTTPS/TLS), controlo de acesso por funções (RLS Supabase), autenticação JWT, passwords com bcrypt. Violações de risco: CNPD notificada em 72 horas.

## 7. Menores

A Plataforma não se destina a menores de 18 anos. Não recolhemos intencionalmente dados de menores; se detectado, os dados são eliminados imediatamente.

## 8. Alterações à política

Alterações substanciais comunicadas por email com 30 dias de antecedência.

## 9. Contacto e DPO

- **Email:** privacy@[domínio]
- **Morada:** [Endereço da entidade legal]
- **CNPD:** [www.cnpd.pt](http://www.cnpd.pt)
