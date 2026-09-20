# Design tokens: Harbor Lantern

A calm, practical token starter for small product teams. Replace the values, keep the names stable, and make visual decisions in one place before implementing components.

This document is intentionally tool-agnostic. It can be read by a designer, copied into a design tool, or transformed into CSS, JSON, or native-platform tokens.

## How to use this file

1. Choose a product voice in `01. Foundations`.
2. Adjust primitive values before touching semantic values.
3. Use semantic tokens in components; avoid reaching into primitives from component code.
4. Record decisions in `06. Decisions` so the next contributor knows why a value exists.
5. Check the accessibility notes before shipping a color or typography change.

## 01. Foundations

### Product voice

- Clear before clever
- Warm without being noisy
- Dense where work happens, spacious where people decide
- Motion explains change; it does not decorate waiting

### Naming

Use lowercase dot-separated names. The last segment describes the role, not the appearance.

```text
primitive.color.blue.600
semantic.color.action.primary
component.button.height.md
```

### Token layers

| Layer | Purpose | Example |
| --- | --- | --- |
| Primitive | Raw scales that rarely change meaning | `primitive.color.blue.600` |
| Semantic | Meaning shared across components | `semantic.color.text.default` |
| Component | A local contract for a component | `component.button.bg.primary` |

## 02. Primitive tokens

### Color

The palette is a starting point, not a guarantee of accessible combinations.

```yaml
primitive:
  color:
    ink:
      950: "#10202B"
      800: "#243845"
      600: "#526672"
      400: "#8EA0A9"
      200: "#D5DEE2"
      50: "#F3F7F8"
    harbor:
      700: "#075E73"
      600: "#087F96"
      500: "#159AB1"
      100: "#D9F1F5"
    lantern:
      700: "#9A4A09"
      500: "#D97706"
      100: "#FFF1D6"
    meadow:
      700: "#21613D"
      500: "#3F8B5B"
      100: "#E0F3E7"
    ember:
      700: "#A52A2A"
      500: "#D14F4F"
      100: "#FDE4E4"
    paper:
      0: "#FFFFFF"
      25: "#FCFDFC"
      50: "#F7FAFA"
```

### Spacing

Use a 4px base unit. Prefer these steps over one-off values.

```yaml
primitive:
  space:
    0: "0px"
    1: "4px"
    2: "8px"
    3: "12px"
    4: "16px"
    5: "20px"
    6: "24px"
    8: "32px"
    10: "40px"
    12: "48px"
    16: "64px"
    20: "80px"
```

### Shape, border, and elevation

```yaml
primitive:
  radius:
    none: "0px"
    sm: "6px"
    md: "10px"
    lg: "16px"
    pill: "999px"
  border:
    thin: "1px"
    focus: "3px"
  shadow:
    none: "0 0 transparent"
    soft: "0 2px 8px rgba(16, 32, 43, 0.08)"
    lift: "0 8px 24px rgba(16, 32, 43, 0.12)"
```

### Typography

Use a system-first stack so the starter has no font dependency.

```yaml
primitive:
  font:
    family:
      sans: "ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif"
      mono: "ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace"
    size:
      xs: "12px"
      sm: "14px"
      md: "16px"
      lg: "18px"
      xl: "24px"
      2xl: "32px"
      3xl: "40px"
    line:
      tight: "1.2"
      normal: "1.5"
      relaxed: "1.7"
    weight:
      regular: 400
      medium: 500
      semibold: 600
      bold: 700
```

## 03. Semantic tokens

These are the values components should consume.

```yaml
semantic:
  color:
    canvas: "{primitive.color.paper.50}"
    surface: "{primitive.color.paper.0}"
    surface.subtle: "{primitive.color.ink.50}"
    text.default: "{primitive.color.ink.950}"
    text.muted: "{primitive.color.ink.600}"
    text.on-action: "{primitive.color.paper.0}"
    border.default: "{primitive.color.ink.200}"
    border.strong: "{primitive.color.ink.400}"
    action.primary: "{primitive.color.harbor.700}"
    action.primary-hover: "{primitive.color.harbor.600}"
    action.secondary: "{primitive.color.harbor.100}"
    status.success: "{primitive.color.meadow.700}"
    status.success-bg: "{primitive.color.meadow.100}"
    status.warning: "{primitive.color.lantern.700}"
    status.warning-bg: "{primitive.color.lantern.100}"
    status.danger: "{primitive.color.ember.700}"
    status.danger-bg: "{primitive.color.ember.100}"
    focus.ring: "{primitive.color.harbor.500}"
  font:
    body.family: "{primitive.font.family.sans}"
    body.size: "{primitive.font.size.md}"
    body.line: "{primitive.font.line.normal}"
    heading.family: "{primitive.font.family.sans}"
    heading.weight: "{primitive.font.weight.semibold}"
  space:
    page-inline: "{primitive.space.6}"
    section: "{primitive.space.12}"
    control-gap: "{primitive.space.2}"
    content-gap: "{primitive.space.4}"
  shape:
    control: "{primitive.radius.md}"
    card: "{primitive.radius.lg}"
```

## 04. Component contracts

Component tokens are the small, explicit interface between design and implementation.

### Button

```yaml
component:
  button:
    height:
      sm: "32px"
      md: "40px"
      lg: "48px"
    padding-inline:
      sm: "{primitive.space.3}"
      md: "{primitive.space.4}"
      lg: "{primitive.space.6}"
    radius: "{semantic.shape.control}"
    gap: "{primitive.space.2}"
    primary:
      bg: "{semantic.color.action.primary}"
      bg-hover: "{semantic.color.action.primary-hover}"
      text: "{semantic.color.text.on-action}"
    secondary:
      bg: "{semantic.color.action.secondary}"
      text: "{semantic.color.action.primary}"
    focus-ring: "{semantic.color.focus.ring}"
```

Behavior notes:

- Every button has a visible `:focus-visible` treatment.
- A disabled button must not be the only way to understand why an action is unavailable; pair it with nearby explanatory text when needed.
- Loading state preserves the button width and announces progress to assistive technology.

### Field

```yaml
component:
  field:
    label-gap: "{primitive.space.2}"
    input-height: "40px"
    input-padding-inline: "{primitive.space.3}"
    border: "{semantic.color.border.default}"
    border-hover: "{semantic.color.border.strong}"
    border-focus: "{semantic.color.focus.ring}"
    error-border: "{semantic.color.status.danger}"
    help-text: "{semantic.color.text.muted}"
```

Behavior notes:

- Labels are visible by default.
- Error text is adjacent to the field and connected with `aria-describedby`.
- Placeholder text is an example, never the only label.

### Card

```yaml
component:
  card:
    bg: "{semantic.color.surface}"
    border: "{semantic.color.border.default}"
    radius: "{semantic.shape.card}"
    padding: "{primitive.space.6}"
    shadow: "{primitive.shadow.soft}"
```

## 05. Responsive rules

Start with content constraints, then choose breakpoints only where the layout needs them.

```yaml
responsive:
  content-max: "1120px"
  compact: "0-639px"
  comfortable: "640-1023px"
  wide: "1024px+"
  rules:
    compact:
      page-inline: "{primitive.space.4}"
      section: "{primitive.space.8}"
    comfortable:
      page-inline: "{primitive.space.6}"
      section: "{primitive.space.10}"
    wide:
      page-inline: "{primitive.space.8}"
      section: "{primitive.space.16}"
```

Do not hide primary actions merely because the viewport is compact. Reflow, shorten labels only when the meaning remains clear, and make overflow intentional.

## 06. Accessibility checklist

Before release, verify the actual rendered interface rather than trusting token names.

- [ ] Body and muted text meet the intended contrast ratio against every surface.
- [ ] Keyboard focus is visible and not clipped by overflow.
- [ ] Color is not the only signal for status, validation, or selection.
- [ ] Text can zoom to 200% without loss of content or controls.
- [ ] Target sizes are usable on touch screens.
- [ ] Reduced-motion preferences disable nonessential transitions.
- [ ] Heading hierarchy reflects document structure.
- [ ] Form errors are announced and remain understandable without color.

## 07. Decisions

Use this small log for changes that would otherwise be lost in a pull request.

| Date | Decision | Reason | Owner |
| --- | --- | --- | --- |
| YYYY-MM-DD | Example: use a 4px spacing base | Keeps compact controls and roomy sections related | Name |

## 08. Handoff checklist

- [ ] Primitive values are free of product-specific meaning.
- [ ] Semantic names describe intent and have a fallback.
- [ ] Component contracts list states, not only the happy path.
- [ ] Tokens have one source of truth in implementation.
- [ ] Contrast, focus, zoom, and reduced-motion checks are recorded.
- [ ] A screenshot or link to the implemented state is attached to the change.
