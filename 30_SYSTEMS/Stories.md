---
projecto: MANGARROSA
tipo: sistema
sistema: stories
estado: especificado-por-instalar
data-origem: 2026-04-07
migrado: 2026-07-03
fonte: Notion — "STORIES — Implementação"
tags: [systems, stories, historias]
---

# Stories (Histórias)

> Conteúdo efémero, visível 24h. Nomenclatura MANGARROSA: *Histórias*.

## Tabelas (Supabase)

`stories_migration.sql` antes de testar. RLS em ambas.

**`stories`:** `id` PK · `user_id`→users · `media_url` · `media_type` (`image`|`video`) · `caption` (opcional) · `created_at` · `expires_at` (`now()+24h`).
**`story_views`:** `story_id`+`viewer_id` (PK composta) · `viewed_at`.

## Ficheiros

Criar: `stories_migration.sql`, `useStories.ts` (fetch activas, mark seen, ordenação), `StoriesBar.tsx` (strip no topo do feed), `StoryViewer.tsx` (viewer fullscreen), `CreateStory.tsx`.
Modificar: `FloatingNav.tsx` (menu + por role), `FeedAuth.tsx` / `Feed.tsx` (integrar bar+viewer), `App.tsx` (rota `/stories/create`).

## UX — StoriesBar
Strip horizontal acima do SegmentedControl. Avatares 62px com ring (verde=unseen, cinzento=seen). Ordem: próprio → unseen → seen. Só aparece com stories activas. Criativos: botão "A tua história" sempre visível. Clientes/visitantes: sem botão de criação.

## UX — StoryViewer
Fullscreen `z-[150]`, 9:16 centrado max-width 430px. Barras de progresso no topo (uma por story). Auto-advance 5s/imagem; vídeos no `onEnded`. Pausa: pressionar e manter. Tap esquerda (1/3) anterior, direita (2/3) próxima. Setas laterais entre users (desktop). Gradientes top/bottom. Fechar: X ou Escape. Views registadas em tempo real.

## UX — CreateStory
Drop zone (JPG/PNG/GIF/MP4, máx 50MB). Preview 9:16. Caption opcional (máx 150 car.). Após publicar → `/feed`.

## FloatingNav — botão + contextual
Criativo/Agência: Publicar trabalho (`/post/create`), Criar história (`/stories/create`). Cliente/Recrutador: Publicar brief (`/briefs/create`), Publicar vaga (`/jobs/create`). Visitante: modal OV1.

## Notas técnicas
- Stories no bucket `posts` (`stories/{user_id}/{timestamp}.ext`) — sem bucket separado.
- `useStories` busca só `expires_at > now()` — **expiração automática via query, sem cron**.
- `story_views` usa upsert silencioso (sem duplicados).
- StoryViewer usa RAF nativo (sem libs externas).

## Checklist
⬜ SQL · ⬜ useStories · ⬜ StoriesBar · ⬜ StoryViewer · ⬜ CreateStory · ⬜ FloatingNav · ⬜ FeedAuth · ⬜ Feed · ⬜ App.tsx
