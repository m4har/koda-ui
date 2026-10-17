# koda-ui

Copy-based shadcn/ui kit carrying the industrial koda design language: sharp corners,
hairline borders, mono HUD micro-labels, one accent orange. There is no npm package —
you copy files from this repo into your app, like every shadcn kit.

**Surfaces:** landing, dashboard, auth. **Stack:** React 19, Tailwind v4, TypeScript, lucide-react.

## Install

### 1. Dependencies

```bash
npm install @radix-ui/react-slot class-variance-authority clsx tailwind-merge lucide-react tw-animate-css
npm install -D typescript @types/react @types/react-dom
```

### 2. Tokens

Copy `app/globals.css` into your app (or merge its token blocks into your existing file).
It contains the `:root` / `.dark` variables and the `@theme inline` bridge for Tailwind v4,
plus the `shimmer` and `spinner` keyframes — those must exist in the **consumer** app's
stylesheet or the animations silently do nothing.

### 3. Path alias

`tsconfig.json`:

```json
{ "compilerOptions": { "paths": { "@/*": ["./*"] } } }
```

`components.json` in this repo already maps `@/components`, `@/lib/utils`, `@/components/ui`.

### 4. Copy the folders

```bash
cp lib/utils.ts <your-app>/lib/utils.ts
cp -r components/ui <your-app>/components/ui
cp -r components/landing <your-app>/components/landing
cp -r components/dashboard <your-app>/components/dashboard
cp -r components/auth <your-app>/components/auth
```

No barrel files: import each component from its own path.

## Token table

| Token | Light | Dark | Role |
| --- | --- | --- | --- |
| `--background` | `#FFFFFF` | `#090909` | Page surface |
| `--foreground` | `#0A0A0A` | `#FAFAFA` | Body ink |
| `--card` | `#FFFFFF` | `#161616` | Panel surface |
| `--primary` | `#FE5F21` | `#FE5F21` | Accent orange |
| `--primary-foreground` | `#0A0A0A` | `#0A0A0A` | Text on accent |
| `--secondary` | `#F1F1F1` | `#161616` | Quiet fill |
| `--muted` | `#F5F5F5` | `#121212` | Skeleton / muted fill |
| `--muted-foreground` | `#666666` | `#AFAFAF` | Secondary text |
| `--border` | `#DDDDDD` | `#2A2A2A` | Hairlines |
| `--input` | `#CDCDCD` | `#323232` | Input borders |
| `--ring` | `#FE5F21` | `#FE5F21` | Focus ring |
| `--destructive` | `#F2433E` | `#F2433E` | Danger |
| `--success` | `#35D49C` | `#35D49C` | Positive status |
| `--warning` | `#FCBB40` | `#FCBB40` | Caution status |
| `--info` | `#1D64FF` | `#1D64FF` | Info status |
| `--radius` | `0rem` | `0rem` | Sharp corners — the identity |

Fonts: `--font-display` (Plus Jakarta Sans), `--font-body` (Inter), `--font-mono` (Geist Mono).
Load them in your app (Google Fonts / self-host); tokens only reference the families.

## House style

- Micro-labels: one `Label` primitive — mono, 10px, uppercase, `tracking-[0.1em]`. Never redefine.
- Hairline grids: `gap-px` on a `bg-border` parent with `bg-background` children.
- Interactive primitives carry press feedback (`active:translate-y-px active:scale-[0.98]`)
  with a `motion-reduce` guard, baked into `buttonVariants`.
- Every component takes `className` and spreads `...props`.
- Skeletons shimmer for known shapes; `Spinner` for indeterminate waits.

## Catalog

| Group | Components |
| --- | --- |
| `components/ui` | button, badge, card, input, textarea, label, select, table, skeleton, spinner, separator, section-frame |
| `components/landing` | navbar, hero, feature-grid, stat-counter, testimonial, cta-band, footer |
| `components/dashboard` | sidebar-shell, stat-card, chart-shell, activity-feed, data-table |
| `components/auth` | auth-card |

Props tables and usage examples: [`docs/`](docs/).

## Typecheck

```bash
npm install
npm run typecheck   # tsc --noEmit
```
