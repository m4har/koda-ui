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
| `--border` | `#DDDDDD` | `#323232` | Hairlines |
| `--input` | `#CDCDCD` | `#323232` | Input borders |
| `--ring` | `#FE5F21` | `#FE5F21` | Focus ring |
| `--koda-blue` | `#6BC7F2` | `#6BC7F2` | Announcement bar / secondary accent |
| `--alumni-pink` / `--alumni-yellow` / `--alumni-green` / `--alumni-blue` | `#F5A3C7` / `#F5D96B` / `#9BE39B` / `#8FC4F5` | same in dark | Alumni card tone accents (`alumni-carousel`) |
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
| `components/landing` | navbar, announcement-bar, rule-rail, hero, feature-grid, career-pillars, curriculum-accordion, alumni-carousel, next-dirimu-band, stat-counter, testimonial, cta-band, footer |
| `components/dashboard` | sidebar-shell, stat-card, chart-shell, activity-feed, data-table |
| `components/auth` | auth-card |

Props tables and usage examples: [`docs/`](docs/).

## Captures

Rendered from the consumer gallery route (`koda-example` → `/gallery`) at 1440px, dark theme.

| ![button](docs/captures/button.png) | ![badge](docs/captures/badge.png) | ![card](docs/captures/card.png) |
| --- | --- | --- |
| ![input](docs/captures/input.png) | ![textarea](docs/captures/textarea.png) | ![select](docs/captures/select.png) |
| --- | --- | --- |
| ![label](docs/captures/label.png) | ![separator](docs/captures/separator.png) | ![skeleton](docs/captures/skeleton.png) |
| --- | --- | --- |
| ![spinner](docs/captures/spinner.png) | ![table](docs/captures/table.png) | ![section-frame](docs/captures/section-frame.png) |
| --- | --- | --- |
| ![announcement-bar](docs/captures/announcement-bar.png) | ![rule-rail](docs/captures/rule-rail.png) | ![navbar](docs/captures/navbar.png) |
| --- | --- | --- |
| ![hero](docs/captures/hero.png) | ![stat-counter](docs/captures/stat-counter.png) | ![feature-grid](docs/captures/feature-grid.png) |
| --- | --- | --- |
| ![testimonial](docs/captures/testimonial.png) | ![accordion](docs/captures/accordion.png) | ![cta-band](docs/captures/cta-band.png) |
| --- | --- | --- |
| ![footer](docs/captures/footer.png) | ![sidebar-shell](docs/captures/sidebar-shell.png) | ![stat-card](docs/captures/stat-card.png) |
| --- | --- | --- |
| ![chart-shell](docs/captures/chart-shell.png) | ![activity-feed](docs/captures/activity-feed.png) | ![data-table](docs/captures/data-table.png) |
| --- | --- | --- |
| ![auth-card](docs/captures/auth-card.png) | ![modal](docs/captures/modal.png) | ![batches](docs/captures/batches.png) |
| --- | --- | --- |
| ![alumni-carousel](docs/captures/alumni-carousel.png) | ![next-dirimu-band](docs/captures/next-dirimu-band.png) | ![career-pillars](docs/captures/career-pillars.png) |
| --- | --- | --- |
| ![curriculum-accordion](docs/captures/curriculum-accordion.png) | | |
| --- | --- | --- |

Light theme (`ui/` primitives, 2x scale):

| ![button](docs/captures/light/button.png) | ![badge](docs/captures/light/badge.png) | ![card](docs/captures/light/card.png) |
| --- | --- | --- |
| ![input](docs/captures/light/input.png) | ![textarea](docs/captures/light/textarea.png) | ![select](docs/captures/light/select.png) |
| --- | --- | --- |
| ![label](docs/captures/light/label.png) | ![separator](docs/captures/light/separator.png) | ![skeleton](docs/captures/light/skeleton.png) |
| --- | --- | --- |
| ![spinner](docs/captures/light/spinner.png) | ![table](docs/captures/light/table.png) | ![section-frame](docs/captures/light/section-frame.png) |
| --- | --- | --- |

## Typecheck

```bash
npm install
npm run typecheck   # tsc --noEmit
```

## Registry (optional)

`registry.json` ships at the repo root, so once the repo is public on GitHub:

```bash
npx shadcn@latest add <user>/<repo>/button          # single item
npx shadcn@latest add <user>/<repo>/button <user>/<repo>/card   # several
npx shadcn@latest add <user>/<repo>/hero --dry-run # preview paths
```

Items: `utils` (lib), `globals` (tokens file), all `components/ui` names, plus
`navbar`, `announcement-bar`, `rule-rail`, `hero`, `feature-grid`, `career-pillars`, `curriculum-accordion`,
`alumni-carousel`, `next-dirimu-band`, `stat-counter`, `testimonial`, `cta-band`, `footer`,
`sidebar-shell`, `stat-card`, `chart-shell`, `activity-feed`, `data-table`, `auth-card`.
`registryDependencies` pull `utils` and cross-group primitives automatically.
Requires `components.json` + the `@/` alias in the consumer (see Install).

