---
projecto: MANGARROSA
tipo: setup
sistema: supabase
estado: schema-de-referência
data-origem: 2026-03-24
migrado: 2026-07-03
fonte: Notion — "SUPABASE INTEGRATION GUIDE"
tags: [setup, supabase, schema, sql, rls]
---

# Supabase — Guia de Integração (schema de referência)

> Liga o frontend (Lovable) ao Supabase: auth, BD, storage. Contém o **esquema completo da base de dados** com RLS. Referência canónica das tabelas.
> Nota: nomes de tabela/coluna em **inglês** (regra de nomenclatura). Copy `MATCHA` nos prompts → actualizar para MANGARROSA.

## Passo 1 — Tabelas

### 1.1 `users` (estende `auth.users`)
```sql
CREATE TABLE users (
  id uuid PRIMARY KEY REFERENCES auth.users(id) ON DELETE CASCADE,
  username text UNIQUE NOT NULL,
  name text NOT NULL,
  bio text,
  discipline text[] DEFAULT '{}',
  location text,
  website text,
  contact_email text,
  role text CHECK (role IN ('creative', 'client')) NOT NULL DEFAULT 'creative',
  avatar_url text,
  billing_name text,
  billing_nif text,
  billing_address text,
  deletion_requested_at timestamp,
  created_at timestamp DEFAULT now(),
  updated_at timestamp DEFAULT now()
);
ALTER TABLE users ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Public profiles are viewable by everyone" ON users FOR SELECT USING (true);
CREATE POLICY "Users can update their own profile" ON users FOR UPDATE USING (auth.uid() = id);
```

### 1.2 `posts`
```sql
CREATE TABLE posts (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id uuid REFERENCES users(id) ON DELETE CASCADE NOT NULL,
  title text NOT NULL,
  description text,
  discipline text[] DEFAULT '{}',
  tags text[] DEFAULT '{}',
  media_urls text[] DEFAULT '{}',
  is_highlighted boolean DEFAULT false,
  created_at timestamp DEFAULT now(),
  updated_at timestamp DEFAULT now()
);
ALTER TABLE posts ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Posts are viewable by everyone" ON posts FOR SELECT USING (true);
CREATE POLICY "Users can create their own posts" ON posts FOR INSERT WITH CHECK (auth.uid() = user_id);
CREATE POLICY "Users can update their own posts" ON posts FOR UPDATE USING (auth.uid() = user_id);
CREATE POLICY "Users can delete their own posts" ON posts FOR DELETE USING (auth.uid() = user_id);
```

### 1.3 `follows`
```sql
CREATE TABLE follows (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  follower_id uuid REFERENCES users(id) ON DELETE CASCADE NOT NULL,
  following_id uuid REFERENCES users(id) ON DELETE CASCADE NOT NULL,
  created_at timestamp DEFAULT now(),
  UNIQUE(follower_id, following_id)
);
ALTER TABLE follows ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Follows are viewable by everyone" ON follows FOR SELECT USING (true);
CREATE POLICY "Users can follow others" ON follows FOR INSERT WITH CHECK (auth.uid() = follower_id);
CREATE POLICY "Users can unfollow" ON follows FOR DELETE USING (auth.uid() = follower_id);
```

### 1.4 `likes`
```sql
CREATE TABLE likes (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id uuid REFERENCES users(id) ON DELETE CASCADE NOT NULL,
  post_id uuid REFERENCES posts(id) ON DELETE CASCADE NOT NULL,
  created_at timestamp DEFAULT now(),
  UNIQUE(user_id, post_id)
);
ALTER TABLE likes ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Likes are viewable by everyone" ON likes FOR SELECT USING (true);
CREATE POLICY "Users can like posts" ON likes FOR INSERT WITH CHECK (auth.uid() = user_id);
CREATE POLICY "Users can unlike posts" ON likes FOR DELETE USING (auth.uid() = user_id);
```

### 1.5 `saved_posts` (favoritos / Colher)
```sql
CREATE TABLE saved_posts (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id uuid REFERENCES users(id) ON DELETE CASCADE NOT NULL,
  post_id uuid REFERENCES posts(id) ON DELETE CASCADE NOT NULL,
  saved_at timestamp DEFAULT now(),
  UNIQUE(user_id, post_id)
);
ALTER TABLE saved_posts ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Users can view their own saved posts" ON saved_posts FOR SELECT USING (auth.uid() = user_id);
CREATE POLICY "Users can save posts" ON saved_posts FOR INSERT WITH CHECK (auth.uid() = user_id);
CREATE POLICY "Users can remove saved posts" ON saved_posts FOR DELETE USING (auth.uid() = user_id);
```

### 1.6 `briefs`
```sql
CREATE TABLE briefs (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  client_id uuid REFERENCES users(id) ON DELETE CASCADE NOT NULL,
  title text NOT NULL,
  description text,
  discipline text[] DEFAULT '{}',
  budget_min numeric,
  budget_max numeric,
  deadline date,
  location text,
  remote boolean DEFAULT false,
  status text CHECK (status IN ('open', 'closed')) DEFAULT 'open',
  created_at timestamp DEFAULT now(),
  updated_at timestamp DEFAULT now()
);
ALTER TABLE briefs ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Briefs are viewable by everyone" ON briefs FOR SELECT USING (true);
CREATE POLICY "Clients can create briefs" ON briefs FOR INSERT WITH CHECK (auth.uid() = client_id);
CREATE POLICY "Clients can update their own briefs" ON briefs FOR UPDATE USING (auth.uid() = client_id);
```

### 1.7 `brief_interests`
```sql
CREATE TABLE brief_interests (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id uuid REFERENCES users(id) ON DELETE CASCADE NOT NULL,
  brief_id uuid REFERENCES briefs(id) ON DELETE CASCADE NOT NULL,
  created_at timestamp DEFAULT now(),
  UNIQUE(user_id, brief_id)
);
ALTER TABLE brief_interests ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Brief interests viewable by brief owner and interested user"
  ON brief_interests FOR SELECT
  USING (auth.uid() = user_id OR auth.uid() IN (SELECT client_id FROM briefs WHERE id = brief_id));
CREATE POLICY "Users can express interest" ON brief_interests FOR INSERT WITH CHECK (auth.uid() = user_id);
CREATE POLICY "Users can withdraw interest" ON brief_interests FOR DELETE USING (auth.uid() = user_id);
```

### 1.8 `messages`
```sql
CREATE TABLE messages (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  sender_id uuid REFERENCES users(id) ON DELETE CASCADE NOT NULL,
  recipient_id uuid REFERENCES users(id) ON DELETE CASCADE NOT NULL,
  brief_id uuid REFERENCES briefs(id) ON DELETE SET NULL,
  content text NOT NULL,
  read boolean DEFAULT false,
  created_at timestamp DEFAULT now()
);
ALTER TABLE messages ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Users can view their own messages" ON messages FOR SELECT
  USING (auth.uid() = sender_id OR auth.uid() = recipient_id);
CREATE POLICY "Users can send messages" ON messages FOR INSERT WITH CHECK (auth.uid() = sender_id);
```

### 1.9 `notifications`
```sql
CREATE TABLE notifications (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id uuid REFERENCES users(id) ON DELETE CASCADE NOT NULL,
  type text CHECK (type IN ('follow', 'like', 'highlight_expiring', 'brief', 'brief_interest', 'message')) NOT NULL,
  actor_id uuid REFERENCES users(id) ON DELETE CASCADE,
  post_id uuid REFERENCES posts(id) ON DELETE CASCADE,
  brief_id uuid REFERENCES briefs(id) ON DELETE CASCADE,
  message_id uuid REFERENCES messages(id) ON DELETE CASCADE,
  read boolean DEFAULT false,
  created_at timestamp DEFAULT now()
);
ALTER TABLE notifications ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Users can view their own notifications" ON notifications FOR SELECT USING (auth.uid() = user_id);
CREATE POLICY "Users can mark notifications as read" ON notifications FOR UPDATE USING (auth.uid() = user_id);
```
> Nota: o `type` foi depois expandido (ver [[30_SYSTEMS/Notificacoes]] — job_*, brief_closed/reopened, new_story, etc.) e a coluna `job_id` adicionada via `notifications_job_migration.sql`.

### 1.10 `highlights`
```sql
CREATE TABLE highlights (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id uuid REFERENCES users(id) ON DELETE CASCADE NOT NULL,
  post_id uuid REFERENCES posts(id) ON DELETE CASCADE NOT NULL,
  stripe_payment_id text,
  duration_days integer NOT NULL,
  starts_at timestamp DEFAULT now(),
  expires_at timestamp NOT NULL,
  active boolean DEFAULT true,
  created_at timestamp DEFAULT now()
);
ALTER TABLE highlights ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Users can view their own highlights" ON highlights FOR SELECT USING (auth.uid() = user_id);
```

## Passo 2 — Auto-criar perfil no signup

```sql
CREATE OR REPLACE FUNCTION public.handle_new_user()
RETURNS trigger AS $$
BEGIN
  INSERT INTO public.users (id, name, username, role)
  VALUES (
    new.id,
    COALESCE(new.raw_user_meta_data->>'full_name', 'Utilizador'),
    COALESCE(new.raw_user_meta_data->>'username', 'user_' || substr(new.id::text, 1, 8)),
    COALESCE(new.raw_user_meta_data->>'role', 'creative')
  );
  RETURN new;
END;
$$ LANGUAGE plpgsql SECURITY DEFINER;

CREATE TRIGGER on_auth_user_created
  AFTER INSERT ON auth.users
  FOR EACH ROW EXECUTE FUNCTION public.handle_new_user();
```

## Passo 3 — Storage buckets

| Bucket | Público | Uso |
|---|---|---|
| `avatars` | Sim | Fotos de perfil |
| `posts` | Sim | Imagens/vídeos de posts (e stories em `stories/{user_id}/…`) |

Política: permitir upload a utilizadores autenticados.

## Passo 4 — Ligar Lovable ao Supabase

```typescript
// src/lib/supabase.ts
import { createClient } from '@supabase/supabase-js'
export const supabase = createClient(
  import.meta.env.VITE_SUPABASE_URL,
  import.meta.env.VITE_SUPABASE_ANON_KEY
)
```

## Passo 5 — Seed data
Correr o script de seed após criar tabelas (ver doc *SUPABASE — Seed Data Plan*, por migrar se necessário).

## Passo 6 — Auth no frontend ✅
`useAuth.ts` (`{ user, session, isAuthenticated, isLoading, signOut }`), login/registo com Supabase, Google OAuth (`signInWithOAuth({ provider: 'google' })`), `isAuthenticated` dinâmico em todas as páginas, sign out no FloatingNav.

## Status
- [ ] Passo 1: criar tabelas · [ ] Passo 2: trigger · [ ] Passo 3: buckets · [ ] Passo 4: verificar ligação Lovable · [ ] Passo 5: seed · [x] Passo 6: auth no frontend ✅
