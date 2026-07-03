---
projecto: MANGARROSA
tipo: sistema
sistema: mensagens
estado: por-implementar
data-origem: 2026-03-27
migrado: 2026-07-03
fonte: Notion — "MESSAGES — Sistema de mensagens"
tags: [systems, mensagens, realtime]
---

# Sistema de Mensagens

> Página `/messages` existe mas com dados fictícios. Tabela `messages` existe no Supabase mas não ligada ao UI. Notificação tipo `message` já definida.

## Decisão MVP

Sistema completo antes do lançamento: inbox (lista de conversas), enviar/receber em tempo real (Supabase Realtime), notificação `message` ao receber, botão "Mensagem" no perfil abre/cria conversa.

> [!note] Guard PRO
> Mensagens são benefício PRO: **Free só responde**, não inicia conversas. Verificar guard no fluxo (ver QA I9 na pipeline).

## SQL

```sql
CREATE TABLE IF NOT EXISTS public.messages (
  id uuid DEFAULT gen_random_uuid() PRIMARY KEY,
  sender_id uuid REFERENCES public.users(id) ON DELETE CASCADE,
  receiver_id uuid REFERENCES public.users(id) ON DELETE CASCADE,
  content text NOT NULL,
  read boolean DEFAULT false,
  created_at timestamptz DEFAULT now()
);

ALTER TABLE messages ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Users can see their own messages" ON messages
  FOR SELECT USING (auth.uid() = sender_id OR auth.uid() = receiver_id);
CREATE POLICY "Users can send messages" ON messages
  FOR INSERT WITH CHECK (auth.uid() = sender_id);
```

## Estrutura `/messages`

- Sidebar esquerda: lista de utilizadores com quem já trocou mensagens
- Área principal: mensagens da conversa seleccionada
- Input na base para enviar
- **Mobile:** lista primeiro, conversa depois (com botão voltar)

## Ficheiros
- `src/pages/Messages.tsx` — redesenhar com dados reais
- `src/hooks/useMessages.ts` — novo hook com Supabase Realtime

## Status
⬜ SQL verificado · ⬜ `useMessages` hook · ⬜ `Messages.tsx` ligado ao Supabase · ⬜ guard PRO · ⬜ testado
