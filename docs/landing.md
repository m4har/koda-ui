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

Left line-number rail: 28px column of 20px cells numbered 1..N, full document
height. Auto-sizes by default: a ResizeObserver measures the wrapper and renders
height / 21 cells (20px cell + 1px gap), re-measured on resize — one rail adapts
from mobile to desktop. Place inside a `relative` page wrapper; it scrolls with
content (never fixed). Offset page content with `pl-7` (28px) on the same wrapper
so text never sits under the rail at any viewport.

| Name | Type | Note |
| --- | --- | --- |
| `rows` | `number` | Optional fixed count; omit for auto-size (measured height / 21, live on resize) |
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

Hairline card grid; index labels auto-number when `index` is omitted. Cells can
carry a full-bleed 4:3 `visual` slot (photo), which is how a section renders
5 features + 2 image cells in one grid.

| Name | Type | Note |
| --- | --- | --- |
| `features` | `{ index?, title, description, icon?, visual? }[]` | Grid cells; `visual` renders a bordered 4:3 block (`[&_img]` is forced to `size-full object-cover`) |
| `...props` | `HTMLAttributes<HTMLElement>` | Spread; `gap-px bg-border` preset |

```tsx
<FeatureGrid
  features={[
    { title: "Biaya dicicil setelah dapat kerja", description: "Cicilan baru mulai setelah kamu berpenghasilan.", icon: <Wallet /> },
    { title: "Asrama & dapur bersama", description: "Tinggal dekat kelas, biaya hidup ditekan.", icon: <Home /> },
    { title: "Pinjaman laptop bila perlu", description: "Perangkat pinjaman sampai kamu siap beli sendiri.", icon: <Laptop /> },
    { title: "Pendampingan sampai dapat kerja", description: "Latihan interview dan review portofolio rutin.", icon: <Users /> },
    { title: "Tech stack sesuai dunia kerja", description: "Repo, CI, dan code review seperti tim produksi.", icon: <GitBranch /> },
    { title: "Foto kelas", description: "", visual: <img src="/foto-kelas.jpg" alt="Suasana kelas" /> },
    { title: "Foto proyek", description: "", visual: <img src="/foto-proyek.jpg" alt="Pengerjaan proyek akhir" /> },
  ]}
/>
```

## CareerPillars

"Why us" block: mono eyebrow + heading + four uppercase pillar cards on the
same hairline grid as `FeatureGrid`. Titles render uppercase; keep them 2–4 words.

| Name | Type | Note |
| --- | --- | --- |
| `eyebrow` | `string` | Mono `Label`, e.g. `"KENAPA MEMILIH BOOTCAMP INI"` |
| `heading` | `ReactNode` | Optional `h2` |
| `pillars` | `{ title, description, index? }[]` | Four cells; `index` auto-numbers `01..0N` |
| `...props` | `HTMLAttributes<HTMLElement>` | Spread |

```tsx
<CareerPillars
  eyebrow="KENAPA MEMILIH BOOTCAMP INI"
  heading="Fokus kami untuk karirmu"
  pillars={[
    { title: "Mentoring 1-on-1", description: "Satu mentor tetap per peserta, sesi mingguan." },
    { title: "Job readiness", description: "Portofolio, CV, dan latihan teknis interview." },
    { title: "Sudut pandang recruiter", description: "Review CV dari sisi perekrut, plus personal branding." },
    { title: "Dukungan interview", description: "Simulasi tes teknis dan pendampingan sampai lolos." },
  ]}
/>
```

## CurriculumAccordion

Single-open module accordion. Each trigger is a native `button` whose
accessible name is exactly `NN Judul Modul Lihat N materi` — the number, the
module title, and the materials meta are read as one string, so do not move the
meta outside the button. The header carries a `N modul` counter derived from
`modules.length`.

| Name | Type | Note |
| --- | --- | --- |
| `modules` | `{ nomor, judul, materiCount, isi }[]` | `nomor` is a padded string (`"01"`); `isi` is the panel content |
| `heading` | `ReactNode` | Optional `h2` |
| `eyebrow` | `string` | Mono `Label`; the counter sits next to it |
| `counterLabel` | `string` | Overrides the default `{N} modul` |
| `defaultOpen` | `number` | Pre-opened module index, default `0` |
| `...props` | `HTMLAttributes<HTMLElement>` | Spread |

a11y: triggers carry `aria-expanded` + `aria-controls`, panels are
`role="region"` with `aria-labelledby`, and collapsed panels use `hidden`
(removed from the a11y tree). Keyboard: native button behaviour — Tab to the
trigger, Enter/Space to toggle. There is no accordion primitive in `ui/`, so this
component is intentionally standalone rather than a wrapper.

```tsx
<CurriculumAccordion
  eyebrow="Kurikulum"
  heading="Enam modul, satu jalur"
  modules={[
    { nomor: "01", judul: "Dasar Pemrograman Web", materiCount: 6, isi: "HTML, CSS, Git, dan dasar JavaScript." },
    { nomor: "02", judul: "Front End Development", materiCount: 4, isi: "Komponen UI, state, dan konsumsi API." },
    { nomor: "03", judul: "Back End Development", materiCount: 8, isi: "HTTP, basis data, auth, dan pengujian." },
    { nomor: "04", judul: "DevOps & Deployment", materiCount: 2, isi: "CI/CD dan deploy ke server sendiri." },
    { nomor: "05", judul: "Capstone Project", materiCount: 1, isi: "Satu produk nyata dikerjakan berkelompok." },
    { nomor: "06", judul: "Career Preparation", materiCount: 1, isi: "CV, portofolio, dan simulasi interview." },
  ]}
/>
```

## AlumniCarousel

Alumni story carousel: one active slide (name + role large) with the
`Tonton cerita lengkap` CTA, `Previous`/`Next` controls, and one dot button per
slide. Uncontrolled and wrapping; state lives inside the component.

| Name | Type | Note |
| --- | --- | --- |
| `items` | `{ name, year, role, tone }[]` | Reference composition uses 10; `tone` is `"pink" \| "yellow" \| "green" \| "blue"` |
| `storyHref` | `string` | Link target of the CTA, default `"#"` |
| `...props` | `HTMLAttributes<HTMLElement>` | Spread on the `section` |

a11y: root is `role="region"` + `aria-roledescription="carousel"`; the dot group
is `role="group"` with `aria-label="Navigasi slide alumni"`; each dot is a
button with `aria-label="Putar slide N"` (1-based) and `aria-current` on the
active one; `Previous` / `Next` are `Button size="icon"` with those exact
`aria-label`s. Keyboard: Tab reaches every control, Enter/Space activates.

Tone colors come from the `--alumni-*` tokens in `globals.css` (see the README
token table) and are applied as the slide's 4px top border, so the card body
stays `bg-card` in both themes.

```tsx
<AlumniCarousel
  storyHref="/alumni/sari-andini"
  items={[
    { name: "Sari Andini", year: "2025", role: "Frontend Engineer", tone: "pink" },
    { name: "Budi Prasetyo", year: "2024", role: "Backend Engineer (Go)", tone: "blue" },
    { name: "Nadia Kusuma", year: "2025", role: "QA Engineer", tone: "green" },
    { name: "Rangga Wijaya", year: "2023", role: "DevOps Engineer", tone: "yellow" },
    { name: "Intan Permata", year: "2024", role: "Data Analyst", tone: "pink" },
    { name: "Yoga Santoso", year: "2025", role: "Mobile Engineer", tone: "blue" },
    { name: "Citra Halim", year: "2023", role: "Product Engineer", tone: "green" },
    { name: "Fajar Nugroho", year: "2024", role: "Platform Engineer", tone: "yellow" },
    { name: "Maya Larasati", year: "2025", role: "Fullstack Engineer", tone: "pink" },
    { name: "Dimas Ardianto", year: "2023", role: "Cloud Engineer", tone: "blue" },
  ]}
/>
```

## NextDirimuBand

One full-width `<a>` — giant uppercase text plus an arrow that nudges on hover,
text turning accent. Use it as the last push before the footer.

| Name | Type | Note |
| --- | --- | --- |
| `href` | `string` | Registration page target |
| `label` | `string` | Band text, default `"Next Dirimu"`; rendered uppercase |
| `...props` | `HTMLAttributes<HTMLAnchorElement>` | Spread on the `<a>` |

a11y: it is a single anchor, so it is one tab stop with a focus ring; the arrow
is `aria-hidden`, meaning the accessible name is just the label — put the whole
meaning in `label`.

```tsx
<NextDirimuBand href="/daftar" label="Next Dirimu" />
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
