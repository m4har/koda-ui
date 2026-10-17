# Auth (`components/auth`)

## AuthCard

Centered auth panel on a muted backdrop: brand mark, bordered card, form slot, footer row.

| Name | Type | Note |
| --- | --- | --- |
| `title` | `string` | Card title |
| `description` | `string` | Sub-line under the title |
| `brand` | `string` | Mono wordmark above the card |
| `footer` | `ReactNode` | Rendered under the card (link row, hint) |
| `children` | `ReactNode` | The form |
| `...props` | `HTMLAttributes<HTMLDivElement>` | Spread |

```tsx
<AuthCard
  brand="Koda"
  title="Sign in"
  description="Use your cohort email."
  footer={
    <a href="/reset" className="font-mono text-[10px] uppercase tracking-[0.1em] text-muted-foreground hover:text-foreground">
      Forgot password
    </a>
  }
>
  <form className="flex flex-col gap-4" onSubmit={submit}>
    <div className="flex flex-col gap-1.5">
      <Label>Email</Label>
      <Input type="email" name="email" required placeholder="you@example.com" />
    </div>
    <div className="flex flex-col gap-1.5">
      <Label>Password</Label>
      <Input type="password" name="password" required />
    </div>
    <Button type="submit" loading={pending}>Sign in</Button>
  </form>
</AuthCard>
```
