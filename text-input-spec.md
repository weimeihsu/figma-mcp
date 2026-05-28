# TextInput — Component Design Spec

**Source:** [官網元件Guideline — node 1321:6031](https://www.figma.com/design/R181m7W0JUi6SJz8wRsWAa/%E5%AE%98%E7%B6%B2%E5%85%83%E4%BB%B6Guideline?node-id=1321-6031)
**Last reviewed:** 2026-05-27

---

## 1. What It Is

A TextInput is a single-line form field that accepts free-text entry, supporting optional prefix/suffix labels, trailing icons, and inline validation feedback via an error state.

---

## 2. When to Use It

- Collecting short free-form text from a user (name, amount, keyword, etc.)
- Form fields that require inline prefix context (e.g., a currency symbol `$`)
- Fields that benefit from a trailing unit label (e.g., `單位`) or a filter/search affordance icon
- Search bars where a Bigger or highlighted style is needed for visual prominence

---

## 3. When NOT to Use It

- **Multi-line text** → use a Textarea instead
- **Selecting from a fixed list** → use a Select / Dropdown
- **Date or time entry** → use a DatePicker component
- **Passwords** → use a PasswordInput (masked variant of this component)
- **Read-only display of values with no editing intent** → use a plain text element; the Disable/Read-only state is only for temporarily locked fields that may become editable

---

## 4. Variants

| Variant | Purpose |
|---|---|
| **Normal** | Standard 16 px form field. Default for all general-purpose inputs. |
| **Bigger** | 20 px bold field for high-emphasis inputs, e.g., a primary search bar or a hero amount field. |
| **Highlight** | Bold green text on a light-green border. Used for a selected/active value that the user should notice at a glance (e.g., a confirmed amount). |

> `Highlight` is only defined for `type=Highlight` + `textConfigurations=input-text` + `state=Enable` + `error=false`. It does not have interactive sub-states — if the design calls for an editable highlight field, confirm with the design team.

---

## 5. States

| State | Trigger | Visual |
|---|---|---|
| **Enable** | Default resting state | White bg · Gray border `#BEBEBE` |
| **Hover** | Cursor enters the field | White bg · Green border `#26A862` · 3 px outer shadow `rgba(0,0,0,0.04)` |
| **Focus / Typing** | Field receives keyboard focus or user is typing | White bg · Green border `#26A862` · Insertion-point cursor shown |
| **Disable / Read-only** | Field is programmatically locked | Gray bg `#EEEEEE` · Gray border `#BEBEBE` · All text dimmed to `#BEBEBE` |
| **Error (modifier)** | Validation failure — overlaid on Enable, Hover, or Focus/Typing | Red border `#E00B00` replaces the green/gray border; hover shadow is retained in Hover+Error |

> **Error is a modifier**, not an independent state. It combines with Enable, Hover, and Focus/Typing. There is no Error+Disable variant.

---

## 6. Anatomy

```
┌─────────────────────────────────────────────────────────┐
│  [Prefix]  [Input Text / Placeholder]  [Clean] [Icon] [Suffix] │
└─────────────────────────────────────────────────────────┘
     1            2                        3       4       5
                         └── 6 (Insertion Point, Focus only)
```

1. **Container** — Outer clickable/tappable region. Height `42px`, border-radius `6px`, horizontal padding `16px`, vertical padding `6px`. Width defaults to `350px` (override per layout context).
2. **Prefix Text** *(optional)* — Short label left of the input text; e.g., `$`. Visible only in Normal type when `prefixText=true` and state is Enable, Hover, or Focus/Typing. Color `#555555` (Gray700). Disabled state dims to `#BEBEBE`.
3. **Input Area** — Flex-grow region that holds either placeholder text or typed input text.
   - **Placeholder text** — `#BEBEBE` (Gray400), communicates expected format
   - **Input text** — `#333333` (Gray900), the user's actual content
4. **Insertion Point** *(Focus/Typing only)* — 1 px wide, `26px` tall, `#333333`. Appears at the left edge of the Input Area in placeholder mode, and after the last character in input-text mode.
5. **Clean Icon** *(optional, Focus/Typing + input-text only)* — 20×20 px × icon. Shown when `cleanIcon=true`. Clears the field value on click. Uses asset `i-19 / Union`.
6. **Trailing Icon** *(optional)* — 20×20 px filter/search icon. Shown when `showSearchIconRear=true`. Visible across Enable, Hover, and Focus/Typing states (Normal type). Uses asset `Icon/30/gray/filter / Union`.
7. **Suffix Text** *(optional)* — Short unit label right of the field; e.g., `單位`. Visible in Normal type when `suffixText=true`. Color `#555555`; dims to `#BEBEBE` in Disable state.

---

## 7. Properties (Figma)

| Property | Type | Values | Default |
|---|---|---|---|
| `type` | Enum | `Normal`, `Bigger`, `Highlight` | `Normal` |
| `state` | Enum | `Enable`, `Hover`, `Focus / Typing`, `Disable / Read-only` | `Enable` |
| `textConfigurations` | Enum | `placeholder-text`, `input-text` | `placeholder-text` |
| `error` | Boolean | `true` / `false` | `false` |
| `text` | String | Any text content | `"Input"` |
| `prefixText` | Boolean | `true` / `false` | `true` |
| `suffixText` | Boolean | `true` / `false` | `true` |
| `showSearchIconRear` | Boolean | `true` / `false` | `true` |
| `cleanIcon` | Boolean | `true` / `false` | `false` |

> `cleanIcon` is only rendered when `textConfigurations=input-text` AND `state=Focus / Typing`.

---

## 8. Design Tokens

| Token | Value | Usage |
|---|---|---|
| `Text/Gray900` | `#333333` | Input text, insertion-point color |
| `Text/Gray700` | `#555555` | Prefix/suffix text, placeholder labels |
| `Neutral/Gray400` | `#BEBEBE` | Placeholder text, default border, disabled text |
| `Supporting/Gray200` | `#EEEEEE` | Disabled/read-only background |
| `Neutral/White` | `#FFFFFF` | Active field background |
| `Main_Cathay/Green600` | `#26A862` | Focus and hover border, Highlight border |
| `Supporting/Green200` | `#C3E6BB` | Highlight variant border (lighter green) |
| `Error/Red600` | `#E00B00` | Error-state border |
| `Form/Hover` | Drop shadow `0 0 0 3px rgba(0,0,0,0.04)` | Hover state outer glow |
| Font: Normal | `Noto Sans TC Regular 16px / line-height 1.5` | Normal type text |
| Font: Bigger | `Noto Sans TC Bold 20px / line-height 1.5` | Bigger type text |

---

## 9. Usage Rules

**Do:**
- Use `Normal` as the default for all standard form fields.
- Use `Bigger` for primary/hero fields where the input value needs visual weight (e.g., a currency amount on a transfer screen).
- Use `Highlight` exclusively for confirmed/selected values the user should notice — not for active editing.
- Show the `cleanIcon` when the field is focused and contains text, so users can clear quickly.
- Always pair an error-state field with an explicit error message below the field — never rely on the red border alone.
- Use `prefixText` (`$`) and `suffixText` (`單位`) only when the unit or currency is fixed and cannot change; otherwise, incorporate it into the label.

**Don't:**
- Don't show `Highlight` type in an editable/interactive flow — it implies a finalized value.
- Don't use `Disable / Read-only` to hide content from users; use conditional rendering instead.
- Don't combine `error=true` with `Disable / Read-only` — disabled fields cannot be invalid.
- Don't use the Bigger type inside dense forms; it is intended for isolated, prominent inputs only.
- Don't omit the field label (rendered outside this component) — the placeholder text is not a substitute for a label.

---

## 10. Accessibility Notes

- **Keyboard navigation** — Focusable via `Tab`. Text entry works as standard. The insertion-point cursor should be replicated via native `<input>` caret behavior.
- **Screen reader** — Use a native `<input type="text">` element with an associated `<label>`. The placeholder is supplemental; never use it as the only accessible name.
- **Error state** — Pair `aria-invalid="true"` on the `<input>` with `aria-describedby` pointing to the error message element below the field.
- **Disabled state** — Use `disabled` attribute (not just visual styling) so assistive technologies correctly report the field as non-interactive. Tooltip or help text should explain why the field is locked when possible.
- **Focus ring** — The green `#26A862` border constitutes the focus indicator. Verify it meets 3:1 contrast against the white background. Do not suppress default `outline` without this custom border in place.
- **Color alone** — The red error border (`#E00B00`) must always be accompanied by a text error message; do not rely on color alone to indicate failure.
- **Touch target** — The 42 px height meets the minimum 44 px guideline only when combined with surrounding tap-area padding; verify on mobile context. *(Confirm with design team.)*
- **Insertion point visibility** — The 1 px cursor line meets the minimum 2 px WCAG 2.2 focus indicator requirement only if considered alongside the border. Confirm implementation aligns with accessibility audit requirements. *(Assumed — confirm with design team.)*

---

## 11. Related Components

| Component | Relationship |
|---|---|
| **TextArea** | Multi-line variant; use when input may exceed one line |
| **SearchInput** | Specialisation of TextInput with a leading search icon and built-in clear behavior |
| **Select / Dropdown** | Use when the user must choose from a predefined list rather than type freely |
| **DatePicker** | Use for date/time entry |
| **FormField** | Wrapper that combines Label + TextInput + Helper/Error text into a complete form row |

---

*Generated from Figma file 官網元件Guideline · node 1321:6031 · 2026-05-27*
