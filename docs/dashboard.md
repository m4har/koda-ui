# Dashboard (`components/dashboard`)

Console shells. Sticky header chrome (`sticky top-0 z-40` + blur) matches the landing navbar.

## SidebarShell

232px sidebar column + main column. Sidebar stacks above content below `lg`,
sticky full-height column at `lg+`.

| Name | Type | Note |
| --- | --- | --- |
| `sidebar` | `ReactNode` | Sidebar nav content |
| `header` | `ReactNode` | Shell header; wrapped in sticky chrome |
| `children` | `ReactNode` | Main content |
| `...props` | `HTMLAttributes<HTMLDivElement>` | Spread; `lg:grid-cols-[232px_1fr] lg:items-start` preset |

```tsx
<SidebarShell
  sidebar={<nav>…</nav>}
  header={<div className="flex h-14 items-center justify-between px-6"><h1 className="text-sm font-medium">Overview</h1></div>}
>
  <StatCard label="Active students" value={248} />
</SidebarShell>
```

## StatCard

KPI panel with mono delta line.

| Name | Type | Note |
| --- | --- | --- |
| `label` | `string` | Mono micro-label header |
| `value` | `ReactNode` | Big display number |
| `delta` | `string` | e.g. `"+12% vs last month"` |
| `trend` | `"positive" \| "negative" \| "neutral"` | Colors the delta; default `neutral` |
| `footer` | `ReactNode` | Small line under the delta |
| `...props` | `HTMLAttributes<HTMLDivElement>` | Spread |

```tsx
<StatCard label="Placement rate" value="95%" delta="+4% vs last batch" trend="positive" />
```

## ChartShell

Chart-agnostic frame: title, legend slot, loading skeleton. Works with any chart lib.

| Name | Type | Note |
| --- | --- | --- |
| `title` | `string` | Card title |
| `description` | `string` | Sub-line |
| `actions` | `ReactNode` | Legend / period switcher slot |
| `loading` | `boolean` | Swaps children for bar skeletons; default `false` |
| `children` | `ReactNode` | Chart body |
| `...props` | `HTMLAttributes<HTMLDivElement>` | Spread |

```tsx
<ChartShell title="Enrollments" description="Weekly" loading={isLoading}>
  <LineChart data={data} />
</ChartShell>
```

## ActivityFeed

Vertical timeline with tone dots.

| Name | Type | Note |
| --- | --- | --- |
| `items` | `{ id, title, description?, timestamp, tone? }[]` | `tone`: `default \| success \| warning \| destructive` |
| `emptyLabel` | `string` | Shown when `items` is empty; default `"No activity yet"` |
| `...props` | `OlHTMLAttributes<HTMLOListElement>` | Spread onto the `<ol>` |

```tsx
<ActivityFeed
  items={[
    { id: "1", title: "Application submitted", description: "Batch 11 — Golang", timestamp: "2h ago", tone: "success" },
  ]}
/>
```

## DataTable

Typed rows over the `ui/table` primitives with an empty state.

| Name | Type | Note |
| --- | --- | --- |
| `columns` | `{ header: string; cell: (row: T) => ReactNode }[]` | Column defs |
| `rows` | `T[]` | Row data |
| `getRowId` | `(row: T) => string` | Row key |
| `emptyLabel` | `string` | Default `"No records"` |
| `...props` | `HTMLAttributes<HTMLDivElement>` | Spread |

```tsx
<DataTable
  columns={[
    { header: "Name", cell: (r) => r.name },
    { header: "Status", cell: (r) => <Badge variant={r.active ? "success" : "muted"}>{r.active ? "Active" : "Paused"}</Badge> },
  ]}
  rows={students}
  getRowId={(r) => r.id}
/>
```
