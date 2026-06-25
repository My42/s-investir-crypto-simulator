# Identité visuelle — `simulateurs.sinvestir.fr`

> Document de référence pour initialiser les styles & composants d'un projet
> **Next.js (App Router)** fidèle au design cible du test technique S'investir.
>
> **Source des données** : extraction directe du CSS/JS compilé du site
> (`/_nuxt/entry.*.css` + bundle JS). Le site cible est une application
> **Nuxt 3 + Nuxt UI v3 + Tailwind CSS v4**, en **thème sombre**, police **Lexend**.
> Les valeurs ci-dessous sont donc factuelles (issues du build), pas estimées.

---

## 1. Stack & esprit visuel

| Aspect | Constat |
|--------|---------|
| Framework cible | Nuxt 3 (Vue) + **Nuxt UI v3** (design system maison de Nuxt) |
| CSS | **Tailwind CSS v4** (tokens en `oklch`, `@theme`, variables `--ui-*`) |
| Thème | **Sombre** par défaut (dark fintech), fond **navy profond** |
| Police | **Lexend** (sans-serif géométrique, lisible, moderne) |
| Radius | Discret — `--ui-radius: 0.25rem` (coins légèrement arrondis, pas de "pill" partout) |
| Conteneur | `max-width: 80rem` (1280px) centré |

**Esprit / mood** : application financière **sérieuse, premium et lisible**.
Fond bleu nuit, larges respirations, accents **bleu vif** (action) et **or/jaune**
(valeur, mise en avant). Vert pour le positif (gains), rouge pour le négatif (pertes).
Typographie nette, hiérarchie marquée, composants épurés type "dashboard SaaS".

---

## 2. Palette de couleurs (valeurs exactes)

### 2.1 Couleurs de marque

| Rôle | Hex | Usage |
|------|-----|-------|
| **Primary** (bleu) | `#1098F7` | Boutons d'action, liens, focus ring, valeurs actives, accents |
| **Secondary** (or/jaune) | `#F8D047` | Mises en avant, badges premium, secondaire CTA, highlights |

> Ces deux couleurs sont injectées en dur partout dans le build
> (`--ui-primary` → `#1098f7`, `--ui-secondary` → `#f8d047`).

### 2.2 Couleurs sémantiques (états)

| Rôle | Hex principal | Variantes vues |
|------|---------------|----------------|
| **Success** (vert / gains) | `#11D05A` | `green-500` ≈ `#00C853` |
| **Error** (rouge / pertes) | `#FF0500` | `#FB2C36` |
| **Warning** (jaune) | `#F8D047` | `yellow-500 #FACC15`, `#E8BA05` |
| **Info** (bleu) | `#1098F7` | `#0049C6`, `#7899CE` |

### 2.3 Surfaces & texte (thème sombre)

Le simulateur définit ses propres tokens de surface (fond navy dégradé) :

| Token | RGB | Hex | Usage |
|-------|-----|-----|-------|
| `--color-surface` | `8 12 22` | `#080C16` | Fond global (le plus sombre) |
| `--color-surface-soft` | `15 23 42` | `#0F172A` | Cartes / panneaux (= slate-900) |
| `--color-surface-elevated` | `0 23 63` | `#00173F` | Éléments surélevés / hover navy |
| `--color-text` | `255 255 255` | `#FFFFFF` | Texte principal |
| `--color-text-muted` | `156 163 175` | `#9CA3AF` | Texte secondaire (= gray-400) |
| `--color-ring` | `16 152 247` | `#1098F7` | Anneau de focus |

### 2.4 Échelle neutre (Nuxt UI `neutral` = **slate**)

En thème sombre, Nuxt UI mappe les surfaces sur l'échelle **slate** :

| Token sémantique (dark) | Réfère à | Approx hex |
|-------------------------|----------|------------|
| `--ui-bg` | slate-900 | `#0F172A` |
| `--ui-bg-muted` | slate-800 | `#1E293B` |
| `--ui-bg-elevated` | slate-800 | `#1E293B` |
| `--ui-bg-accented` | slate-700 | `#334155` |
| `--ui-border` | slate-800 | `#1E293B` |
| `--ui-border-accented` | slate-700 | `#334155` |
| `--ui-text` | slate-200 | `#E2E8F0` |
| `--ui-text-muted` | slate-400 | `#94A3B8` |
| `--ui-text-dimmed` | slate-500 | `#64748B` |
| `--ui-text-highlighted` | white | `#FFFFFF` |

> ⚠️ Deux systèmes coexistent : les **surfaces custom navy** (`--color-surface*`,
> très bleutées) pour le simulateur, et les **neutres slate** de Nuxt UI pour les
> composants génériques. Pour la fidélité, privilégie le **navy** (`#080C16` /
> `#0F172A` / `#00173F`) sur les cartes du simulateur.

---

## 3. Typographie

- **Famille** : `Lexend` (Google Fonts), fallback system-ui.
- **Stack complète utilisée** :
  ```
  Lexend, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont,
  "Segoe UI", Roboto, "Helvetica Neue", Arial, "Noto Sans", sans-serif,
  "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji"
  ```
- **Mono** (chiffres/code éventuels) : `ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace`

**Échelle indicative (Tailwind par défaut, conservée par Nuxt UI)** :

| Usage | Classe | Taille / line-height |
|-------|--------|----------------------|
| Titre hero | `text-4xl`–`text-5xl` font-bold | 36–48px |
| Titre section | `text-2xl`–`text-3xl` font-semibold | 24–30px |
| Sous-titre / card title | `text-lg` font-medium | 18px |
| Corps | `text-base` | 16px / 1.5 |
| Secondaire / labels | `text-sm` text-muted | 14px |
| Légendes | `text-xs` | 12px |
| Chiffres clés (résultats) | `text-3xl`/`text-4xl` font-bold tabular-nums | gros, gras |

**Poids Lexend à charger** : 300, 400, 500, 600, 700.
Pour les montants/€ : utiliser `tabular-nums` (alignement des chiffres).

---

## 4. Tokens d'espacement, rayon, ombres

| Token | Valeur |
|-------|--------|
| Base spacing | `0.25rem` (échelle Tailwind 4px) |
| Radius par défaut | `--ui-radius: 0.25rem` (4px) ; cartes souvent `rounded-lg`/`rounded-xl` (8–12px) |
| Conteneur max | `--ui-container: 80rem` (1280px) |
| Hauteur header | `4rem` (64px) |
| Focus ring | `2px` couleur `#1098F7` (`ring-primary`), souvent `ring-offset` sur fond sombre |
| Ombres | Tailwind `shadow-sm`/`md`/`lg` ; sur fond sombre, profondeur surtout via surfaces élevées + bordures `slate-800` |

---

## 5. Composants UI (catalogue Nuxt UI → équivalents React)

Le site s'appuie sur la bibliothèque **Nuxt UI v3**. Voici les composants
repérés et leur traduction recommandée côté React/Next.js.

| Composant cible | Description visuelle | Équivalent React conseillé |
|-----------------|----------------------|----------------------------|
| **Button** | Plein `#1098F7` texte blanc (primary), variantes `outline`/`ghost`/`soft`, radius léger, `hover:brightness-110` | `<button>` stylé + variants (CVA) ou shadcn/ui `Button` |
| **Input / NumberField** | Fond surface sombre, bordure slate-700, focus ring bleu, label au-dessus | Headless UI / Radix `Input` + Tailwind |
| **Slider / Range** | Piste slate, remplissage bleu `#1098F7`, poignée ronde | Radix `Slider` |
| **Select / Dropdown** | Menu sombre élévé, item `hover:bg-elevated`, highlight bleu | Radix `Select` / `DropdownMenu` |
| **Card** | Fond navy `#0F172A`, bordure slate-800, radius `lg`/`xl`, padding généreux | `<div>` + classes utilitaires |
| **Tabs** | Onglet actif texte `#1098F7` + indicateur, inactif text-muted | Radix `Tabs` |
| **Badge / Chip** | Petit, soft (`bg-primary/10 text-primary`), variantes success/warning | composant `Badge` |
| **Tooltip** | Fond inversé, texte court | Radix `Tooltip` |
| **Toggle / Switch** | Piste slate → bleu quand actif, translation poignée | Radix `Switch` |
| **Table** | Lignes séparées par bordures slate-800, en-têtes text-muted | `<table>` + TanStack Table |
| **Chart** | Courbes de projection ; vert (gains) / rouge (pertes) / bleu (référence) sur grille discrète | **Recharts** ou Chart.js (thème sombre) |

**Patterns visuels clés à reproduire** :
- Cartes navy sur fond plus sombre, séparées par des bordures fines.
- Accent **bleu** réservé aux actions/valeurs actives ; **or** pour la mise en valeur.
- Vert/rouge **uniquement** pour le sens financier (gain/perte), jamais décoratif.
- Focus visible bleu (`ring-2 ring-[#1098F7]`) pour l'accessibilité.
- Chiffres importants en gros, gras, `tabular-nums`.

---

## 6. Stratégie d'implémentation — shadcn vs tout à la main

> Décision dictée par la **contrainte n°3 du brief** : *« composant autonome et
> intégrable — peu de dépendances, embarquable proprement »*. C'est ce critère
> qui tranche, pas le confort de développement.

### Reco : **shadcn en mode chirurgical** (mix ciblé)

Ni « tout shadcn », ni « tout à la main » :

| Besoin | Approche | Pourquoi |
|--------|----------|----------|
| Slider, Select, Switch, Tabs, NumberField, Tooltip | **shadcn** (Radix) | Accessibilité (clavier, ARIA, focus) longue et risquée à écrire à la main. Le site cible (**Nuxt UI**) tourne **déjà sur Radix** → parité de comportement gratuite. |
| Button, Card, Badge, layout, affichage des résultats | **à la main** | Purement présentationnel, ~10 lignes de Tailwind chacun. Tirer un composant n'apporte rien. |
| Graphique | **Recharts** | Indépendant de ce choix. |

### Pourquoi shadcn respecte « peu de dépendances »

shadcn n'est **pas une dépendance runtime** : il **copie le code des composants
dans le repo** (`components/ui/`). On n'embarque que `@radix-ui/*` (primitives
légères) + Tailwind.

- ✅ Code vendored = contrôlé, taillable, thémé avec les tokens de ce doc
- ✅ Pas de gros design system en prod (contrairement à MUI / Chakra)
- ✅ On installe **uniquement** les 4-5 primitives utiles au simulateur

### Le vrai piège : l'embeddabilité (bonus #6)

Le modèle shadcn (Tailwind global + variables sur `:root`) **peut entrer en
conflit avec la page hôte** :

- **Iframe** → isolation totale, aucun souci. **Option retenue pour la démo.**
- **Web component** → nécessite de scoper le CSS (shadow DOM + Tailwind `@scope`
  ou préfixe). Dans ce cas, des primitives **maison en CSS scopé** seraient plus
  propres que shadcn.

### Décision

- **MVP / démo Vercel (livrable obligatoire)** → **shadcn ciblé + iframe pour l'embed**.
- **Si on pousse le bonus web-component scopé** → basculer les primitives critiques
  en maison avec CSS scopé, garder Recharts.

---

## 7. Mise en œuvre — Next.js (App Router) + Tailwind v4

> **Choix de framework — Next.js.** Non pas pour Vercel (qui héberge aussi bien
> Vite/TanStack), mais pour la **compatibilité avec la stack interne S'investir**
> (Next.js, explicitement notée dans le critère *« intégrabilité du code »*) :
> le composant tombe directement dans leur codebase, sans justification à fournir.
> La logique reste **framework-agnostique** (TS pur dans `lib/`, composant React
> autonome) pour rester portable — le wrapper Next n'est qu'une page de montage.
>
> Le site cible utilise **Tailwind v4**. On reproduit ses tokens via `@theme`
> pour rester iso-design. Compatible Next.js App Router (déploiement Vercel natif).

### 7.1 `app.css` (ou `styles/globals.css`)

```css
@import "tailwindcss";

/* === Police Lexend === */
@import url("https://fonts.googleapis.com/css2?family=Lexend:wght@300;400;500;600;700&display=swap");

@theme {
  /* Typo */
  --font-sans: "Lexend", ui-sans-serif, system-ui, -apple-system,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, "Noto Sans", sans-serif;

  /* Couleurs de marque */
  --color-primary: #1098f7;     /* bleu action */
  --color-secondary: #f8d047;   /* or / highlight */

  /* États (sens financier) */
  --color-success: #11d05a;     /* gains */
  --color-error: #ff0500;       /* pertes */
  --color-warning: #f8d047;
  --color-info: #1098f7;

  /* Surfaces (navy fintech) */
  --color-surface: #080c16;          /* fond global */
  --color-surface-soft: #0f172a;     /* cartes */
  --color-surface-elevated: #00173f; /* éléments surélevés */

  /* Texte */
  --color-text: #ffffff;
  --color-text-muted: #9ca3af;

  /* Bordures (slate) */
  --color-border: #1e293b;        /* slate-800 */
  --color-border-accent: #334155; /* slate-700 */

  /* Rayon */
  --radius-ui: 0.25rem;

  /* Conteneur */
  --container-app: 80rem;
}

:root {
  color-scheme: dark;
}

body {
  background-color: var(--color-surface);
  color: var(--color-text);
  font-family: var(--font-sans);
  -webkit-font-smoothing: antialiased;
}

/* Chiffres alignés pour montants */
.tabular {
  font-variant-numeric: tabular-nums;
}
```

### 7.2 Échelle `primary` complète (si besoin de variantes 50→950)

Le `#1098F7` correspond à la teinte ~500. Ramp cohérent (à ajuster finement) :

```css
@theme {
  --color-primary-50:  #e7f4fe;
  --color-primary-100: #c4e4fd;
  --color-primary-200: #8ecbfb;
  --color-primary-300: #57b1f9;
  --color-primary-400: #2ba5f8;
  --color-primary-500: #1098f7; /* marque */
  --color-primary-600: #0b7ace;
  --color-primary-700: #0961a4;
  --color-primary-800: #0a4f85;
  --color-primary-900: #0d426d;
  --color-primary-950: #082a47;
}
```

### 7.3 Exemple de composant (style fidèle)

```tsx
// Bouton primaire fidèle à simulateurs.sinvestir.fr
export function PrimaryButton(props: React.ComponentProps<"button">) {
  return (
    <button
      {...props}
      className="inline-flex items-center justify-center gap-2
                 rounded-md bg-primary px-4 py-2 text-sm font-medium
                 text-white transition hover:brightness-110
                 focus-visible:outline-none focus-visible:ring-2
                 focus-visible:ring-primary focus-visible:ring-offset-2
                 focus-visible:ring-offset-surface
                 disabled:cursor-not-allowed disabled:opacity-60"
    />
  );
}

// Carte navy
export function Card({ children }: { children: React.ReactNode }) {
  return (
    <div className="rounded-xl border border-border bg-surface-soft p-6">
      {children}
    </div>
  );
}
```

### 7.4 Thème graphique (Recharts)

```ts
export const chartTheme = {
  grid: "#1e293b",      // slate-800
  axis: "#9ca3af",      // text-muted
  positive: "#11d05a",  // gains
  negative: "#ff0500",  // pertes
  reference: "#1098f7", // capital investi
  highlight: "#f8d047", // mise en avant
  tooltipBg: "#0f172a",
  tooltipBorder: "#334155",
};
```

---

## 8. Checklist de fidélité visuelle

- [ ] Police **Lexend** chargée (300–700) et appliquée globalement.
- [ ] Fond global **navy `#080C16`**, cartes **`#0F172A`**.
- [ ] Primary **`#1098F7`** sur tous les CTA / valeurs actives / focus ring.
- [ ] Secondary **`#F8D047`** pour les mises en avant uniquement.
- [ ] Vert **`#11D05A`** = gains, Rouge **`#FF0500`** = pertes (sens uniquement).
- [ ] Texte principal blanc, secondaire **`#9CA3AF`**.
- [ ] Bordures fines **slate-800 `#1E293B`** entre les surfaces.
- [ ] Radius discret (`rounded-md`/`lg`/`xl`, base 4px).
- [ ] Conteneur centré **max 1280px**.
- [ ] Chiffres en `tabular-nums`, gras pour les résultats clés.
- [ ] Focus visible bleu (accessibilité).
- [ ] Responsive desktop + mobile (cf. livrable obligatoire du brief).

---

### Annexe — provenance des valeurs

| Donnée | Source |
|--------|--------|
| Police Lexend | `font-family:Lexend,...` dans `entry.*.css` |
| `#1098F7` / `#F8D047` | hex les plus fréquents + `--tw-ring-color`, `--color-ring:16 152 247` |
| Surfaces navy | `--color-surface*` (RGB) dans `entry.*.css` |
| `neutral: slate`, `primary`, etc. | objet de config Nuxt UI dans le bundle JS |
| `--ui-radius: .25rem`, `--ui-container: 80rem` | variables `--ui-*` du build |
