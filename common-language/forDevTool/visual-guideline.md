# jelvo – Visual Guideline (Brand Guide 2026)

**Version:** 2.0.0
**Last Updated:** 2026-02-09

This is the **strict** visual system for jelvo-aligned UI in this repo.

**Sources of truth**
- Brand PDF: `docs/guidelines/Jelvo.Brand.Guide.2026.pdf`
- Tokens (extracted from the PDF): `docs/guidelines/docliq-tokens.json`

If anything conflicts, prefer the **brand PDF**, then `docliq-tokens.json`, then implementation.

**Related documents**

| Document | Purpose |
|----------|---------|
| `docliq-tokens.json` | Machine-readable token values |
| `copy-guidelines.md` | Tone, microcopy, and i18n rules |

---

## 1. Visual Identity

**jelvo** combines trust and efficiency, a digital companion that makes health appointments as simple as they should be.

**Name etymology:**
- **jel** = Health, well-being
- **vo** = Progress, advancement
- *Your health, finally simple.*

**Brand promise:** "Health should never be complicated. With one click, we take care of the rest."

### Three Pillars

| Trust | Efficiency | Humanity |
|-------|------------|----------|
| Professional and secure, like visiting a doctor, just digital | To an appointment in seconds. No waiting queues, no paperwork | Warmth in technology. Health is personal |

### Core Aesthetic

- **Warm and trustworthy**, not sterile or cold
- **Clean and clear**, prioritizing readability
- **Accessible for everyone**, from digital natives to beginners
- **Teal-dominant** for modern trust
- **Coral accents** for warmth and humanity

### Key Visual Qualities

| Quality | Expression |
|---------|------------|
| Trustworthy | Teal primary, clean typography, consistent spacing |
| Accessible | Large touch targets, high contrast (4.8:1 min), clear hierarchy |
| Efficient | Minimal decoration, purposeful whitespace, direct actions |
| Warm | Cream backgrounds, coral highlights, friendly motion |

---

## 2. Design Principles

### Design intent (non-negotiable)
- **Trust, efficiency, humanity** (professional healthcare tone; calm, not "startup flashy").
- **Mobile-first**: single-column, one primary action per screen, predictable navigation.
- **Germany + i18n-first**: support long German strings; avoid truncation; avoid idioms.
- **Semantic tokens**: use color roles, not hard-coded values.

### Design Rationale

**Why teal-dominant:**
- Combines the trust of blue with the warmth of green.
- Modern and distinctive without being clinical.
- Conveys both professionalism and approachability.

**Why cream backgrounds (#FAF8F5):**
- Warmer than cool grays, aligns with "Warmth in Technology" pillar.
- Reduces eye strain for extended use.
- Creates calm, welcoming environment.

**Why moderate border radius (8-16px):**
- Professional appearance without being harsh.
- Softer than clinical/corporate, but not playful.
- Balances trust with modernity.

**Why charcoal-tinted shadows:**
- Warm depth that complements cream backgrounds.
- Consistent with charcoal text color.
- Sophisticated without clinical coldness.

**Why DM Sans:**
- Modern, geometric sans-serif with excellent readability.
- Clean and technical, yet friendly.
- Excellent German character support (umlauts, eszett).
- Medium weight (500) adds typographic flexibility.

### Anti-Patterns

**Visual:**
- **Cool gray backgrounds**. Use cream for warmth.
- **Blue primary colors**. Use teal for modern trust.
- **Very rounded corners (24px+)** on primary elements. Feels too casual.
- **Low contrast text**. Maintain 4.8:1 minimum.
- **Decorative illustrations** without purpose. Every visual must inform or guide.
- Decorative gradients, glassmorphism, fintech "shine".
- Dense dashboards on mobile; too many CTAs per screen.
- Arbitrary blues/greens that don't map to jelvo tokens.

**Interaction:**
- **Overly bouncy animations**. Keep motion subtle and purposeful.
- **Gamification elements**. This is healthcare, not a game.
- **Hidden navigation**. Users must always know where they are.
- **Animations over 500ms**. Respect users' time.

**Content:**
- **Casual or trendy language**. Warm but professional.
- **Medical jargon without explanation**. Clear for all literacy levels.

---

## 3. Color System

### Color Philosophy

jelvo's palette combines professionalism with warmth. Teal for action, Slate for calm, Coral for humanity.

**Always use semantic tokens in components.** Primitives are for edge cases only.

Do not invent palettes. Use `docs/guidelines/docliq-tokens.json` → `color.semantic.*`.

### Brand Palette

| Color | Hex | Usage |
|-------|-----|-------|
| **Teal 500** | `#13A3B5` | Primary CTA |
| **Charcoal 500** | `#1C2A30` | Primary text |
| **Cream 100** | `#FAF8F5` | Background |
| **Slate 500** | `#5E7A86` | Secondary text |
| **Coral 500** | `#E88A73` | Accent |

### Core Surfaces

| Token | Hex | Usage |
|-------|-----|-------|
| `background.primary` | `#FAF8F5` | App background (Cream 100) |
| `background.secondary` | `#FFFFFF` | Card/surface |
| `background.tertiary` | `#F5F3EF` | Subtle section (Cream 200) |
| `background.inverse` | `#1C2A30` | Inverse surface (Charcoal 500) |

### Primary Action

| Token | Hex | Usage |
|-------|-----|-------|
| `interactive.primary` | `#13A3B5` | Default (Teal 500) |
| `interactive.primaryHover` | `#0F8A99` | Hover (Teal 600) |
| `interactive.primaryActive` | `#0B6F7C` | Active/pressed (Teal 700) |
| `text.onBrand` | `#FFFFFF` | Text on primary |

### Text

| Token | Hex | Usage |
|-------|-----|-------|
| `text.primary` | `#1C2A30` | Primary text (Charcoal 500) |
| `text.secondary` | `#5E7A86` | Secondary text (Slate 500) |
| `text.tertiary` | `#7C939D` | Large text only |
| `text.link` | `#0F8A99` | Link text (Teal 600) |

### Neutral

| Token | Hex | Usage |
|-------|-----|-------|
| `border` | `#E2E8F0` | Dividers, card borders |

### Status Colors (never color-only)

| State | Background | Border | Icon/Text |
|-------|-----------|--------|-----------|
| Success | `#E8F6F8` | `#13A3B5` | `#0B6F7C` |
| Error | `#FDF3F0` | `#E06A4F` | `#A03D2D` |
| Warning | `#FAE0D9` | `#E88A73` | `#C9503A` |
| Info | `#EEF1F3` | `#5E7A86` | `#3E5159` |

### Coral Usage Rules

- Highlights, badges, warmth moments (booking confirmation)
- Featured elements (top doctors, best times)
- **Never** for semantic states (success/warning/error use the status palette above)

---

## 4. Typography (DM Sans)

### Font Family

**Primary:** DM Sans
**Weights:** 400 (Regular), 500 (Medium), 600 (SemiBold), 700 (Bold)
**Fallback:** system-ui, sans-serif

Use `typography.*` from `docliq-tokens.json`.

### Mobile Type Scale (375-428px screens)

| Level | Size | Weight | Line Height | Usage |
|-------|------|--------|-------------|-------|
| H1 Display | 32px | 700 bold | 40px | Page titles |
| H2 Section | 24px | 600 semibold | 32px | Section headers |
| H3 Card | 20px | 600 semibold | 28px | Card titles, subsections |
| Body Large | 18px | 400 regular | 28px | Introductions, key info |
| Body | 16px | 400 regular | 24px | Default text |
| Label | 14px | 500 medium | 20px | Form labels, navigation |
| Caption | 14px | 400 regular | 20px | Metadata |
| Small | 12px | 400 regular | 16px | Fine print, timestamps |

### Desktop/Marketing Scale (web, presentations, landing pages)

| Level | Size |
|-------|------|
| H1 Display | 72px |
| H2 Section | 48px |
| H3 Card | 32px |
| Body Large | 20px |
| Body | 16px |

### Typography Rules

- No fixed-height text containers.
- Prefer wrapping; allow hyphenation where appropriate (`de-DE`).
- Overlines: uppercase, wider tracking (use sparingly).

### German Language Considerations

- German text is 20-30% longer than English equivalents.
- Design layouts with flexible widths, not fixed pixel counts.
- Test all UI with German text before English.
- Special characters (a, o, u, eszett) must render correctly.

---

## 5. Icons (Lucide)

### Icon Style

- **Source:** Lucide Icons
- **Stroke weight:** 2px (Lucide default)
- **Style:** Rounded corners, simple shapes
- **Color:** Inherit from parent (foreground, primary, etc.)

### Icon Sizing

| Context | Size |
|---------|------|
| Small / inline with text | 16px |
| Default / inline | 20px |
| Buttons, navigation | 24px |
| Feature illustrations | 32px |

### Icon Colors

| State | Color |
|-------|-------|
| Default | `text.secondary` (#5E7A86) |
| Active/Selected | `interactive.primary` (#13A3B5) |
| Disabled | `text.tertiary` (#7C939D) |
| Accent | Coral (#E88A73) |

---

## 6. Spacing & Layout

### Spacing Scale

```
4px (xs) → 8px (sm) → 12px → 16px (md) → 20px → 24px (lg) → 32px (xl) → 48px (2xl)
```

Use `spacing.*` (4px base).

### Screen Layout

| Element | Value |
|---------|-------|
| Page padding | 16-24px |
| Card padding | 20-24px |
| Section gap | 24-32px |
| Component gap | 12-16px |
| Minimum width | 320px |
| Minimum tap target | **44px** |
| Critical action target | **48px** |

---

## 7. Shapes & Border Radius

### Radius Scale

| Token | Value | Usage |
|-------|-------|-------|
| `radius.sm` | 8px | Chips, badges, small elements |
| `radius.md` | 8px | Buttons, inputs |
| `radius.lg` | 12px | Cards, panels |
| `radius.xl` | 16px | Bottom sheets, modals |
| `radius.pill` | 9999px | Pill buttons, avatars |

- Not too sharp (clinical/cold), not too round (playful/casual).
- Consistent application builds trust.

---

## 8. Shadows & Elevation

All shadows use charcoal tint (rgba(28, 42, 48, *)) for warm depth.

| Token | Value | Usage |
|-------|-------|-------|
| `shadow.sm` | 0 1px 3px rgba(28, 42, 48, 0.06) | Subtle depth, list items |
| `shadow.md` | 0 2px 8px rgba(28, 42, 48, 0.08) | Cards, default elevation |
| `shadow.lg` | 0 4px 16px rgba(28, 42, 48, 0.12) | Modals, sheets, overlays |

**Elevation hierarchy:**
1. **Background (0)**: Screen background, no shadow
2. **Surface (1)**: Cards, panels (`shadow.md`)
3. **Elevated (2)**: Modals, bottom sheets (`shadow.lg`)

Prefer `shadow.sm`/`shadow.md`; avoid heavy elevation except dialogs.

---

## 9. Visual Hierarchy

### Hierarchy Principles

1. **Primary actions** are most prominent (filled teal buttons).
2. **Secondary actions** are visible but subdued (outlined or ghost buttons).
3. **Destructive actions** use error color, positioned away from primary actions.
4. **Information hierarchy** follows: title, key data, metadata.

### Card Hierarchy

```
┌─────────────────────────────────┐
│ [Icon] Title              Badge │  ← Most prominent
│                                 │
│ Key information or action       │  ← Primary content
│                                 │
│ Secondary details, metadata     │  ← Subdued (caption style)
└─────────────────────────────────┘
```

---

## 10. Animation & Interaction

### Animation Principles

- **Purposeful:** Every animation guides attention, confirms action, or adds delight.
- **Subtle:** Smooth and refined, not bouncy or jarring.
- **Responsive:** 200-300ms for most interactions.
- **Reduced motion:** Honor `prefers-reduced-motion` setting.

### Timing

| Interaction | Duration | Easing |
|-------------|----------|--------|
| Micro interactions | 150ms | ease-out |
| Button press / hover | 200ms | ease-out |
| Default transitions | 200ms | ease-out |
| Page / modal transitions | 300ms | ease-out |
| Skeleton loading | 1.5s | linear (pulse) |

### Feedback Patterns

| Interaction | Effect |
|-------------|--------|
| Button hover | scale(1.05) or lift (translateY + shadow) |
| Button press | scale(0.98), slight opacity change |
| Success | Brief checkmark animation |
| Error | Subtle shake on invalid input |
| Loading | Skeleton screens, not spinners (where possible) |

### Do's and Don'ts

| Do | Don't |
|----|-------|
| Fast, subtle transitions (200-300ms) | Long animations (>500ms) |
| Consistent easing (ease-out) | Blinking/pulsing elements |
| Animation on interaction | Animation on critical flows |
| Respect reduced motion | Complex keyframe sequences |
| Hover scale/lift for delight | Bouncy spring physics |

---

## 11. Accessibility

### Overview

jelvo meets WCAG 2.1 AA compliance as minimum standard. Accessibility is built into the base design.

### Baseline

| Property | Standard |
|----------|----------|
| Contrast ratio | 4.8:1 minimum |
| Touch targets | 44px minimum |
| Base font size | 16px |
| Focus indicators | Visible, 2px teal ring |
| Keyboard navigation | Full support |

### Four Accessibility Pillars

| Visual | Motor | Auditory | Cognitive |
|--------|-------|----------|-----------|
| Contrast min. 4.8:1 | Full keyboard navigation | Subtitles for videos | Clear, simple language |
| Font size min. 16px | Skip links available | No audio autoplay | Consistent navigation |
| Focus indicators visible | Touch targets 44px+ | Visual alternatives | Errors clearly described |
| No text in images | No time limits | Transcripts available | Help always accessible |

### Enhanced Mode (Optional)

For users requiring additional accommodation:

| Property | Standard | Enhanced |
|----------|----------|----------|
| Base font size | 16px | 18px |
| Touch targets | 44px | 48px |
| Contrast ratio | 4.8:1 | 7:1 |
| Line height | 1.5 | 1.6 |
| Focus ring width | 2px | 3px |

```css
.accessibility-enhanced {
  --font-size-body: 1.125rem;
  --touch-target-min: 48px;
  --focus-ring-width: 3px;
}
```

---

## 12. Component Rules

### Buttons

| Type | Style |
|------|-------|
| Primary | Filled teal (#13A3B5), white text, rounded-md |
| Secondary | Outlined, neutral surface with border |
| Ghost | No border, teal text |
| Destructive | Filled error (#E06A4F), white text |
| Disabled | Neutral surface + muted text (not "ghost teal") |

### Cards

- White background (#FFFFFF)
- Rounded-lg (12px)
- Shadow-md (charcoal-tinted)
- Padding 20-24px

### Inputs

- Border: slate (#5E7A86) at 40% opacity
- Rounded-md (8px)
- Padding: 12-16px
- Focus: 2px teal ring
- Size: 16px (avoid iOS zoom)
- Error: icon + message, not color-only

### Bottom Sheets / Modals

- Rounded top (`radius.xl`, 16px)
- Shadow-lg
- White background
- Dim overlay
- Close button with 44px target
- Drag handle indicator

### Headers

- Sticky only when needed
- Keep titles short
- Provide back affordance

### Bottom Navigation

- Calm, neutral
- Active state: stronger text/underline, not aggressive brand blocks

---

## 13. Content & Tone

- German, informal "du" for a personal, modern approach (see `copy-guidelines.md`).
- Short, direct, reassuring; no marketing claims.
- Exclamation marks allowed in success states only (e.g. "Termin bestätigt!").
- Avoid diagnostic language; describe actions and next steps.

---

## 14. Emotional Feel

The jelvo experience should feel:

| Quality | Not |
|---------|-----|
| Warm | Cold |
| Trustworthy | Clinical |
| Clear | Boring |
| Efficient | Rushed |
| Helpful | Patronizing |
| Modern | Trendy |

**Target emotion:** "I trust this app with my health. It feels warm and gets things done quickly."

---

## Changelog

| Version | Date | Changes |
|---------|------|---------|
| 2.0.0 | 2026-02-09 | Merged MedAlpha-Flow depth. Correct brand colors (#13A3B5, #1C2A30, #FAF8F5, #5E7A86, #E88A73). Complete type scales. Accessibility section with 4.8:1 contrast. Design rationale. Anti-patterns. Component details. Shadow values. Informal "du". Exclamation marks in success states. Removed white-label. Removed stale file paths. |
| 1.0.0 | 2026-01-16 | Initial release |
