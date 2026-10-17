# Landing (`components/landing`)

Public marketing chrome. Pair with `ui/section-frame` for section structure.

## Navbar

Sticky top chrome matching the dashboard shell header.

| Name | Type | Note |
| --- | --- | --- |
| `brand` | `string` | Mono wordmark |
| `items` | `{ label: string; href: string }[]` | Nav links; hidden below `md` |
| `cta` | `{ label: string; href: string }` | Renders a `Button asChild` — dark `#222222` fill |
| `...props` | `HTMLAttributes<HTMLElement>` | Spread; `sticky top-5 z-40 h-10` preset (sticks under `AnnouncementBar`) |

```tsx
<AnnouncementBar>Registration closes 30 Sep 2026 — 10 seats left</AnnouncementBar>
<Navbar
  brand="Koda"
  items={[{ label: "Curriculum", href: "#curriculum" }, { label: "Alumni", href: "#alumni" }]}
  cta={{ label: "Apply now", href: "/apply" }}
/>
```

## AnnouncementBar

Sticky 20px strip above the navbar — koda blue, black uppercase 12px.

| Name | Type | Note |
| --- | --- | --- |
| `children` | `ReactNode` | Message; styled uppercase 12px |
| `href` | `string` | Optional — wraps the message in a link |
| `...props` | `HTMLAttributes<HTMLElement>` | Spread; `sticky top-0 z-50 h-5 bg-koda-blue` preset |

```tsx
<AnnouncementBar href="/apply">
  Registration closes 30 Sep 2026 — 10 seats left
</AnnouncementBar>
```

## RuleRail

Left line-number rail: 28px column of 20px cells numbered 1..`rows`, full document
height. Place inside a `relative` page wrapper — it scrolls with content (never fixed).
Offset page content with `pl-7` (28px) on the same wrapper so text never sits under
the rail at any viewport; the rail is absolute and always visible.

| Name | Type | Note |
| --- | --- | --- |
| `rows` | `number` | Cells = documentHeight / 20; default `333` |
| `...props` | `HTMLAttributes<HTMLDivElement>` | Spread; `absolute left-0 top-0 w-7` preset, `aria-hidden` |

```tsx
<div className="relative pl-7">
  <RuleRail rows={333} />
  {/* page content */}
</div>
```

## Hero

Full-bleed opening section.

| Name | Type | Note |
| --- | --- | --- |
| `eyebrow` | `string` | Mono `Label` above the heading |
| `heading` | `ReactNode` | `h1`, display font |
| `description` | `ReactNode` | Supporting line |
| `actions` | `ReactNode` | Button row (`flex-wrap`) |
| `meta` | `ReactNode` | Small print row under actions |
| `...props` | `HTMLAttributes<HTMLElement>` | Spread |

```tsx
<Hero
  eyebrow="Batch 11 — Golang"
  heading={<>Ship production code in 14 weeks</>}
  description="Intensive classes, real projects, personal mentoring."
  actions={<><Button>Apply now</Button><Button variant="outline">View curriculum</Button></>}
/>
```

## FeatureGrid

Hairline card grid; index labels auto-number when `index` is omitted.

| Name | Type | Note |
| --- | --- | --- |
| `features` | `{ index?, title, description, icon? }[]` | Grid cells |
| `...props` | `HTMLAttributes<HTMLElement>` | Spread; `gap-px bg-border` preset |

```tsx
<FeatureGrid
  features={[
    { title: "1-on-1 mentoring", description: "CV, portfolio, interview prep.", icon: <Users /> },
    { index: "07", title: "Job readiness", description: "Real projects, industry briefs." },
  ]}
/>
```

## StatCounter

Numeric proof strip.

| Name | Type | Note |
| --- | --- | --- |
| `stats` | `{ value: string; label: string }[]` | Up to 4 per row |
| `...props` | `HTMLAttributes<HTMLElement>` | Spread |

```tsx
<StatCounter stats={[{ value: "100+", label: "Alumni hired" }, { value: "95%", label: "Hired in 6 months" }]} />
```

## Testimonial

Quote cards with initials squares — no photos needed.

| Name | Type | Note |
| --- | --- | --- |
| `items` | `{ quote, name, role }[]` | Up to 3 per row |
| `...props` | `HTMLAttributes<HTMLElement>` | Spread |

```tsx
<Testimonial
  items={[{ quote: "Landed a backend role 3 weeks after graduation.", name: "Rani Putri", role: "Backend Engineer" }]}
/>
```

## CtaBand

Closing conversion band with accent hairline.

| Name | Type | Note |
| --- | --- | --- |
| `eyebrow` | `string` | Mono label |
| `heading` | `ReactNode` | `h2` |
| `description` | `ReactNode` | Supporting line |
| `actions` | `ReactNode` | Button row |
| `...props` | `HTMLAttributes<HTMLElement>` | Spread |

```tsx
<CtaBand
  eyebrow="Next batch"
  heading="Seats close October 26"
  actions={<Button size="lg">Reserve a seat</Button>}
/>
```

## Footer

Brand block + mono link columns + newsletter row + socials + bottom bar.

| Name | Type | Note |
| --- | --- | --- |
| `brand` | `string` | Wordmark; also used in copyright |
| `tagline` | `string` | One-liner under the brand |
| `columns` | `{ title, links: { label, href }[] }[]` | Link columns |
| `newsletter` | `{ heading?, placeholder?, buttonLabel? } \| false` | Newsletter row; default button label `Langganan` (`#434343` fill); `false` hides |
| `socials` | `{ label, href, icon }[]` | Defaults to Instagram / LinkedIn / YouTube |
| `...props` | `HTMLAttributes<HTMLElement>` | Spread |

```tsx
<Footer
  brand="Koda"
  tagline="Career-first engineering bootcamp."
  columns={[{ title: "Program", links: [{ label: "Curriculum", href: "#curriculum" }] }]}
  newsletter={{ buttonLabel: "Langganan" }}
/>
```
