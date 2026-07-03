---
projecto: MANGARROSA
tipo: brand
estado: plano-de-implementação
data-origem: 2026-04-10
migrado: 2026-07-03
fonte: Notion — "IDENTIDADE VISUAL — MANGARROSA Brand System"
tags: [brand, identidade, design-system, tokens, cor, tipografia]
---

# Identidade Visual — MANGARROSA Brand System

> Sistema de identidade: tokens de cor, tipografia, linguagem gráfica e princípios de interação, com mapeamento ficheiro a ficheiro. **Base directa para a Fase N** (tokenização W3C DTCG → Figma → Tailwind) — ver [[70_PIPELINE/00_Roadmap_Retoma]].

## 1. Sistema de cor

Tokens em `tailwind.config.ts`:

```typescript
colors: {
  mango:    '#F6B73C',  // amarelo solar — fonte de luz
  rose:     '#D6456B',  // rosa profundo — emoção
  coral:    '#F08A7E',  // coral suave — emoção secundária
  sage:     '#7A9D8E',  // verde musgo — equilíbrio
  offwhite: '#F6F3EE',  // branco quente — texto/elementos pontuais (NÃO background)
  primary:  { DEFAULT: '#F6B73C', foreground: '#1A1000' }, // substitui o antigo #00C896
}
```

**Regra: nunca flat fills.** O amarelo nunca aparece como bloco sólido — sempre com gradiente, grain ou variação de luz.

### Gradientes
```css
--gradient-hero:   linear-gradient(135deg, #F6B73C 0%, #F08A7E 50%, #D6456B 100%);
--gradient-warm:   linear-gradient(180deg, #F6B73C 0%, #F08A7E 100%);
--gradient-subtle: linear-gradient(135deg, rgba(246,183,60,0.15) 0%, rgba(214,69,107,0.10) 100%);
--gradient-card:   linear-gradient(180deg, transparent 60%, rgba(214,69,107,0.20) 100%);
```

Ficheiros críticos onde o `primary` antigo (#00C896) é usado: `index.css` (`:root`), `tailwind.config.ts`, `PostCard.tsx`, `FloatingNav.tsx`, `BriefDetail.tsx`/`JobDetail.tsx`, `OwnProfile.tsx`, `Button.tsx`.

## 2. Tipografia

**Plus Jakarta Sans** (expressiva, orgânica; pesos 300–800; Google Fonts, cobertura PT/BR).

```typescript
fontFamily: { sans: ['Plus Jakarta Sans', 'Inter', 'system-ui', 'sans-serif'] }
```

| Uso | Classe |
|---|---|
| Hero / oversized | `text-[72px] font-bold leading-[0.95]` |
| Heading principal | `text-[32px] font-bold` |
| Heading secção | `text-[20px] font-semibold` |
| Body | `text-[15px] font-normal leading-relaxed` |
| Caption / label | `text-[12px] font-medium tracking-wide` |

## 3. Linguagem gráfica

- **Grain/noise:** via SVG `feTurbulence` data-URI num pseudo-elemento `.grain::after` (opacity ~0.04, zero-cost). Aplicar em hero/cards de destaque, botão primário, backgrounds de `Feed`/`AboutPage`.
- **Blobs/liquid forms:** componente `BlobDecor.tsx` (SVG path com gradiente mango→rose, opacity 0.12) como decoração de background, não layout. Aplicar em `Feed`, `AboutPage`, `Login`/`SignUp`, modais de auth.
- **Light leaks:** `radial-gradient` mango (canto superior) e rose (canto inferior), baixa opacidade. Aplicar em hover de `PostCard`, headers de perfil, topo de `BriefDetail`.

## 4. Princípios de interação

- **Transitions:** fade + drift, nunca snap. `cubic-bezier(0.4,0,0.2,1)` ~280–300ms; `hover-drift` faz `translateY(-2px)`.
- **Hover:** soft glow no botão primário — `box-shadow: 0 0 20px rgba(246,183,60,0.35), 0 4px 16px rgba(214,69,107,0.20)`.
- **Microinteractions:** `@keyframes breathe` (2.5s, opacity+scale) para stories/PRO badges; `@keyframes flow` (gradientes animados, `background-size:200%`) no botão `+`.
- **Scroll:** hook `useScrollParallax(factor)` para blobs no hero (parallax leve).

## 5. Ficheiros

**Novos:** `BlobDecor.tsx`, `useScrollParallax.ts`, `styles/animations.css` (breathe/flow/drift).
**Modificar:** `tailwind.config.ts` (cores, fonte, animations), `index.css` (vars, grain, light leaks, transições), `index.html` (Google Fonts), `Button.tsx`, `PostCard.tsx`, `FloatingNav.tsx` (+ logo "MG"), `StoryAvatar.tsx`, `StoriesBar.tsx`, `CreativeCard.tsx`, `Feed.tsx`/`FeedAuth.tsx`, `Login`/`SignUp`, modais de auth, `AboutPage.tsx` (full treatment), `OwnProfile.tsx`, `Profile.tsx`, `ModalHighlight.tsx`.

## 6. Ordem de implementação

1. **Tokens** (base): `tailwind.config.ts` (cores+fonte) → `index.css` (vars+fonte) → `index.html` → verificar que nada quebra (primary verde→mango).
2. **Componentes core:** Button, PostCard, FloatingNav, StoryAvatar/StoriesBar.
3. **Páginas e decoração:** BlobDecor, Feed/FeedAuth, Login/SignUp, AboutPage.
4. **Microinteractions:** animations.css, breathe (stories/PRO), flow (botão +), useScrollParallax.

## 7. Decisões finais (excepções ao sistema de cor)

> - **Projeto Destacado (Manga Madura):** gradiente Deep Rose (#D6456B) → Soft Coral (#F08A7E) — **nunca mango**. Ícone Zap do badge também Deep Rose.
> - **Like (Heart):** Deep Rose (#D6456B) quando activo.
> - **Favorito (Bookmark/Colher):** Mango (#F6B73C) quando activo.
> - **Verde (#00C896):** mantém-se **apenas** em estados de sucesso ("Interesse registado", "Candidatura enviada").
> - **Dark mode nativo:** offwhite (#F6F3EE) é para texto/elementos pontuais, **não** background. Mango e coral são acentos, não fundos.
> - **Contraste:** mango sobre offwhite carece de verificação WCAG — usar rose ou texto escuro nesses contextos.
> - **Performance:** grain via SVG data-URI e blobs SVG inline são leves; evitar PNG/JPG para texturas.
