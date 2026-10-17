# Primitives (`components/ui`)

Base layer. Import each component from its own file — no barrels.

## Button

`cva` variants with press feedback and `motion-reduce` guard baked in. `loading` renders the built-in `Spinner`, sets `aria-busy`, disables the button. On `asChild` children pass through untouched.

| Name | Type | Note |
| --- | --- | --- |
| `variant` | `"default" \| "outline" \| "ghost" \| "link" \| "destructive"` | cva variant, default `default` |
| `size` | `"default" \| "sm" \| "lg" \| "icon"` | cva variant, default `default` |
| `asChild` | `boolean` | Render as the child element via Radix `Slot` |
| `loading` | `boolean` | Spinner + `aria-busy` + disabled |
| `iconLeft` | `React.ReactNode` | Leading icon slot |
| `iconRight` | `React.ReactNode` | Trailing icon slot |
| `className` | `string` | Merged with variant classes |
| `...props` | `ButtonHTMLAttributes` | Spread onto the element |

```tsx
<Button loading={saving} iconLeft={<Save className="size-4" />} onClick={save}>
  Save changes
</Button>

<Button asChild variant="outline">
  <a href="/docs">Read the docs</a>
</Button>
```

## Badge

Mono uppercase status token.

| Name | Type | Note |
| --- | --- | --- |
| `variant` | `"default" \| "outline" \| "muted" \| "success" \| "warning" \| "destructive" \| "info"` | default `default` |
| `...props` | `HTMLAttributes<HTMLSpanElement>` | Spread |

```tsx
<Badge variant="success">Active</Badge>
<Badge variant="outline">Batch 11</Badge>
```

## Card

Standard panel set.

| Name | Type | Note |
| --- | --- | --- |
| `...props` | `HTMLAttributes<HTMLDivElement>` | Spread; `className` merged |

```tsx
<Card>
  <CardHeader>
    <CardTitle>Revenue</CardTitle>
    <CardDescription>Last 30 days</CardDescription>
  </CardHeader>
  <CardContent>…</CardContent>
</Card>
```

## Input / Textarea

Sharp-cornered fields with focus-border ring.

| Name | Type | Note |
| --- | --- | --- |
| `type` | `string` (Input only) | Native input type |
| `...props` | `InputHTMLAttributes` / `TextareaHTMLAttributes` | Spread |

```tsx
<Input placeholder="you@example.com" aria-label="Email" />
<Textarea placeholder="Message" rows={4} />
```

## Label

The kit's ONE micro-label primitive: mono, 10px, uppercase, `tracking-[0.1em]`.
Reuse everywhere; never redefine in a second file.

| Name | Type | Note |
| --- | --- | --- |
| `...props` | `HTMLAttributes<HTMLSpanElement>` | Spread |

```tsx
<Label>01 / Curriculum</Label>
```

## Select

Native `<select>` wrapper with chevron. Zero deps — keyboard and screen-reader
behavior for free.

| Name | Type | Note |
| --- | --- | --- |
| `children` | `ReactNode` | `<option>` elements |
| `...props` | `SelectHTMLAttributes` | Spread |

```tsx
<Select defaultValue="golang" aria-label="Track">
  <option value="golang">Golang</option>
  <option value="java">Java</option>
</Select>
```

## Table

Hairline table primitives; heads use the mono micro-label style.

| Name | Type | Note |
| --- | --- | --- |
| `...props` | `HTMLAttributes` (table-level) | Spread |

```tsx
<Table>
  <TableHeader>
    <TableRow><TableHead>Name</TableHead><TableHead>Status</TableHead></TableRow>
  </TableHeader>
  <TableBody>
    <TableRow><TableCell>Rani</TableCell><TableCell><Badge>Active</Badge></TableCell></TableRow>
  </TableBody>
</Table>
```

## Skeleton / SkeletonText

Shimmering placeholder for content with a known shape. Use `Spinner` for
indeterminate waits instead.

| Name | Type | Note |
| --- | --- | --- |
| `lines` | `number` (SkeletonText only) | Number of bars, last is `w-2/3`; default 3 |
| `...props` | `HTMLAttributes<HTMLDivElement>` | Spread |

```tsx
<Skeleton className="h-8 w-40" />
<SkeletonText lines={4} />
```

## Spinner

Indeterminate loading icon. Built from an SVG circle with a `strokeOpacity` track;
needs the `spinner` keyframes from `globals.css`.

| Name | Type | Note |
| --- | --- | --- |
| `...props` | `SVGProps<SVGSVGElement>` | Spread; `role="status"` already set |

```tsx
<Spinner className="size-6" />
```

## Separator

Hairline rule.

| Name | Type | Note |
| --- | --- | --- |
| `orientation` | `"horizontal" \| "vertical"` | default `horizontal` |
| `...props` | `HTMLAttributes<HTMLDivElement>` | Spread |

```tsx
<Separator />
<Separator orientation="vertical" className="h-6" />
```

## SectionFrame

Landing section chrome: top hairline, mono eyebrow, heading block, content slot.

| Name | Type | Note |
| --- | --- | --- |
| `eyebrow` | `string` | HUD index label, e.g. `"02 / Curriculum"` |
| `heading` | `ReactNode` | Section `h2` |
| `description` | `ReactNode` | Supporting line |
| `as` | `"section" \| "div"` | Element tag, default `section` |
| `...props` | `HTMLAttributes<HTMLElement>` | Spread |

```tsx
<SectionFrame eyebrow="02 / Curriculum" heading="Six modules, one capstone">
  <FeatureGrid features={features} />
</SectionFrame>
```
