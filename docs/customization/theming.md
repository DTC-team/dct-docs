# Theming

Theming is **provisioned per partner by the Bluecom team during onboarding** (not self-serve in v1). You supply brand tokens; Bluecom creates a CSS class bound to your `partnerCode`.

## What you supply during onboarding

- Primary color (`#RRGGBB` or `oklch(...)`)
- Logo URL

## What's themeable

OKLCh CSS custom properties:

- `--primary`, `--primary-foreground`
- `--secondary`, `--muted`
- `--ring`
- `--chart-1` … `--chart-5`
- `--sidebar-*` family

## What's not themeable today

- Logo placement and layout
- Typography (font family, weights)
- Component shapes (radii, borders)
- Iconography

## Changing your theme after launch

Email `integrations@bluecom.vn` with the new tokens. Changes apply on the next deploy (typically within 1 business day).
