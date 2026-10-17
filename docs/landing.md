# Landing (`components/landing`)

Public marketing chrome. Pair with `ui/section-frame` for section structure.

## Navbar

Sticky top chrome matching the dashboard shell header.

| Name | Type | Note |
| --- | --- | --- |
| `brand` | `string` | Mono wordmark |
| `items` | `{ label: string; href: string }[]` | Nav links; hidden below `md` |
| `cta` | `{ label: string; href: string }` | Renders a `Button asChild` |
| `...props` | `HTMLAttributes<HTMLElement>` | Spread; `sticky top-0 z-40` preset |

```tsx
<Navbar
  brand="Koda"
  items={[{ label: "Curriculum", href: "#curriculum" }, { label: "Alumni", href: "#alumni" }]}
  cta={{ label: "Apply now", href: "/apply" }}
/>
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

Brand block + mono link columns + bottom bar.

| Name | Type | Note |
| --- | --- | --- |
| `brand` | `string` | Wordmark; also used in copyright |
| `tagline` | `string` | One-liner under the brand |
| `columns` | `{ title, links: { label, href }[] }[]` | Link columns |
| `...props` | `HTMLAttributes<HTMLElement>` | Spread |

```tsx
<Footer
  brand="Koda"
  tagline="Career-first engineering bootcamp."
  columns={[{ title: "Program", links: [{ label: "Curriculum", href: "#curriculum" }] }]}
/>
```
