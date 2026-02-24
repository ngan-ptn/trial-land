# Design System Workflow

A step-by-step prompt chain for building a design system from visual inspiration.

---

## Workflow Overview

```
[Visual Moodboard] → [Concept] → [Foundation (Tokens)] → [Stress-Test Preview] → [Design Guideline] → [Functional Component Specs] → [Decision Trees] → [Storybook] → [App]
```

| Step | Input | Output |
|------|-------|--------|
| 1 | Moodboard link/image | Concept document |
| 2 | Concept document | Design tokens (JSON) + WCAG contrast validation |
| 3 | Design tokens | Stress-Test Preview (high-density layout) |
| 3b | Tokens + Stress-Test results | Design Guideline (detailed token system + styling rules) |
| 4 | Stress-Test HTML | Functional Component Groups + TypeScript interfaces |
| 4b | Component specs | Decision Trees (IF/THEN selection logic) |
| 5 | Specs + Decision Trees | Storybook setup (functional folder structure) |
| 6 | Storybook | App screens |

---

## Step 1: Extract Concept from Visual Moodboard

### Purpose
Translate visual inspiration into structured design intent that AI can use consistently.

### Command
```
Context:
This is a visual moodboard for a product feature.
Do NOT generate UI yet.

Moodboard source: [PASTE LINK OR DESCRIBE IMAGE]

Emotional intent:
- Create: [what feelings should the design evoke]
- Avoid: [what feelings must be prevented]

Visual tokens extracted from moodboard:
- Color: [describe palette - warm/cool, saturated/muted, primary/accent]
- Contrast: [high/low, where contrast is used]
- Shape: [rounded/sharp, organic/geometric, corner radius tendency]
- Layout density: [spacious/compact, whitespace usage]
- Typography tone: [friendly/formal, heavy/light, serif/sans]
- Motion tone: [playful/subtle, fast/slow, bouncy/smooth]

Behavioral purpose:
This visual direction is meant to influence user behavior by...

Boundaries / anti-patterns:
- Never...
- Avoid...
- Do not...

Task:
Explain back this visual direction in your own words,
and list 3 risks if it is implemented incorrectly.
```

### Output Format
```markdown
# Design Concept: [Concept Name]

## Visual Direction Summary
[2-3 sentence explanation in AI's own words]

## Emotional Framework
| Create | Avoid |
|--------|-------|
| [emotion] | [emotion] |

## Extracted Visual Tokens
- **Color:** [description]
- **Contrast:** [description]
- **Shape:** [description]
- **Layout density:** [description]
- **Typography tone:** [description]
- **Motion tone:** [description]

## Behavioral Intent
[How this design influences user behavior]

## Implementation Risks
1. **[Risk name]:** [description and how to prevent]
2. **[Risk name]:** [description and how to prevent]
3. **[Risk name]:** [description and how to prevent]

## Anti-Patterns Checklist
- [ ] Never [action]
- [ ] Avoid [action]
- [ ] Do not [action]
```

---

## Step 2: Generate Design Foundation (Tokens)

### Purpose
Convert the concept into concrete, code-ready design tokens.

### Command
```
Based on this design concept:
[PASTE CONCEPT FROM STEP 1]

Generate a design token foundation in JSON format.

Requirements:
- Use semantic naming (not "blue-500" but "color-primary")
- Include all categories: color, spacing, typography, radius, shadow, motion
- Provide both light mode values (dark mode optional)
- Use CSS-compatible values (px, rem, hex, rgba)
- Include usage comments for each token

Accessibility Requirements (WCAG AA Compliance):
- Ensure all text/background color pairings meet minimum contrast ratios:
  - Normal text (< 18px): 4.5:1 contrast ratio
  - Large text (>= 18px bold or >= 24px): 3:1 contrast ratio
  - UI components and graphics: 3:1 contrast ratio
- For each color pairing, include the contrast ratio in the output
- If a token fails contrast requirements, adjust lightness/darkness until it passes
- Include a "contrastPairings" section documenting all validated combinations

Target framework: [Tailwind CSS / CSS Variables / Styled Components / etc.]

Output a single JSON file that can be imported into the codebase.
```

### Output Format
```json
{
  "$schema": "design-tokens",
  "version": "1.0.0",
  "concept": "[Concept Name]",

  "color": {
    "primary": {
      "value": "#hexcode",
      "usage": "Primary actions, key UI elements"
    },
    "secondary": {
      "value": "#hexcode",
      "usage": "Secondary actions, supporting elements"
    },
    "background": {
      "default": { "value": "#hexcode", "usage": "Page background" },
      "elevated": { "value": "#hexcode", "usage": "Cards, modals" }
    },
    "text": {
      "primary": { "value": "#hexcode", "usage": "Headings, body text" },
      "secondary": { "value": "#hexcode", "usage": "Captions, hints" },
      "inverse": { "value": "#hexcode", "usage": "Text on dark backgrounds" }
    },
    "semantic": {
      "success": { "value": "#hexcode", "usage": "Success states" },
      "warning": { "value": "#hexcode", "usage": "Warning states" },
      "error": { "value": "#hexcode", "usage": "Error states" },
      "info": { "value": "#hexcode", "usage": "Informational states" }
    },
    "border": {
      "default": { "value": "#hexcode", "usage": "Default borders" },
      "focus": { "value": "#hexcode", "usage": "Focus rings" }
    }
  },

  "spacing": {
    "xs": { "value": "4px", "usage": "Tight spacing, icon gaps" },
    "sm": { "value": "8px", "usage": "Small gaps, inline spacing" },
    "md": { "value": "16px", "usage": "Default component padding" },
    "lg": { "value": "24px", "usage": "Section spacing" },
    "xl": { "value": "32px", "usage": "Large section gaps" },
    "2xl": { "value": "48px", "usage": "Page-level spacing" }
  },

  "typography": {
    "fontFamily": {
      "primary": { "value": "'Inter', sans-serif", "usage": "All UI text" },
      "mono": { "value": "'JetBrains Mono', monospace", "usage": "Code, numbers" }
    },
    "fontSize": {
      "xs": { "value": "12px", "lineHeight": "16px", "usage": "Captions, labels" },
      "sm": { "value": "14px", "lineHeight": "20px", "usage": "Body small" },
      "base": { "value": "16px", "lineHeight": "24px", "usage": "Body default" },
      "lg": { "value": "18px", "lineHeight": "28px", "usage": "Body large" },
      "xl": { "value": "20px", "lineHeight": "28px", "usage": "Heading small" },
      "2xl": { "value": "24px", "lineHeight": "32px", "usage": "Heading medium" },
      "3xl": { "value": "30px", "lineHeight": "36px", "usage": "Heading large" },
      "4xl": { "value": "36px", "lineHeight": "40px", "usage": "Display" }
    },
    "fontWeight": {
      "normal": { "value": "400", "usage": "Body text" },
      "medium": { "value": "500", "usage": "Emphasis" },
      "semibold": { "value": "600", "usage": "Headings, buttons" },
      "bold": { "value": "700", "usage": "Strong emphasis" }
    }
  },

  "radius": {
    "none": { "value": "0px", "usage": "Sharp corners" },
    "sm": { "value": "4px", "usage": "Subtle rounding" },
    "md": { "value": "8px", "usage": "Default rounding" },
    "lg": { "value": "12px", "usage": "Cards, containers" },
    "xl": { "value": "16px", "usage": "Large cards" },
    "2xl": { "value": "24px", "usage": "Modals, prominent elements" },
    "full": { "value": "9999px", "usage": "Pills, avatars" }
  },

  "shadow": {
    "none": { "value": "none", "usage": "Flat elements" },
    "sm": { "value": "0 1px 2px rgba(0,0,0,0.05)", "usage": "Subtle elevation" },
    "md": { "value": "0 4px 6px rgba(0,0,0,0.1)", "usage": "Cards" },
    "lg": { "value": "0 10px 15px rgba(0,0,0,0.1)", "usage": "Dropdowns, popovers" },
    "xl": { "value": "0 20px 25px rgba(0,0,0,0.15)", "usage": "Modals" }
  },

  "motion": {
    "duration": {
      "instant": { "value": "0ms", "usage": "No animation" },
      "fast": { "value": "150ms", "usage": "Micro-interactions" },
      "normal": { "value": "250ms", "usage": "Default transitions" },
      "slow": { "value": "400ms", "usage": "Page transitions" }
    },
    "easing": {
      "default": { "value": "cubic-bezier(0.4, 0, 0.2, 1)", "usage": "General purpose" },
      "in": { "value": "cubic-bezier(0.4, 0, 1, 1)", "usage": "Enter animations" },
      "out": { "value": "cubic-bezier(0, 0, 0.2, 1)", "usage": "Exit animations" },
      "bounce": { "value": "cubic-bezier(0.68, -0.55, 0.265, 1.55)", "usage": "Playful feedback" }
    }
  },

  "contrastPairings": {
    "comment": "WCAG AA validated color combinations",
    "pairings": [
      {
        "foreground": "text.primary",
        "background": "background.default",
        "ratio": "12.5:1",
        "passes": ["normal-text", "large-text", "ui-components"]
      },
      {
        "foreground": "text.secondary",
        "background": "background.default",
        "ratio": "5.2:1",
        "passes": ["normal-text", "large-text", "ui-components"]
      },
      {
        "foreground": "text.inverse",
        "background": "primary",
        "ratio": "7.1:1",
        "passes": ["normal-text", "large-text", "ui-components"]
      }
    ]
  }
}
```

---

## Step 3b: Create Design Guideline

### Purpose
Create a comprehensive design guideline based on design tokens and stress-test preview results. This step bridges the gap between conceptual intent and concrete implementation by defining how tokens should be used, incorporating token gaps discovered during stress-testing.

### Command
```
Based on these inputs:
- Design tokens from Step 2: [PASTE JSON]
- Stress-Test Preview results from Step 3: [PASTE TOKEN GAPS DISCOVERED]

Create a comprehensive Design Guideline document following this structure:

# Design Style: [Style Name]

## Design Philosophy
- Core Principle: Define the fundamental design approach
- Emotional Target: What feelings should the design evoke?
- The Guiding Question: What question validates design decisions?

## Design Token System (The DNA)

### Color Palette
- Base Colors
- The Five Accent Colors (always have 5 distinct accents)
- Color Usage Rules: Section rotation, repeated elements, contrast ratios

### Typography System
- Font Stack: Headings, body, display fonts
- Type Scale: Aggressive sizing
- Type Styling Patterns: Weight distribution, letter spacing, line height
- Text Shadow System: Offset patterns, gradient text

### Border & Radius System
- Border Widths
- Border Styles: Solid, dashed, dotted, double
- Border Radius Values
- Border Color Strategy

### Shadow & Glow System
- Glow Shadows: Colored, soft, luminous
- Hard Shadows: Offset, flat, stacked
- Shadow Mixing: Combine glow + hard shadows

### Texture & Pattern System (MANDATORY Layering)
- Pattern Types: Dot grid, diagonal stripes, checkerboard, gradient mesh
- Pattern Layering Strategy: Global base + section-specific

## Component Styling Principles
- Buttons
- Inputs & Forms
- Cards & Containers
- Navigation Elements
- Feedback Components

## Anti-Patterns (What to Avoid)
- List of design patterns that contradict the style

## Accessibility & Best Practices
- Contrast requirements
- Reduced motion considerations
- Screen reader support

## Layout & Spacing Rhythm
- Spacing scale
- Layout patterns
- Responsive behavior

## Iconography Guidelines
- Style approach
- Usage rules

## Implementation Notes
- Practical advice for developers
- Common pitfalls

## Additional Checklist Coverage
- A. Emotions to Avoid
- C. Behavior Alignment
- D. Boundary / Anti-pattern Awareness
- E. Fidelity Under Pressure
- F. Language Consistency

## Integration Notes
How this guideline ensures the design system passes Concept Understanding Checklist

Requirements:
- This document becomes the single source of truth for all design decisions
- Design tokens from Step 2 must align with this guideline
- All components in Step 4-5 must follow these principles
- Include specific values (px, hex codes, named tokens)
- Add "FINAL REMINDER" summarizing the design philosophy
```

### Output Format
```markdown
# Design Style: [Style Name]

## Design Philosophy

**Core Principle**: [One sentence defining the fundamental approach]

**Emotional Target**: [What the design should make users feel]

**The Guiding Question**: "[Question that validates design decisions]"

---

## Design Token System (The DNA)

### Color Palette ([Mode] Foundation)

**Base Colors**:
- Primary: #hexcode
- Secondary: #hexcode
- Background: #hexcode
- Text: #hexcode

**The Five Accent Colors** (This is critical - always have 5 distinct accents):
- Accent 1: #hexcode - [Usage]
- Accent 2: #hexcode - [Usage]
- Accent 3: #hexcode - [Usage]
- Accent 4: #hexcode - [Usage]
- Accent 5: #hexcode - [Usage]

**Color Usage Rules**:
- **Section Rotation**: Each major section cycles through the 5 accents as its primary color. Use modulo arithmetic (index % 5) to rotate systematically.
- **Repeated Elements**: In grids (stats, features, testimonials), rotate accent colors using the same modulo approach.
- **Contrast Ratios**: Despite chaos, maintain text-to-background contrast ratios that meet WCAG AA (4.5:1 for normal text).
- **Accent Text**: Only use accent colors for decorative text, labels, or non-critical content. Never body text.

### Typography System

**Font Stack**:
- **Headings**: [Font name] (bold, geometric, 700-900 weight)
- **Body**: [Font name] (clean, readable, 400-700 weight)
- **Display/Accent**: [Font name] (special use, for callouts)

**Type Scale** (Aggressive sizing):
- Text-xs: 12px - [Usage]
- Text-sm: 14px - [Usage]
- Text-base: 16px - [Usage]
- Text-lg: 18px - [Usage]
- Text-xl: 20px - [Usage]
- Text-2xl: 24px - [Usage]
- Text-3xl: 30px - [Usage]
- Text-4xl: 36px - [Usage]
- Text-5xl: 48px - [Usage]

**Type Styling Patterns**:
- **Weight Distribution**: Headlines = 800-900 weight, body = 400-500, labels = 700 bold
- **Letter Spacing**: Headlines get `tracking-tight` or `tracking-tighter`, labels get `tracking-widest`, body stays normal
- **Line Height**: Headlines = leading-none or leading-tight (0.9-1.1), body = leading-relaxed (1.625)
- **Text Transform**: Uppercase for headlines, labels, and buttons. Normal case for body text.

**Text Shadow System** (CRITICAL - Always Use):
- Pattern: 2px increments in offset, rotate through accent colors
- Headlines get triple or mega stack
- Subheadings get double shadow
- Card titles get single or double shadow

**Gradient Text**:
- Use on 20-30% of headlines for variety
- Pattern: `background: linear-gradient(90deg, #accent1, #accent2, #accent3, #accent1)`
- Make background-size 200-300% and animate with gradient shift
- Apply with `background-clip: text` and `-webkit-text-fill-color: transparent`

### Border & Radius System

**Border Widths** (Go bold):
- Border-1: 1px - [Usage]
- Border-2: 2px - [Usage]
- Border-4: 4px - [Usage]

**Border Styles** (Mix deliberately):
- **Solid**: Default for most containers and cards
- **Dashed**: Use on 30% of borders for variety (`border-dashed`)
- **Dotted**: Rare, for small decorative elements
- **Double**: Occasional use for special containers (`border-double`)
- **Critical Rule**: Within a single section, use 2-3 different border styles intentionally

**Border Radius Values**:
- Radius-none: 0px - [Usage]
- Radius-sm: 4px - [Usage]
- Radius-md: 8px - [Usage]
- Radius-lg: 16px - [Usage]
- Radius-full: 9999px - [Usage]

**Border Color Strategy**:
- Primary: Accent color that clashes with background
- Never: Neutral or muted borders
- Technique: If background uses accent-1, border uses accent-2 or accent-3

### Shadow & Glow System (Multi-Layered)

**Glow Shadows** (Colored, soft, luminous):
- Pattern: `0 0 [spread]px rgba([r,g,b], [opacity])`
- Use on: Buttons, icons, featured elements
- Hover: Increase opacity by 0.1-0.2 and spread by 50%
- Combine 2-3 colors for richer glow

**Hard Shadows** (Offset, flat, stacked):
- Pattern: Each layer doubles the offset (8→16→24 or 12→24→36)
- Colors: Rotate through different accents per layer
- Use on: Cards, containers, prominent buttons
- Hover: Increase offsets by 2-4px to simulate lift

**Shadow Mixing**:
- Combine glow + hard shadows on hero elements
- Example: `box-shadow: 0 0 30px rgba(255,58,242,0.6), 8px 8px 0 #FFE600, 16px 16px 0 #FF3AF2`

### Texture & Pattern System (MANDATORY Layering)

**Pattern Types** (Always layer 2-3 minimum):

1. **Dot Grid**:
   - Implementation: `radial-gradient(circle, [accent] 1px, transparent 1px)`
   - Vary dot size (1px-2px) and spacing (20px-40px)
   - Use different accent colors per section

2. **Diagonal Stripes**:
   - Implementation: `repeating-linear-gradient([angle], transparent, transparent [width], [accent] [width+2px])`
   - Keep opacity low (0.05-0.1) to avoid overwhelming
   - Vary stripe width (10-20px) and angle (30deg-60deg)

3. **Checkerboard**:
   - Implementation: Conic gradient with 4 alternating colors
   - Use subtle opacity (0.03-0.07)
   - Vary grid size (30px-50px)

4. **Gradient Mesh** (Radial overlaps):
   - Implementation: Multiple radial gradients at different positions
   - Place ellipses at different positions
   - Use 2-4 overlapping gradients
   - Keep opacity low (0.1-0.2)

**Pattern Layering Strategy**:
- **Global Base**: 2 fixed patterns on entire page (dots + stripes)
- **Section Specific**: Each major section adds 1-2 unique patterns
- **Implementation**: Use pseudo-elements (::before, ::after) with `pointer-events: none`
- **Blend Modes**: Apply `mix-blend-mode: overlay` or `screen` on some layers for deeper integration
- **Opacity Range**: 0.05-0.3 per pattern (multiply for stacking)

---

## Component Styling Principles

### Buttons
- **Primary**: Gradient background with glow shadow, uppercase text
- **Secondary**: Border-heavy style with hard shadow
- **States**: Hover increases shadow spread and glow opacity
- **Icons**: Include accent-colored icons in 40% of buttons

### Inputs & Forms
- **Background**: Darker than page background (#0D0D1A → #151525)
- **Border**: 2-4px solid using current section's accent color
- **Focus**: Glow shadow using input's accent color
- **Labels**: Uppercase, tracking-widest, with text shadow

### Cards & Containers
- **Layering**: Minimum 3 visual layers (border + shadow + pattern)
- **Borders**: Mix solid (60%), dashed (30%), double (10%)
- **Shadows**: Stacked hard shadows + soft glow on hover
- **Titles**: Text shadow using card's accent color

### Navigation Elements
- **Active State**: Full accent color background with glow
- **Inactive State**: Border-only style
- **Hover**: Transition between states with shadow expansion

### Feedback Components
- **Success**: Green/yellow gradient with celebratory pattern
- **Error**: Pink/red with high-contrast border
- **Warning**: Orange/yellow with dashed border
- **Info**: Cyan/blue with dot grid pattern

---

## Anti-Patterns (What to Avoid)

- [ ] Empty whitespace without patterns
- [ ] Single-color backgrounds without texture
- [ ] Muted or desaturated accents
- [ ] Matching border and background colors
- [ ] Minimal shadows or no glow effects
- [ ] Standard border styles only (mix it up)
- [ ] Regular line height on headlines
- [ ] Lowercase headlines
- [ ] No texture layering (patterns are mandatory)

---

## Accessibility & Best Practices

### Contrast Requirements
- Body text on backgrounds: Minimum 4.5:1 (WCAG AA)
- Large text (18px+): Minimum 3:1 (WCAG AA)
- Decorative accents: Can be lower contrast (2:1 acceptable)
- Test all accent combinations against background

### Reduced Motion
- Respect `prefers-reduced-motion` media query
- Replace animations with static states when detected
- Keep critical functionality accessible without motion

### Screen Reader Support
- Decorative patterns: `aria-hidden="true"` or role="presentation"
- Icons: Include `aria-label` on icon-only buttons
- Color-only information: Provide text alternative

---

## Layout & Spacing Rhythm

### Spacing Scale
- spacing-xs: 4px - Tight gaps, icon spacing
- spacing-sm: 8px - Small gaps, inline spacing
- spacing-md: 16px - Default component padding
- spacing-lg: 24px - Section spacing
- spacing-xl: 32px - Large section gaps
- spacing-2xl: 48px - Page-level spacing

### Layout Patterns
- **Grid**: Use accent rotation for different grid items
- **Sections**: Each section gets unique accent color
- **Overlapping**: Allow some elements to overlap with layering (z-index)
- **Container Patterns**: Add texture to all major containers

### Responsive Behavior
- Mobile: Reduce pattern complexity (2 layers max)
- Tablet: Maintain 2-3 pattern layers
- Desktop: Full maximalist treatment (3-4 pattern layers)

---

## Iconography Guidelines

### Style Approach
- **Line Style**: Bold outlines (2px-3px stroke width)
- **Fill**: Use solid fills for 60% of icons, outlined for 40%
- **Color**: Use section's accent color
- **Size**: Scale aggressively (16px → 24px → 32px → 48px)

### Usage Rules
- **Decorative Icons**: Use on 50% of cards/sections
- **Action Icons**: Add glow shadow on hover
- **Spacing**: Generous spacing around icons (16px+)

---

## Implementation Notes

### Developer Checklist
- [ ] Check contrast ratios for all accent combinations
- [ ] Apply text shadows to all headings
- [ ] Layer at least 2-3 patterns per section
- [ ] Mix border styles (not all solid)
- [ ] Use stacked shadows on cards
- [ ] Rotate accent colors systematically
- [ ] Test with reduced motion enabled
- [ ] Verify keyboard focus states have visual indicators

### Common Pitfalls
1. **Too much contrast on small text**: Use lighter accent colors for decorative labels
2. **Pattern overwhelming content**: Keep pattern opacity below 0.3
3. **All borders solid**: Mix in dashed/dotted for variety
4. **Shadows too subtle**: Increase opacity and spread for glow effects
5. **No texture layering**: Every major container needs at least 1 pattern
6. **Forgetting text shadows**: Headlines need 2-3 layered shadows

### CSS Code Snippets

**Text Shadow Pattern**:
```css
.text-shadow-maximalist {
  text-shadow:
    2px 2px 0 #accent1,
    4px 4px 0 #accent2,
    6px 6px 0 #accent3;
}
```

**Pattern Layering**:
```css
.patterns-layered::before {
  content: '';
  position: absolute;
  inset: 0;
  background-image:
    radial-gradient(circle at 20% 30%, #accent1 1px, transparent 1px),
    repeating-linear-gradient(45deg, transparent, transparent 15px, #accent2 15px, #accent2 17px);
  background-size: 40px 40px, 100% 100%;
  opacity: 0.15;
  pointer-events: none;
  mix-blend-mode: overlay;
}
```

**Glow Shadow**:
```css
.glow-accent {
  box-shadow:
    0 0 20px rgba(255, 58, 242, 0.5),
    0 0 40px rgba(255, 58, 242, 0.3),
    0 0 60px rgba(255, 58, 242, 0.1);
}
```

---

# Additional Checklist Coverage

### A. Emotions to Avoid
- Avoid inducing **anxiety**, **guilt**, or **shame**.
- Prevent feelings of **surveillance** or being overly monitored.
- Do not create competitive stress or urgency.

### C. Behavior Alignment
- Visual chaos is designed to **increase joy and playful exploration**, encouraging users to linger and interact.
- Dense layering reduces monotony and keeps attention engaged.
- Bright contrasts and motion reduce disengagement and boredom.
- The abundance of visual stimuli is meant to **stimulate dopamine release**, reinforcing positive engagement rather than compliance.

### D. Boundary / Anti-pattern Awareness
- **Anti-goals**: Surveillance, guilt-tripping, competition escalation.
- **Risks if misapplied**:
  1. Overwhelming users into anxiety instead of joy.
  2. Turning playful chaos into manipulative dark patterns (e.g., forced urgency, gamified ranking).
  3. Breaking accessibility by ignoring reduced-motion or contrast needs.
- Explicitly avoid: leaderboards, urgent notifications, guilt-based nudges.

### E. Fidelity Under Pressure
- If PM requests conflicting features (e.g., leaderboard, urgency banners):
  - **Reject** escalation that contradicts mood.
  - Offer softer alternatives: playful decorative badges, celebratory animations, or ambient engagement cues.
  - Preserve core principle: joy through abundance, not pressure.

### F. Language Consistency
- Language remains playful, descriptive, and energetic.
- Avoid coercive or judgmental terms.
- Maintain tone consistent with maximalism.

---

## Integration Notes
These additions ensure that design system passes the **Concept Understanding Checklist** fully, covering emotional boundaries, behavioral alignment, anti-pattern awareness, and fidelity under pressure. The augmented system now explicitly defines what emotions to avoid, how visuals tie to user behavior, which anti-goals to guard against, and how to resist conflicting product demands while preserving the design philosophy.

---

**Final Reminder**: [Summarize the design philosophy in one powerful sentence that designers and developers should keep in mind]

**Design Guideline Version:** 1.0
**Created:** 2026-01-11
```

---

## Step 3: Stress-Test Preview (Visual Validation)

### Purpose
Create an HTML preview implementing your app screenshot using the design tokens from Step 2. This validates the look & feel of your specific app before building the actual implementation.

### Command
```
Based on these inputs:
- Design tokens from Step 2: [PASTE JSON]
- Your app screenshot: [ATTACH IMAGE or DESCRIBE LAYOUT]

Create an HTML preview of your app's screen using the design tokens.

Requirements:
- Replicate the layout shown in your screenshot as closely as possible
- Apply ALL design tokens from Step 2 (colors, typography, spacing, shadows, borders)
- Match the structure and components visible in the screenshot
- Include realistic content (labels, buttons, inputs, cards, etc.)
- Single HTML file with inline CSS
- Desktop or mobile viewport (match what you intend to build)
- No external dependencies (self-contained)
- Add HTML comments marking each component/section

CRITICAL - Token Enforcement:
- ONLY use CSS Variables defined in the :root block from Step 2 tokens
- DO NOT use hardcoded hex codes, pixel values, or any raw values in component styles
- Every color must reference var(--color-*)
- Every spacing must reference var(--spacing-*)
- Every font property must reference var(--font-*)
- Every radius must reference var(--radius-*)
- Every shadow must reference var(--shadow-*)
- Every transition must reference var(--duration-*) and var(--easing-*)

TOKEN GAP DISCOVERY:
- If tokens feel insufficient for the complexity in your screenshot, flag missing tokens
- Common gaps: 'surface-sunken', 'text-muted', 'border-subtle', 'spacing-2xs', 'shadow-glow'
- List all gaps at the end of the file for Step 2 revision

Output:
1. Complete HTML file ready to open in browser
2. List of "TOKEN GAPS" discovered during implementation
3. Notes on any visual elements from screenshot that need new components
```

### Output Format
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[App Screen Name] Preview</title>
  <style>
    /* ========================================
       DESIGN TOKENS (from Step 2)
       ======================================== */
    :root {
      /* Colors */
      --color-primary: #hexcode;
      --color-secondary: #hexcode;
      --color-background: #hexcode;
      --color-text-primary: #hexcode;
      --color-text-secondary: #hexcode;
      
      /* Spacing */
      --spacing-xs: 4px;
      --spacing-sm: 8px;
      --spacing-md: 16px;
      --spacing-lg: 24px;
      --spacing-xl: 32px;
      
      /* Typography */
      --font-family: 'Inter', sans-serif;
      --font-size-base: 16px;
      --font-size-lg: 18px;
      --font-size-2xl: 24px;
      --font-weight-normal: 400;
      --font-weight-semibold: 600;
      --line-height: 1.5;
      
      /* Radius */
      --radius-md: 8px;
      --radius-lg: 12px;
      --radius-full: 9999px;
      
      /* Shadow */
      --shadow-md: 0 4px 6px rgba(0,0,0,0.1);
      --shadow-lg: 0 10px 15px rgba(0,0,0,0.1);
      
      /* Motion */
      --duration-normal: 250ms;
      --easing-default: cubic-bezier(0.4, 0, 0.2, 1);
    }

    /* ========================================
       BASE STYLES
       ======================================== */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: var(--font-family);
      font-size: var(--font-size-base);
      line-height: var(--line-height);
      color: var(--color-text-primary);
      background: var(--color-background);
      min-height: 100vh;
    }

    /* ========================================
       COMPONENT STYLES
       ======================================== */
    /* Your app-specific component styles here */
    /* Match the layout from your screenshot */
  </style>
</head>
<body>
  <!-- ========================================
       APP SCREEN: [Screen Name]
       ======================================== -->
  
  <!-- Section: [Name] -->
  <div class="component-name">
    <!-- Content matching your screenshot -->
  </div>

  <!-- ========================================
       TOKEN GAPS DISCOVERED
       ======================================== -->
  <!--
  The following tokens were needed but missing from the foundation:
  
  1. --color-surface-sunken: Needed for inset areas
  2. --color-text-muted: Needed for de-emphasized text
  3. --shadow-glow: Needed for button hover states
  
  ACTION: Return to Step 2 and add these tokens before proceeding.
  -->
  
  <!-- ========================================
       NEW COMPONENTS NEEDED
       ======================================== -->
  <!--
  Visual elements from screenshot that require new components:
  
  1. [Component]: [Description of what was in screenshot]
  2. [Component]: [Description]
  
  ACTION: These will be added to Component Specs in Step 4.
  -->

</body>
</html>
```

## Step 4: Extract Components (Functional Groups + Schema-First)

### Purpose
Identify reusable components and define their specifications using TypeScript interfaces as the source of truth.

### Command
```
Analyze this HTML screen:
[PASTE HTML FROM STEP 3]

Extract all reusable components and organize them into FUNCTIONAL GROUPS
based on the job they do for the user:

Functional Groups:
- Actions: Components that trigger events (Button, IconButton, Link, MenuItem)
- Data Entry: Components for user input (Input, Textarea, DatePicker)
- Selection: Components for choosing options (Checkbox, Radio, Switch, Select, Combobox)
- Feedback: Components that communicate status (Toast, Modal, Alert, Progress, Spinner)
- Display: Components that present information (Card, Badge, Avatar, Tooltip, DataTable)
- Navigation: Components for wayfinding (Tabs, Breadcrumbs, Sidebar, Pagination)
- Layout: Components that structure content (Stack, Grid, Container, Divider)

For each component, provide:
1. Component name (PascalCase)
2. Functional Group assignment
3. Purpose (one sentence)
4. TypeScript Interface (THIS IS THE PRIMARY OUTPUT - defines the component contract)
5. States (default, hover, focus, disabled, loading)
6. Accessibility requirements
7. Usage examples

CRITICAL - Schema-First Approach:
- Define the component's props as a TypeScript interface FIRST
- This interface becomes the "contract" that Step 4b, Step 5, and Step 6 must follow
- Use strict typing (avoid 'any', prefer union types for variants)
- Include JSDoc comments for each prop
- Export interfaces grouped by functional category

Output format: TypeScript interfaces (grouped) + component specification document.
```

### Output Format
```typescript
// types/components.ts - Organized by Functional Group

// ============================================
// GROUP: ACTIONS
// Components that trigger events or navigate
// ============================================

/**
 * Button component props
 * @group Actions
 */
export interface ButtonProps {
  /** Visual style variant */
  variant?: 'primary' | 'secondary' | 'ghost' | 'danger';
  /** Button size - affects height and padding */
  size?: 'sm' | 'md' | 'lg';
  /** Disables the button and prevents interaction */
  disabled?: boolean;
  /** Shows loading spinner and disables interaction */
  loading?: boolean;
  /** Makes button fill container width */
  fullWidth?: boolean;
  /** Icon displayed before the label */
  leftIcon?: React.ReactNode;
  /** Icon displayed after the label */
  rightIcon?: React.ReactNode;
  /** Button content */
  children: React.ReactNode;
  /** Click handler */
  onClick?: (event: React.MouseEvent<HTMLButtonElement>) => void;
}

/**
 * IconButton component props
 * @group Actions
 */
export interface IconButtonProps {
  /** The icon to display */
  icon: React.ReactNode;
  /** Accessible label (required for screen readers) */
  'aria-label': string;
  /** Visual style variant */
  variant?: 'primary' | 'secondary' | 'ghost';
  /** Button size */
  size?: 'sm' | 'md' | 'lg';
  /** Disables the button */
  disabled?: boolean;
  /** Click handler */
  onClick?: (event: React.MouseEvent<HTMLButtonElement>) => void;
}

// ============================================
// GROUP: SELECTION
// Components for choosing from options
// ============================================

/**
 * Checkbox component props
 * @group Selection
 */
export interface CheckboxProps {
  /** Whether the checkbox is checked */
  checked?: boolean;
  /** Indeterminate state (for "select all" patterns) */
  indeterminate?: boolean;
  /** Label text */
  label?: string;
  /** Disables the checkbox */
  disabled?: boolean;
  /** Change handler */
  onChange?: (checked: boolean) => void;
}

// ============================================
// GROUP: LAYOUT
// Components that structure content
// ============================================

/**
 * Stack layout component props
 * @group Layout
 */
export interface StackProps {
  /** Direction of the stack */
  direction?: 'vertical' | 'horizontal';
  /** Spacing between children (uses design tokens) */
  spacing?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
  /** Alignment of children on cross axis */
  align?: 'start' | 'center' | 'end' | 'stretch';
  /** Alignment of children on main axis */
  justify?: 'start' | 'center' | 'end' | 'between' | 'around';
  /** Stack content */
  children: React.ReactNode;
}

// ... additional component interfaces per group
```

```markdown
# Component Specifications (Functional Groups)

## Group: Actions
*Components that trigger events or navigate*

### Button
**Purpose:** Primary interaction element for user actions.
**TypeScript Interface:** `ButtonProps`

**Variants:**
| Variant | Use Case |
|---------|----------|
| primary | Main CTA, important actions |
| secondary | Supporting actions |
| ghost | Tertiary actions, subtle |
| danger | Destructive actions |

**Sizes:** sm (32px), md (40px), lg (48px)

**States:** default, hover, focus, active, disabled, loading

**Accessibility:**
- Minimum touch target: 44x44px
- Focus visible for keyboard navigation
- aria-disabled when disabled
- aria-busy when loading

---

### IconButton
**Purpose:** Compact action button using only an icon.
**TypeScript Interface:** `IconButtonProps`

**Usage:** Toolbars, table row actions, constrained spaces

---

## Group: Selection
*Components for choosing from options*

### Checkbox
**Purpose:** Toggle a single boolean or select multiple items.
**TypeScript Interface:** `CheckboxProps`

---

## Group: Feedback
*Components that communicate status to users*

### Toast
**Purpose:** Non-blocking notifications that auto-dismiss.

### Modal
**Purpose:** Blocking dialogs requiring user acknowledgment.

### InlineAlert
**Purpose:** Contextual feedback tied to specific content.

---

## Group: Layout
*Components that structure content*

### Stack
**Purpose:** Arrange children with consistent spacing.
**TypeScript Interface:** `StackProps`

---

[Continue for all groups...]
```

---

## Step 4b: Component Decision Trees

### Purpose
Create IF/THEN decision logic to help developers choose the right component for their use case.

### Command
```
Based on the Functional Groups from Step 4, create decision trees
for each group in "If/Then" format.

For each functional group:
1. List all components in the group
2. Identify the key decision factors (number of options, blocking vs non-blocking, etc.)
3. Create clear IF/THEN rules that lead to a single component choice

The decision tree should answer: "Given my use case, which component should I use?"

Output format: Decision tree document with all functional groups covered.
```

### Output Format
```markdown
# Component Decision Trees

Use these trees to select the right component for your use case.

---

## Actions Group

**Choosing between Button, IconButton, Link, MenuItem**

- If action navigates to a new page → use **Link**
- If action is in a menu/dropdown context → use **MenuItem**
- If action is in a constrained space (toolbar, table row) → use **IconButton**
- If action is a primary CTA on the page → use **Button (primary)**
- If action is secondary/supporting → use **Button (secondary)**
- If action is low-emphasis/tertiary → use **Button (ghost)**
- If action is destructive → use **Button (danger)** with confirmation

---

## Selection Group

**Choosing between Checkbox, Radio, Switch, Select, Combobox**

- If toggling a single on/off setting → use **Switch**
- If selecting ONE option from ≤ 4 visible choices → use **Radio**
- If selecting ONE option from 5-10 items → use **Select**
- If selecting ONE option from > 10 items (needs search) → use **Combobox**
- If selecting MULTIPLE options from ≤ 6 items → use **Checkbox Group**
- If selecting MULTIPLE options from > 6 items → use **Multi-Select Combobox**
- If the selection has immediate effect (no submit) → prefer **Switch** or **SegmentedControl**

---

## Feedback Group

**Choosing between Toast, Modal, InlineAlert, Progress, Spinner, Skeleton**

- If feedback is non-blocking and auto-dismisses → use **Toast**
- If feedback requires user acknowledgment/decision → use **Modal**
- If feedback is contextual to a specific field or section → use **InlineAlert**
- If showing progress of a known-duration task → use **Progress Bar**
- If showing progress of an unknown-duration task → use **Spinner**
- If content is loading and you want to preserve layout → use **Skeleton**
- If the entire page/section is loading → use **Spinner** (centered)

---

## Display Group

**Choosing between Card, Badge, Avatar, Tooltip, Tag, DataTable**

- If displaying a single entity with actions → use **Card**
- If showing a small status indicator → use **Badge**
- If representing a user/entity visually → use **Avatar**
- If providing supplementary info on hover → use **Tooltip**
- If categorizing or labeling content → use **Tag**
- If displaying structured data with sorting/filtering → use **DataTable**

---

## Navigation Group

**Choosing between Tabs, Breadcrumbs, Sidebar, Pagination, Menu**

- If switching between views in the same context → use **Tabs**
- If showing hierarchy/path in deep navigation → use **Breadcrumbs**
- If providing persistent app-level navigation → use **Sidebar**
- If navigating through paginated data → use **Pagination**
- If providing contextual actions (right-click, dropdown) → use **Menu**

---

## Layout Group

**Choosing between Stack, Grid, Container, Divider, Spacer**

- If arranging items in a single direction with gaps → use **Stack**
- If arranging items in a 2D grid pattern → use **Grid**
- If centering content with max-width → use **Container**
- If visually separating sections → use **Divider**
- If adding flexible space between items → use **Spacer**
```

---

## Step 5: Create Storybook Setup

### Purpose
Generate a working Storybook with all components documented.

### Command
```
Based on these inputs:
- Component specifications and TypeScript interfaces from Step 4
- Decision Trees from Step 4b

Generate a Storybook setup with:

1. Project structure organized by FUNCTIONAL GROUPS (not alphabetically)
2. Storybook configuration (.storybook/main.ts, preview.ts)
3. Design tokens as CSS/JS (importable)
4. Story files for each component
5. Decision Tree documentation pages (MDX)

Requirements:
- Use Storybook 7+ with Vite
- Include Controls addon for props
- Include Accessibility addon
- Storybook sidebar MUST mirror functional groups: Actions, Selection, Feedback, etc.
- Include Decision Tree docs for each group
- Add design token documentation page

CRITICAL - Interface Compliance:
- Import and use the TypeScript interfaces from Step 4 (types/components.ts)
- Component implementations MUST match the interface contracts exactly
- Story controls should be auto-generated from the interface types
- Use satisfies operator to ensure type safety: `const meta = { ... } satisfies Meta<typeof Button>`

CRITICAL - Folder Structure:
- Components organized by functional group, NOT by type (primitive/pattern/layout)
- This ensures the codebase matches the design system logic

Output: File-by-file code for complete Storybook setup.
```

### Output Format
```
design-system/
├── .storybook/
│   ├── main.ts
│   ├── preview.ts
│   └── theme.ts
├── src/
│   ├── tokens/
│   │   ├── tokens.json
│   │   ├── tokens.css
│   │   └── index.ts
│   ├── types/
│   │   └── components.ts          # All TypeScript interfaces (grouped)
│   ├── components/
│   │   ├── actions/               # Button, IconButton, Link, MenuItem
│   │   │   ├── Button/
│   │   │   │   ├── Button.tsx
│   │   │   │   ├── Button.stories.tsx
│   │   │   │   ├── Button.module.css
│   │   │   │   └── index.ts
│   │   │   ├── IconButton/
│   │   │   └── Link/
│   │   ├── selection/             # Checkbox, Radio, Switch, Select, Combobox
│   │   │   ├── Checkbox/
│   │   │   ├── Radio/
│   │   │   └── Select/
│   │   ├── feedback/              # Toast, Modal, Alert, Progress, Spinner
│   │   │   ├── Toast/
│   │   │   ├── Modal/
│   │   │   └── InlineAlert/
│   │   ├── display/               # Card, Badge, Avatar, Tooltip, DataTable
│   │   │   ├── Card/
│   │   │   └── Badge/
│   │   ├── navigation/            # Tabs, Breadcrumbs, Sidebar, Pagination
│   │   │   ├── Tabs/
│   │   │   └── Breadcrumbs/
│   │   └── layout/                # Stack, Grid, Container, Divider
│   │       ├── Stack/
│   │       ├── Grid/
│   │       └── Container/
│   └── index.ts                   # Barrel export all components
├── docs/
│   ├── Introduction.mdx
│   ├── DesignTokens.mdx
│   ├── DecisionTrees.mdx          # Component selection guide
│   └── Guidelines.mdx
├── package.json
└── tsconfig.json
```

**Storybook Sidebar Structure:**
```
├── Docs
│   ├── Introduction
│   ├── Design Tokens
│   ├── Decision Trees
│   └── Guidelines
├── Actions
│   ├── Button
│   ├── IconButton
│   └── Link
├── Selection
│   ├── Checkbox
│   ├── Radio
│   └── Select
├── Feedback
│   ├── Toast
│   ├── Modal
│   └── InlineAlert
├── Display
│   ├── Card
│   └── Badge
├── Navigation
│   ├── Tabs
│   └── Breadcrumbs
└── Layout
    ├── Stack
    └── Grid
```

---

## Step 6: Build App Screens

### Purpose
Use the design system to build actual application screens.

### Command
```
Using this design system:
[REFERENCE STORYBOOK FROM STEP 5]

Build the following screen:
[DESCRIBE SCREEN AND USER FLOW]

Requirements:
- Import components from design system (no custom styles)
- Follow component usage guidelines
- Maintain accessibility standards
- Include responsive breakpoints
- Add realistic content/data
- Include loading and error states

Output:
1. Screen component code
2. List of design system components used
3. Any new components needed (flag for design system addition)
```

### Output Format
```tsx
// screens/OnboardingWelcome.tsx

import {
  Container,
  Stack,
  Heading,
  Text,
  Button,
  Image
} from '@/design-system';

export function OnboardingWelcome({ onGetStarted }: Props) {
  return (
    <Container maxWidth="sm" padding="xl">
      <Stack spacing="lg" align="center">
        <Image src="/logo.svg" alt="App Logo" size="lg" />
        <Stack spacing="sm" align="center">
          <Heading level={1} align="center">
            Welcome to AppName
          </Heading>
          <Text variant="secondary" align="center">
            Your journey to better health starts here
          </Text>
        </Stack>
        <Button
          variant="primary"
          size="lg"
          fullWidth
          onClick={onGetStarted}
        >
          Get Started
        </Button>
      </Stack>
    </Container>
  );
}

/*
Components Used:
- Container (layout)
- Stack (layout)
- Heading (primitive)
- Text (primitive)
- Button (primitive)
- Image (primitive)

New Components Needed:
- None
*/
```

---

## Quick Reference: Full Workflow Commands

| Step | Short Command |
|------|---------------|
| 1 | "Extract concept from this moodboard: [link]" |
| 2 | "Generate design tokens JSON with WCAG contrast validation" |
| 3 | "Create stress-test dashboard preview using these tokens" |
| 3b | "Create comprehensive design guideline from tokens and stress-test results" |
| 4 | "Extract components into functional groups with TypeScript interfaces" |
| 4b | "Create decision trees for each functional group" |
| 5 | "Generate Storybook with functional folder structure" |
| 6 | "Build [screen] using the design system" |

---

## Iteration Prompts

### Refine Tokens
```
The [color/spacing/typography] doesn't feel right.
Current: [value]
Problem: [too bright/too tight/too formal]
Adjust to be more [description].
```

### Add Component Variant
```
Add a new variant to [Component]:
- Name: [variant name]
- Use case: [when to use]
- Visual difference: [how it differs]
Update the component spec and Storybook story.
```

### Validate Against Moodboard
```
Compare this implementation:
[PASTE SCREENSHOT OR HTML]

Against the original moodboard intent:
[PASTE CONCEPT FROM STEP 1]

Does it match? List any deviations and suggest fixes.
```

---

**Workflow Version:** 1.4
**Created:** 2025-01-08
**Updated:** 2026-01-11

## Changelog

### v1.4 (2026-01-11)
- **Workflow:** Moved Design Guideline step from 2b to 3b (after Stress-Test Preview)
- **Rationale:** Design guideline should incorporate token gaps discovered during stress-testing
- **Step 3b:** Updated to take both tokens and stress-test results as inputs
- Updated workflow overview and quick reference to reflect new step order

### v1.5 (2026-01-11)
- **Step 3:** Redesigned to take user app screenshot as input instead of generic dashboard
- **Rationale:** Validate look & feel of user's specific app before implementation
- **New Command:** Implement provided screenshot using design tokens, discover token gaps and identify new components needed
- **New Output:** HTML preview matching user's app + list of token gaps + new component requirements
- Updated purpose to reflect visual validation workflow

### v1.3 (2026-01-11)
- **Workflow:** Added Step 2b (Create Design Guideline) between Design Tokens and Stress-Test Preview
- **Step 2b (NEW):** Comprehensive design guideline generation with full token system, component styling principles, anti-patterns, accessibility requirements, and implementation notes
- Updated workflow overview to include step 2b in the pipeline

### v1.2 (2026-01-08)
- **Workflow:** Added Decision Trees step (4b) between Components and Storybook
- **Step 3:** Changed to "Stress-Test Preview" with high-density dashboard requirement
- **Step 4:** Reorganized components into Functional Groups (Actions, Selection, Feedback, Display, Navigation, Layout)
- **Step 4b (NEW):** Added Decision Trees with IF/THEN component selection logic for each group
- **Step 5:** Updated folder structure to match functional groupings; Storybook sidebar mirrors groups

### v1.1 (2026-01-08)
- **Step 2:** Added WCAG AA contrast validation requirements and `contrastPairings` output section
- **Step 3:** Added strict token enforcement rules - no hardcoded values allowed in component styles
- **Step 4:** Changed to Schema-First approach using TypeScript interfaces as the source of truth
- **Step 5:** Added interface compliance requirements to ensure Storybook matches Step 4 contracts
