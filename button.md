# Button

A button component with two types and three interactive states, used as the primary action trigger in the UI.

---

## Preview

| | Default | Hover | Disabled |
|---|---|---|---|
| **Primary** | Dark bg, white text | Slightly lighter dark bg, white text | Light gray bg, muted text |
| **Tertiary** | No bg, subtle gray text | Light gray bg, subtle gray text | — |

---

## Variants

### Type

| Value | Description |
|---|---|
| `primary` | High-emphasis action. Dark filled background. |
| `tertiary` | Low-emphasis action. No background by default. |

### State

| Value | Description |
|---|---|
| `default` | Resting state. |
| `hover` | User is hovering over the button. |
| `disabled` | Button is non-interactive. Reduces visual weight. |

---

## Design Tokens

### Backgrounds

| Token | Hex | Used when |
|---|---|---|
| `--color/background/bg-active` | `#111827` | Primary · Default |
| `--color/background/bg-active-hover` | `#374151` | Primary · Hover |
| `--color/background/bg-disabled` | `#f3f4f6` | Primary · Disabled |
| `--color/background/bg-hovered` | `#e5e7eb` | Tertiary · Hover |

### Text

| Token | Hex | Used when |
|---|---|---|
| `--color/text/text-inverse` | `#ffffff` | Primary · Default & Hover |
| `--color/text/text-disabled` | `#9ca3af` | Primary · Disabled |
| `--color/text/text-subtle` | `#6b7280` | Tertiary · Default & Hover |

---

## Anatomy

```
┌─────────────────────┐
│      Label text      │  ← Inter Medium 12px / line-height 16px
└─────────────────────┘
     ↑ 8px            ↑ 8px     (vertical padding)
  ← 12px           12px →       (horizontal padding)
      border-radius: 8px
```

---

## Spacing & Sizing

| Property | Value |
|---|---|
| Padding (horizontal) | `12px` |
| Padding (vertical) | `8px` |
| Border radius | `8px` |
| Layout | Flex column, center-aligned |

---

## Typography

| Property | Value |
|---|---|
| Font family | Inter |
| Font weight | Medium (500) |
| Font size | `12px` |
| Line height | `16px` |
| Letter spacing | `0` |
| Style name | `body/medium/sm` |

---

## States × Types Matrix

| State | Primary bg | Primary text | Tertiary bg | Tertiary text |
|---|---|---|---|---|
| Default | `#111827` | `#ffffff` | none | `#6b7280` |
| Hover | `#374151` | `#ffffff` | `#e5e7eb` | `#6b7280` |
| Disabled | `#f3f4f6` | `#9ca3af` | — | — |

> **Note:** The tertiary type does not have a formal disabled state in this design system.

---

## Default Label Copy

| Type | Label |
|---|---|
| Primary | Add Task |
| Tertiary | Cancel |

---

## Usage Guidelines

- Use **primary** for the main confirmatory action on a surface (e.g. "Add Task").
- Use **tertiary** for secondary or dismissive actions alongside a primary button (e.g. "Cancel").
- Never place two primary buttons side by side — pair primary with tertiary.
- Apply the `disabled` state when the action is unavailable; do not hide the button entirely.
