---
projecto: MANGARROSA
tipo: índice-cluster
migrado: 2026-07-03
tags: [systems, overview]
---

# Sistemas

Índice dos sistemas funcionais do MANGARROSA.

| Sistema | Estado | Doc |
|---|---|---|
| **Mensagens** | ⬜ por implementar (Realtime) | [[30_SYSTEMS/Mensagens]] |
| **Notificações** | ✅ in-app (cron pendente) | [[30_SYSTEMS/Notificacoes]] |
| **Briefs (Chamadas)** | ✅ decisões tomadas | [[30_SYSTEMS/Briefs_Tenho_Interesse]] |
| **Stories (Histórias)** | ⬜ especificado, por instalar | [[30_SYSTEMS/Stories]] |
| **Explore (Descobrir)** | ✅ implementado | [[30_SYSTEMS/Explore_Search]] |
| **Favoritos (Colher)** | ⬜ por implementar | [[30_SYSTEMS/Favorites]] |
| **Eliminação de conta** | ⬜ por implementar | [[30_SYSTEMS/Account_Deletion]] |

## Notas transversais
- **Notificações** são in-app; emails vivem em [[70_PIPELINE/Fase_K_Emails]].
- **Mensagens** têm guard PRO (Free só responde).
- **Stories** expiram por query (`expires_at > now()`), sem cron.
- **Favoritos** e **Eliminação de conta** têm implicações de privacidade/RGPD → [[90_LEGAL/Politica_Privacidade_RGPD]].
- Nomenclatura MANGARROSA a alinhar na Fase J: Descobrir, Chamadas, Colher, Cultivar.
