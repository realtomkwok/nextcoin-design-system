# NextCoin Design System

A comprehensive design token system built for NextCoin's brand identity, optimised for Tailwind CSS v4 and shadcn/ui
components.

_For the convenience and consistency of development, variable names should be in American English, e.g. `color`._

## Overview

This design system uses a three-tier token architecture that separates brand foundations from semantic UI applications,
ensuring consistency across all NextCoin touchpoints while maintaining flexibility for light/dark modes and future
expansion.

### Design Philosophy

-   **Intentionally Human**: Expressive colors and typography that reflect NextCoin's mission to bridge young
    professionals with meaningful opportunities
-   **Technically Precise**: Systematic color scales using OKLCH color space for perceptual uniformity and optimal
    contrast
-   **Developer-Friendly**: Direct integration with Tailwind CSS and shadcn/ui conventions

---

## Token Architecture

### Three-Tier System

```
Foundation Tokens (Primitives)
    ↓ reference
Core Tokens (Brand Roles)
    ↓ reference
Semantic Tokens (UI Application)
    ↓ export
CSS Variables (shadcn/ui + Tailwind)
```

#### 1. Foundation Tokens

**Location**: `tokens/foundation/`

Raw design values that form the basis of the system. These are pure, context-free values.

-   **colors.json**: All color palettes in hex format
    -   `base` - Monochrome scale (0, 50, 100...900, 1000)
    -   `accent` - Brand accent colors (yellow, cyan)
    -   `supporting` - Extended palette (blue, purple, pink)
    -   `functional` - Status colors (error, warning, success)
-   **typography.json**: Complete typography system including font families, sizes, weights, line heights, and letter spacing
-   **spacing.json**: 8-point grid system
-   **border-radius.json**: Border radius values
-   **effects.json**: Shadows and opacity values

**Naming Pattern**: `{category}-{variant}-{scale}`

-   `color-base-900`
-   `color-accent-yellow-300`
-   `spacing-4`
-   `font-size-lg`
-   `radius-md`

#### 2. Core Tokens

**Location**: `tokens/core/`

Brand-level semantic roles that define "what this color/style means for NextCoin."

-   **Brand Colours**: Primary, secondary, tertiary brand identities
-   **Typography Styles**: Composed heading, body, label, button styles
-   **Brand Effects**: Signature shadows, brand-specific treatments

**Naming Pattern**: `{role}.{variant}`

```text
brand.primary
brand.accent-primary
typography.heading-xl
effects.brand-shadow
```

#### 3. Semantic Tokens

**Location**: `tokens/semantic/`

UI-level tokens that map to specific interface contexts. These export directly to CSS variables for shadcn/ui.

-   **Light mode**: `semantic/light.json` → `:root` in CSS
-   **Dark mode**: `semantic/dark.json` → `.dark` in CSS

**Naming Pattern**: `{ui-role}` or `{component}-{role}`

```text
background
foreground
primary
primary-foreground
destructive
border
sidebar-accent
```

---

## Color System

### Overview

NextCoin's color system balances warm neutrals with vibrant accents to create an approachable yet professional identity.
All colors are defined with both **Hex** (for Figma) and **OKLCH** (for CSS) values, ensuring design-development
consistency.

**Key Principles:**

-   **Perceptual Uniformity**: OKLCH color space ensures equal numeric changes create equal perceived changes
-   **Contrast Consistency**: APCA-validated contrast values maintained across all hues at each scale level
-   **Dual Format**: Every color token includes both Hex and OKLCH values
-   **Systematic Progression**: Mathematical relationships between scale levels for predictable behavior

---

### Complete Color Palette Reference

#### Foundation Tokens: Monochrome (Base)

The foundation for all neutral colors, optimized for text, backgrounds, and borders.

| Scale | Token             | Hex       | OKLCH                       | Light Mode Lc\* | Dark Mode Lc\*\* | Role                                |
| ----- | ----------------- | --------- | --------------------------- | --------------- | ---------------- | ----------------------------------- |
| 0     | `color-base-0`    | `#ffffff` | `oklch(1 0 0)`              | —               | 99               | Pure white, light mode cards        |
| 50    | `color-base-50`   | `#f5f3f0` | `oklch(0.965 0.005 71.747)` | —               | 97               | Light mode page background          |
| 100   | `color-base-100`  | `#e6e4e2` | `oklch(0.92 0.003 71.802)`  | 90              | 89               | Light borders, disabled backgrounds |
| 200   | `color-base-200`  | `#cfcdcb` | `oklch(0.849 0.004 71.776)` | 77              | 76               | Medium borders, subtle emphasis     |
| 300   | `color-base-300`  | `#bbb9b7` | `oklch(0.787 0.004 71.714)` | 65              | 65               | Dark mode body text minimum         |
| 400   | `color-base-400`  | `#adaba8` | `oklch(0.742 0.005 71.685)` | 66              | 57               | Placeholder text                    |
| 500   | `color-base-500`  | `#999895` | `oklch(0.68 0.005 71.682)`  | 58              | 47               | Secondary text                      |
| 600   | `color-base-600`  | `#7b7a78` | `oklch(0.58 0.003 71.711)`  | 67              | 48               | Light mode body text minimum        |
| 700   | `color-base-700`  | `#595856` | `oklch(0.461 0.003 71.664)` | 81              | 33               | Light mode heading text             |
| 800   | `color-base-800`  | `#3e3d3c` | `oklch(0.361 0.002 71.696)` | 91              | 19               | Dark mode cards, high contrast text |
| 900   | `color-base-900`  | `#161515` | `oklch(0.198 0.002 71.641)` | 99              | 8                | Dark mode foreground, cards         |
| 1000  | `color-base-1000` | `#000000` | `oklch(0 0 0)`              | 99              | —                | Pure black, dark mode page          |

\*Light Mode Lc: Contrast against `base-50` (light mode page background)  
\*\*Dark Mode Lc: Contrast against `base-900` (dark mode card surface)

**Key Properties:**

-   Warm undertone (56-84° hue) for an approachable feel
-   Consistent lightness steps for predictable contrast
-   Perceptually uniform progression using OKLCH color space
-   Optimized for both light and dark mode applications

---

## Semantic Color Roles

This section defines how foundation tokens map to semantic UI roles in both light and dark modes, following shadcn/ui conventions and APCA contrast guidelines.

### Design Philosophy

**Monochrome-First Approach:**

-   All UI elements use the monochrome scale for consistency and professionalism
-   Accent colors (yellow, cyan, blue, purple, pink, red) are reserved exclusively for focus states and rings
-   Creates a clean, readable interface that lets content shine

**Elevated Card Pattern:**

-   Cards are always more luminous than page backgrounds
-   Light mode: White cards (`base-0`) on warm gray pages (`base-50`)
-   Dark mode: Near-black cards (`base-900`) on pure black pages (`base-1000`)
-   Provides clear visual hierarchy without heavy shadows

### Semantic Token Mappings

#### Light Mode (Default)

**Page Structure:**

-   `background`: `base-50` — Warm gray page background (L 96.5)
-   `foreground`: `base-1000` — Pure black primary text (99 Lc on cards)
-   `card`: `base-0` — Pure white elevated surface (L 100)
-   `card-foreground`: `base-1000` — Pure black text on cards (99 Lc)

**Text Hierarchy:**

-   `foreground`: `base-1000` — Headings and primary text (99 Lc on cards)
-   `muted-foreground`: `base-600` — Secondary text, captions (67 Lc on cards)
-   `popover-foreground`: `base-1000` — Text in popovers (99 Lc)

**Interactive Elements:**

-   `primary`: `base-1000` — Black buttons and primary actions
-   `primary-foreground`: `base-0` — White text on primary buttons (99 Lc)
-   `secondary`: `base-200` — Secondary button backgrounds
-   `secondary-foreground`: `base-1000` — Text on secondary buttons (77 Lc)

**Surfaces & Containers:**

-   `muted`: `base-50` — Subtle sections, same as the page background
-   `accent`: `base-200` — Highlighted sections, table row hovers
-   `accent-foreground`: `base-1000` — Text on accent surfaces (77 Lc)
-   `popover`: `base-0` — Popover backgrounds (white)

**Borders & Inputs:**

-   `border`: `base-200` — Default borders (77 Lc separation)
-   `input`: `base-200` — Input field borders (77 Lc)
-   `ring`: `yellow-300` — Focus rings
    -   _TODO: replace the accent colour with gradient_

**Functional Colors:**

-   `destructive`: `red-500` — Destructive actions
-   `destructive-foreground`: `base-0` — Text on destructive buttons

#### Dark Mode

**Page Structure:**

-   `background`: `base-1000` — Pure black page background (L 0)
-   `foreground`: `base-50` — Very light primary text (97 Lc on cards)
-   `card`: `base-900` — Near-black elevated surface (L 19.8)
-   `card-foreground`: `base-50` — Light text on cards (97 Lc)

**Text Hierarchy:**

-   `foreground`: `base-50` — Headings and primary text (97 Lc on cards)
-   `muted-foreground`: `base-300` — Secondary text, captions (65 Lc on cards)
-   `popover-foreground`: `base-50` — Text in popovers (97 Lc)

**Interactive Elements:**

-   `primary`: `base-50` — Light buttons and primary actions
-   `primary-foreground`: `base-1000` — Black text on primary buttons (99 Lc)
-   `secondary`: `base-700` — Secondary button backgrounds
-   `secondary-foreground`: `base-50` — Text on secondary buttons (81 Lc)

**Surfaces & Containers:**

-   `muted`: `base-800` — Subtle sections (L 36.1)
-   `accent`: `base-700` — Highlighted sections, table row hovers
-   `accent-foreground`: `base-50` — Text on accent surfaces (81 Lc)
-   `popover`: `base-900` — Popover backgrounds (near-black)

**Borders & Inputs:**

-   `border`: `base-600` — Default borders (48 Lc separation)
-   `input`: `base-600` — Input field borders (48 Lc)
-   `ring`: `cyan-300` — Focus rings
    -   _TODO: replace the accent colour with gradient_

**Functional Colors:**

-   `destructive`: `red-500` — Destructive actions
-   `destructive-foreground`: `base-50` — Text on destructive buttons

### APCA Contrast Requirements

Minimum contrast values for accessibility compliance:

| Use Case                 | Minimum Lc | Light Mode Solution    | Dark Mode Solution      |
| ------------------------ | ---------- | ---------------------- | ----------------------- |
| **Body Text** (16px)     | ≥ 60 Lc    | `base-600` or darker   | `base-300` or lighter   |
| **Heading Text** (24px+) | ≥ 75 Lc    | `base-700` or darker   | `base-200` or lighter   |
| **Large Text** (18pt+)   | ≥ 60 Lc    | `base-600` or darker   | `base-300` or lighter   |
| **Button Text**          | ≥ 90 Lc    | `base-1000` / `base-0` | `base-50` / `base-1000` |
| **Placeholder Text**     | ≥ 40 Lc    | `base-400` or darker   | `base-500` or lighter   |
| **Disabled Text**        | ≥ 30 Lc    | `base-300` or darker   | `base-500` or lighter   |
| **Non-text (icons, UI)** | ≥ 45 Lc    | `base-500` or darker   | `base-400` or lighter   |

### Accent Color Usage Guidelines

[//]: # "**IMPORTANT: Accent colors (yellow, cyan, blue, purple, pink, red) are used ONLY for:**"
[//]: # "- Focus rings (`ring` token)"
[//]: # "- Focus indicators on interactive elements"
[//]: # "- Visual feedback for keyboard navigation"
[//]: #
[//]: # "**Accent colors should NEVER be used for:**"
[//]: # "- Primary or secondary buttons"
[//]: # "- Text colors (except in error/warning/success states using functional colors)"
[//]: # "- Background colors (use monochrome scale)"
[//]: # "- Badges or labels (use monochrome scale)"

**Focus Ring Colors:**

-   Light mode: `yellow-300` (warm, energetic, matches brand)
-   Dark mode: `cyan-300` (cool, tech-forward, high visibility)

### Component-Specific Mappings

#### Buttons

**Primary Button:**

-   Light: `bg-primary` (black) + `text-primary-foreground` (white)
-   Dark: `bg-primary` (light) + `text-primary-foreground` (black)
-   Maximum contrast for primary actions

**Secondary Button:**

-   Light: `bg-secondary` (`base-200`) + `text-secondary-foreground` (`base-1000`)
-   Dark: `bg-secondary` (`base-700`) + `text-secondary-foreground` (`base-50`)
-   Subtle but clear alternative actions

**Destructive Button:**

-   Both modes: `bg-destructive` (red) + `text-destructive-foreground`
-   Reserved for delete, remove, or dangerous actions

#### Form Elements

**Text Input:**

-   Background: `bg-background` (page background color)
-   Border: `border-input`
-   Text: `text-foreground`
-   Placeholder: `text-muted-foreground`
-   Focus ring: `ring-ring` (yellow/cyan accent)

**Select / Dropdown:**

-   Same as text input
-   Hover state: `bg-accent` with `text-accent-foreground`

#### Cards & Containers

**Card:**

-   Background: `bg-card` (elevated, pure white/near-black)
-   Text: `text-card-foreground`
-   Border: `border` (optional)

**Muted Section within Card:**

-   Background: `bg-muted` (subtle, blends with page)
-   Text: `text-muted-foreground`

#### Navigation & Menus

**Navigation Item:**

-   Default: `text-foreground`
-   Hover: `bg-accent` + `text-accent-foreground`
-   Active: `bg-primary` + `text-primary-foreground`

### Cross-Platform Considerations

**Figma → Web:**

-   Use semantic token names in Figma variables
-   Map directly to CSS custom properties
-   Maintain 1:1 naming convention

**Web → Mobile (iOS/Android):**

-   Convert OKLCH values to platform-native color spaces
-   iOS: Use P3 display color space when available
-   Android: Convert to sRGB for maximum compatibility
-   Maintain semantic meaning across platforms

### Token Selection Decision Tree

When choosing a semantic token:

1. **Is it text?**

    - Primary content → `foreground`
    - Secondary/supporting → `muted-foreground`

2. **Is it a surface/background?**

    - Main page → `background`
    - Elevated container → `card`
    - Subtle section → `muted`
    - Highlighted area → `accent`

3. **Is it interactive?**

    - Primary action → `primary` + `primary-foreground`
    - Secondary action → `secondary` + `secondary-foreground`
    - Destructive action → `destructive` + `destructive-foreground`

4. **Is it a border/outline?**

    - Default → `border`
    - Input field → `input`
    - Focus state → `ring` (only accent usage!)

5. **Is it a functional state?**
    - Error/danger → Use `red` from functional palette
    - Warning → Use functional yellow (not the accent yellow!)
    - Success → Use functional green (to be defined)
    - Info → Use `blue` from supporting palette

---

#### Foundation Tokens: Accent Colours

Brand identity colors that convey NextCoin's energy and innovation.

##### Yellow (Primary Brand Accent)

**Purpose**: Call-to-action, highlights, success states, optimism  
**Personality**: Energetic, forward-thinking, opportunity  
**Foundation Token Pattern**: `color-accent-yellow-{scale}`

| Scale | APCA Lc\* | Token                     | sRGB Hex  | sRGB                 | P3 OKLCH                    | P3 Hex (Figma) | Role                                    |
| ----- | --------- | ------------------------- | --------- | -------------------- | --------------------------- | -------------- | --------------------------------------- |
| 50    | 13        | `color-accent-yellow-50`  | `#fff1d0` | `rgb(255, 241, 209)` | `oklch(0.961 0.046 86.037)` | `#fdf1d4`      | Subtle yellow backgrounds, hover states |
| 100   | 27        | `color-accent-yellow-100` | `#ffe1a0` | `rgb(255, 225, 160)` | `oklch(0.92 0.089 86.132)`  | `#fae2a8`      | Light accents, soft emphasis            |
| 200   | 27        | `color-accent-yellow-200` | `#f9c647` | `rgb(248, 198, 71)`  | `oklch(0.85 0.15 86.645)`   | `#f0c85f`      | Secondary actions, badges               |
| 300   | 36        | `color-accent-yellow-300` | `#edb400` | `rgb(232, 179, 0)`   | `oklch(0.792 0.164 87.015)` | `#e0b43a`      | **Primary brand yellow** - Main CTAs    |
| 400   | 48        | `color-accent-yellow-400` | `#cc9f2c` | `rgb(208, 163, 51)`  | `oklch(0.739 0.135 86.002)` | `#c9a549`      | Active states, pressed buttons          |
| 500   | 54        | `color-accent-yellow-500` | `#bc9536` | `rgb(184, 146, 50)`  | `oklch(0.68 0.12 86.646)`   | `#b29444`      | Strong emphasis, prominent badges       |
| 600   | 70        | `color-accent-yellow-600` | `#8b7647` | `rgb(135, 118, 81)`  | `oklch(0.573 0.057 86.144)` | `#847755`      | Text on light backgrounds               |
| 700   | 85        | `color-accent-yellow-700` | `#665633` | `rgb(102, 86, 51)`   | `oklch(0.46 0.055 86.227)`  | `#635738`      | Heading text with yellow tint           |
| 800   | 96        | `color-accent-yellow-800` | `#413a28` | `rgb(66, 58, 40)`    | `oklch(0.35 0.031 86.108)`  | `#403a2a`      | High contrast yellow-tinted text        |
| 900   | 105       | `color-accent-yellow-900` | `#19160e` | `rgb(25, 22, 14)`    | `oklch(0.201 0.016 86.085)` | `#19160f`      | Dark mode surfaces with yellow base     |

##### Cyan (Secondary Brand Accent)

**Purpose**: Links, interactive elements, technology/innovation signals  
**Personality**: Fresh, digital, forward-moving  
**Foundation Token Pattern**: `color-accent-cyan-{scale}`

| Scale | APCA Lc\* | Token                   | sRGB Hex  | sRGB                 | P3 OKLCH                     | P3 Hex (Figma) | Role                                  |
| ----- | --------- | ----------------------- | --------- | -------------------- | ---------------------------- | -------------- | ------------------------------------- |
| 50    | 13        | `color-accent-cyan-50`  | `#d0fcfe` | `rgb(208, 252, 254)` | `oklch(0.961 0.045 199.079)` | `#d9fbfd`      | Subtle cyan backgrounds               |
| 100   | 27        | `color-accent-cyan-100` | `#90f5fb` | `rgb(146, 247, 253)` | `oklch(0.918 0.095 200.579)` | `#aaf5fc`      | Light info states                     |
| 200   | 27        | `color-accent-cyan-200` | `#00e0eb` | `rgb(32, 231, 242)`  | `oklch(0.845 0.14 201.275)`  | `#6de3ef`      | **Primary cyan** - Links, interactive |
| 300   | 35        | `color-accent-cyan-300` | `#01d2dc` | `rgb(14, 212, 214)`  | `oklch(0.789 0.133 196.259)` | `#61d1d5`      | Hover states, active links            |
| 400   | 45        | `color-accent-cyan-400` | `#27bdc6` | `rgb(44, 192, 196)`  | `oklch(0.736 0.117 197.697)` | `#5fbdc2`      | Pressed states                        |
| 500   | 55        | `color-accent-cyan-500` | `#23a8b0` | `rgb(34, 167, 173)`  | `oklch(0.666 0.107 199.311)` | `#51a5ab`      | Strong tech accents                   |
| 600   | 70        | `color-accent-cyan-600` | `#438286` | `rgb(67, 130, 133)`  | `oklch(0.566 0.065 199.142)` | `#538184`      | Cyan-tinted text                      |
| 700   | 85        | `color-accent-cyan-700` | `#315e61` | `rgb(49, 94, 96)`    | `oklch(0.451 0.05 199.142)`  | `#3c5d5f`      | Dark cyan text                        |
| 800   | 96        | `color-accent-cyan-800` | `#273f41` | `rgb(39, 63, 64)`    | `oklch(0.349 0.03 199.133)`  | `#2c3e40`      | High contrast cyan                    |
| 900   | 105       | `color-accent-cyan-900` | `#0a191a` | `rgb(10, 25, 26)`    | `oklch(0.201 0.021 199.141)` | `#0e1919`      | Dark mode cyan surfaces               |

---

#### Foundation Tokens: Supporting Colors

Extended palette for visual hierarchy, data visualization, and specialized UI contexts.

##### Blue

**Purpose**: Trust, professionalism, information, calm  
**Foundation Token Pattern**: `color-supporting-blue-{scale}`

| Scale | APCA Lc\* | Token                       | sRGB Hex  | sRGB                 | P3 OKLCH                     | P3 Hex (Figma) | Role                 |
| ----- | --------- | --------------------------- | --------- | -------------------- | ---------------------------- | -------------- | -------------------- |
| 50    | 13        | `color-supporting-blue-50`  | `#e8f3ff` | `rgb(232, 243, 255)` | `oklch(0.959 0.02 250.383)`  | `#eaf3fe`      | Info backgrounds     |
| 100   | 28        | `color-supporting-blue-100` | `#d0e8ff` | `rgb(207, 231, 254)` | `oklch(0.917 0.04 248.565)`  | `#d4e6fc`      | Light info states    |
| 200   | 28        | `color-supporting-blue-200` | `#a2d0fc` | `rgb(162, 208, 252)` | `oklch(0.841 0.079 247.647)` | `#abcff8`      | Info accents         |
| 300   | 35        | `color-supporting-blue-300` | `#83c4ff` | `rgb(131, 196, 255)` | `oklch(0.799 0.107 246.959)` | `#91c2fa`      | Info actions         |
| 400   | 45        | `color-supporting-blue-400` | `#57b2ff` | `rgb(87, 178, 255)`  | `oklch(0.741 0.142 246.772)` | `#6eb0f9`      | Active info states   |
| 500   | 54        | `color-supporting-blue-500` | `#4fa0e5` | `rgb(78, 157, 227)`  | `oklch(0.678 0.13 247.547)`  | `#629cdd`      | Strong info emphasis |
| 600   | 70        | `color-supporting-blue-600` | `#477eae` | `rgb(71, 126, 174)`  | `oklch(0.576 0.095 246.677)` | `#547daa`      | Blue text on light   |
| 700   | 85        | `color-supporting-blue-700` | `#365978` | `rgb(54, 89, 120)`   | `oklch(0.451 0.065 246.571)` | `#3e5875`      | Dark blue text       |
| 800   | 96        | `color-supporting-blue-800` | `#2c3c4c` | `rgb(44, 60, 76)`    | `oklch(0.349 0.035 248.861)` | `#2f3c4b`      | High contrast blue   |
| 900   | 105       | `color-supporting-blue-900` | `#0f171f` | `rgb(15, 23, 31)`    | `oklch(0.201 0.02 248.861)`  | `#11171e`      | Dark blue surfaces   |

##### Purple

**Purpose**: Creativity, innovation, premium features  
**Foundation Token Pattern**: `color-supporting-purple-{scale}`

| Scale | APCA Lc\* | Token                         | sRGB Hex  | sRGB                 | P3 OKLCH                     | P3 Hex (Figma) | Role                 |
| ----- | --------- | ----------------------------- | --------- | -------------------- | ---------------------------- | -------------- | -------------------- |
| 50    | 13        | `color-supporting-purple-50`  | `#f5eeff` | `rgb(245, 238, 255)` | `oklch(0.959 0.024 304.494)` | `#f4eefe`      | Purple backgrounds   |
| 100   | 28        | `color-supporting-purple-100` | `#ece0ff` | `rgb(236, 224, 255)` | `oklch(0.926 0.043 303.11)`  | `#eae0fd`      | Light purple states  |
| 200   | 28        | `color-supporting-purple-200` | `#d9c0ff` | `rgb(217, 192, 255)` | `oklch(0.85 0.09 302.667)`   | `#d5c1fb`      | Purple accents       |
| 300   | 37        | `color-supporting-purple-300` | `#ceaaff` | `rgb(206, 170, 255)` | `oklch(0.8 0.123 303.18)`    | `#c8abf9`      | Purple actions       |
| 400   | 46        | `color-supporting-purple-400` | `#c293ff` | `rgb(194, 147, 255)` | `oklch(0.75 0.157 302.867)`  | `#bb95f8`      | Active purple        |
| 500   | 57        | `color-supporting-purple-500` | `#a884d7` | `rgb(173, 136, 219)` | `oklch(0.693 0.125 303.933)` | `#a789d6`      | Strong purple        |
| 600   | 70        | `color-supporting-purple-600` | `#886caf` | `rgb(136, 108, 175)` | `oklch(0.585 0.104 302.539)` | `#846dab`      | Purple text          |
| 700   | 85        | `color-supporting-purple-700` | `#624e7e` | `rgb(98, 78, 126)`   | `oklch(0.465 0.079 302.599)` | `#5f4f7b`      | Dark purple text     |
| 800   | 96        | `color-supporting-purple-800` | `#3f364c` | `rgb(63, 54, 76)`    | `oklch(0.352 0.039 303.139)` | `#3e364a`      | High contrast purple |
| 900   | 105       | `color-supporting-purple-900` | `#191321` | `rgb(25, 19, 33)`    | `oklch(0.201 0.029 303.578)` | `#181320`      | Dark purple surfaces |

##### Pink

**Purpose**: Community, approachability, youth focus, warmth  
**Foundation Token Pattern**: `color-supporting-pink-{scale}`

| Scale | APCA Lc\* | Token                       | sRGB Hex  | sRGB                 | P3 OKLCH                     | P3 Hex (Figma) | Role               |
| ----- | --------- | --------------------------- | --------- | -------------------- | ---------------------------- | -------------- | ------------------ |
| 50    | 13        | `color-supporting-pink-50`  | `#fbeef1` | `rgb(251, 238, 241)` | `oklch(0.96 0.015 1.55)`     | `#f9eef1`      | Pink backgrounds   |
| 100   | 28        | `color-supporting-pink-100` | `#ffdbe6` | `rgb(255, 219, 230)` | `oklch(0.924 0.042 357.591)` | `#f9dce6`      | Light pink states  |
| 200   | 28        | `color-supporting-pink-200` | `#ffb6cc` | `rgb(255, 182, 204)` | `oklch(0.85 0.089 359.437)`  | `#f4b9cc`      | Pink accents       |
| 300   | 38        | `color-supporting-pink-300` | `#ff9abc` | `rgb(255, 154, 188)` | `oklch(0.799 0.126 358.718)` | `#f19fbb`      | Pink actions       |
| 400   | 45        | `color-supporting-pink-400` | `#ff83af` | `rgb(255, 131, 175)` | `oklch(0.761 0.157 358.997)` | `#ef8aae`      | Active pink        |
| 500   | 54        | `color-supporting-pink-500` | `#e07b9e` | `rgb(220, 119, 152)` | `oklch(0.692 0.13 0.323)`    | `#cf7c98`      | Strong pink        |
| 600   | 71        | `color-supporting-pink-600` | `#ad607a` | `rgb(173, 96, 122)`  | `oklch(0.585 0.104 359.222)` | `#a36479`      | Pink text          |
| 700   | 85        | `color-supporting-pink-700` | `#7d4558` | `rgb(125, 69, 88)`   | `oklch(0.464 0.08 358.98)`   | `#754858`      | Dark pink text     |
| 800   | 96        | `color-supporting-pink-800` | `#4c323a` | `rgb(76, 50, 58)`    | `oklch(0.351 0.04 359.273)`  | `#48333a`      | High contrast pink |
| 900   | 105       | `color-supporting-pink-900` | `#211016` | `rgb(33, 16, 22)`    | `oklch(0.2 0.03 357.516)`    | `#1f1116`      | Dark pink surfaces |

---

#### Foundation Tokens: Functional Colors

Status and feedback colors for system states.

##### Error/Destructive (Red)

**Purpose**: Errors, warnings, destructive actions, critical alerts  
**Foundation Token Pattern**: `color-functional-error-{scale}`

| Scale | APCA Lc\* | Token                        | sRGB Hex  | sRGB                 | P3 OKLCH                    | P3 Hex (Figma) | Role                    |
| ----- | --------- | ---------------------------- | --------- | -------------------- | --------------------------- | -------------- | ----------------------- |
| 50    | 13        | `color-functional-error-50`  | `#fceeed` | `rgb(252, 238, 237)` | `oklch(0.96 0.015 22.397)`  | `#faeeed`      | Error backgrounds       |
| 100   | 28        | `color-functional-error-100` | `#ffddd9` | `rgb(255, 221, 217)` | `oklch(0.925 0.038 25.815)` | `#f9deda`      | Light error states      |
| 200   | 28        | `color-functional-error-200` | `#ffbab2` | `rgb(255, 186, 178)` | `oklch(0.851 0.081 26.357)` | `#f5bdb4`      | Error accents           |
| 300   | 37        | `color-functional-error-300` | `#ffa097` | `rgb(255, 160, 151)` | `oklch(0.799 0.115 25.784)` | `#f2a49a`      | Error actions           |
| 400   | 46        | `color-functional-error-400` | `#ff857b` | `rgb(255, 135, 125)` | `oklch(0.754 0.15 26.093)`  | `#f08d81`      | Active error states     |
| 500   | 60        | `color-functional-error-500` | `#f6534e` | `rgb(254, 95, 91)`   | `oklch(0.694 0.199 25.091)` | `#ee6960`      | **Primary error color** |
| 600   | 71        | `color-functional-error-600` | `#cf413d` | `rgb(207, 65, 61)`   | `oklch(0.579 0.179 26.08)`  | `#bf4c44`      | Error text on light     |
| 700   | 85        | `color-functional-error-700` | `#933732` | `rgb(147, 55, 50)`   | `oklch(0.466 0.125 26.216)` | `#883d36`      | Dark error text         |
| 800   | 96        | `color-functional-error-800` | `#5a2b27` | `rgb(90, 43, 39)`    | `oklch(0.351 0.07 26.256)`  | `#542d29`      | High contrast error     |
| 900   | 105       | `color-functional-error-900` | `#22100f` | `rgb(34, 16, 15)`    | `oklch(0.199 0.031 23.599)` | `#201110`      | Dark error surfaces     |

---

### APCA Contrast Reference

All colors maintain consistent APCA Lc (Lightness contrast) values across hues at each scale level, tested against
`base-100` as reference.

**Contrast Scale Validation:**

| Scale | APCA Lc Range | Monochrome | Yellow | Cyan | Blue | Purple | Pink | Red | Accessibility                     |
| ----- | ------------- | ---------- | ------ | ---- | ---- | ------ | ---- | --- | --------------------------------- |
| 50    | ~13           | 13         | 13     | 13   | 13   | 13     | 13   | 13  | Subtle backgrounds only           |
| 100   | ~27           | 27         | 27     | 27   | 28   | 28     | 28   | 28  | Light backgrounds                 |
| 200   | ~27-38        | 38         | 27     | 27   | 28   | 28     | 28   | 28  | Borders, disabled states          |
| 300   | ~35-38        | 45         | 36     | 35   | 35   | 37     | 38   | 37  | Primary actions, badges           |
| 400   | ~45-48        | 55         | 48     | 45   | 45   | 46     | 45   | 46  | Active states, emphasis           |
| 500   | ~54-60        | 70         | 54     | 55   | 54   | 57     | 54   | 60  | Strong accents                    |
| 600   | ~70-71        | 85         | 70     | 70   | 70   | 70     | 71   | 71  | **Body text minimum** (Lc 60+)    |
| 700   | ~85           | 95         | 85     | 85   | 85   | 85     | 85   | 85  | **Heading text minimum** (Lc 75+) |
| 800   | ~95-96        | 100        | 96     | 96   | 96   | 96     | 96   | 96  | Maximum contrast text             |
| 900   | ~100-105      | 105        | 105    | 105  | 105  | 105    | 105  | 105 | Dark mode backgrounds             |

**Accessibility Thresholds:**

-   **Lc 60+**: Minimum for body text (scales 600+)
-   **Lc 75+**: Minimum for small text and headings (scales 700+)
-   **Lc 90+**: High contrast for maximum readability (scales 800+)

---

### Universal Scale Role Definitions

Each scale level has a **consistent functional role** across all color hues, enabling predictable color behavior.

#### Surface & Background Roles (50-100)

-   **50**: Page backgrounds, subtle fills, hover on white
-   **100**: Card backgrounds, muted surfaces, secondary fills

#### Interactive & Accent Roles (200-400)

-   **200**: Soft emphasis, secondary actions, borders
-   **300**: **PRIMARY ACTION LEVEL** - Main CTAs, links, badges, focus indicators
-   **400**: Active/pressed states, strong interactive emphasis

#### Medium Contrast Roles (500-600)

-   **500**: High emphasis accents, prominent UI elements, strong badges
-   **600**: Body text on light backgrounds (APCA Lc 60+), medium contrast UI

#### High Contrast Text Roles (700-800)

-   **700**: Heading text on light backgrounds (APCA Lc 75+), primary emphasis
-   **800**: Maximum contrast text on light, critical information

#### Dark Mode & Inversion (900)

-   **900**: Dark mode backgrounds, inverted surface colors, maximum dark

---

### Chart & Data Visualization Colors

For charts and data visualization, NextCoin uses a **tone progression strategy** that maps brand colors with
mathematical relationships for clear data hierarchy.

#### Chart Color System

**Primary Chart Scale** (Maps to brand accent colors):

-   `chart-1`: Yellow tone (from `color-accent-yellow-300`)
-   `chart-2`: Cyan tone (from `color-accent-cyan-200`)

**Supporting Chart Scale** (Maps to supporting colors):

-   `chart-3`: Blue tone (from `color-supporting-blue-300`)
-   `chart-4`: Purple tone (from `color-supporting-purple-300`)
-   `chart-5`: Pink tone (from `color-supporting-pink-300`)

**Tone Progression Strategy:**

Each chart colour includes five tonal variations for data hierarchy:

-   **Lightest** (50): Background fills, hover states
-   **Light** (100-200): Secondary data, less emphasis
-   **Base** (300): **Primary data point** - Main visualization
-   **Dark** (400-500): Emphasis, active selection
-   **Darkest** (600-700): Maximum contrast, text labels

**Example: Chart 1 (Yellow) Progression**

```
Foundation → Semantic Chart Token
────────────────────────────────
color-accent-yellow-50   → chart-1-lightest
color-accent-yellow-100  → chart-1-light
color-accent-yellow-300  → chart-1         (base)
color-accent-yellow-400  → chart-1-dark
color-accent-yellow-600  → chart-1-darkest
```

This creates a clear visual hierarchy in multi-series charts while maintaining brand consistency.

---

### 3-Tier Naming Flow Examples

Complete examples showing how colors flow through Foundation → Core → Semantic layers.

#### Example 1: Yellow Primary Action (CTA Button)

```
┌─────────────────────────────────────────────────────────────────┐
│ FOUNDATION LEVEL                                                │
├─────────────────────────────────────────────────────────────────┤
│ Token:  color-accent-yellow-300                                 │
│ Hex:    #edb400                                                 │
│ OKLCH:  oklch(0.75 0.15 85)  [TBD]                              │
│ Role:   Raw color value for primary brand yellow                │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ CORE LEVEL                                                      │
├─────────────────────────────────────────────────────────────────┤
│ Token:  brand.accent-primary                                    │
│ Value:  {color-accent-yellow-300}                               │
│ Role:   Primary brand accent for CTAs and highlights            │
│ Usage:  Main call-to-action buttons, focus indicators           │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ SEMANTIC LEVEL (Light Mode)                                     │
├─────────────────────────────────────────────────────────────────┤
│ Token:    ring                                                  │
│ Value:    {brand.accent-primary}                                │
│ CSS Var:  --ring                                                │
│ Usage:    Focus ring, keyboard navigation indicator             │
│ Tailwind: ring-ring                                             │
└─────────────────────────────────────────────────────────────────┘
```

#### Example 2: Base Foreground Text

```
┌─────────────────────────────────────────────────────────────────┐
│ FOUNDATION LEVEL                                                │
├─────────────────────────────────────────────────────────────────┤
│ Token:  color-base-700                                          │
│ Hex:    #595856                                                 │
│ OKLCH:  oklch(0.362 0.004 67.7)                                 │
│ Role:   Heading text level for monochrome palette               │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ CORE LEVEL                                                      │
├─────────────────────────────────────────────────────────────────┤
│ Token:  text.primary-light                                      │
│ Value:  {color-base-700}                                        │
│ Role:   Primary text color for light mode                       │
│ Usage:  Headings, emphasized text, primary copy                 │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ SEMANTIC LEVEL (Light Mode)                                     │
├─────────────────────────────────────────────────────────────────┤
│ Token:    foreground                                            │
│ Value:    {text.primary-light}                                  │
│ CSS Var:  --foreground                                          │
│ Usage:    Default text color for all UI elements                │
│ Tailwind: text-foreground                                       │
└─────────────────────────────────────────────────────────────────┘
```

#### Example 3: Cyan Interactive Link

```
┌─────────────────────────────────────────────────────────────────┐
│ FOUNDATION LEVEL                                                │
├─────────────────────────────────────────────────────────────────┤
│ Token:  color-accent-cyan-200                                   │
│ Hex:    #00e0eb                                                 │
│ OKLCH:  oklch(0.85 0.12 195)  [TBD]                             │
│ Role:   Primary cyan for interactive elements                   │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ CORE LEVEL                                                      │
├─────────────────────────────────────────────────────────────────┤
│ Token:  interactive.link                                        │
│ Value:  {color-accent-cyan-200}                                 │
│ Role:   Link and interactive element color                      │
│ Usage:  Hyperlinks, clickable text, nav indicators              │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ SEMANTIC LEVEL (Light Mode)                                     │
├─────────────────────────────────────────────────────────────────┤
│ Token:    accent                                                │
│ Value:    {interactive.link}                                    │
│ CSS Var:  --accent                                              │
│ Usage:    Links, secondary interactive elements                 │
│ Tailwind: text-accent, bg-accent                                │
└─────────────────────────────────────────────────────────────────┘
```

#### Example 4: Error State (Destructive)

```
┌─────────────────────────────────────────────────────────────────┐
│ FOUNDATION LEVEL                                                │
├─────────────────────────────────────────────────────────────────┤
│ Token:  color-functional-error-500                              │
│ Hex:    #f6534e                                                 │
│ OKLCH:  oklch(0.615 0.200 25.9)  [TBD]                          │
│ Role:   Primary error/destructive action color                  │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ CORE LEVEL                                                      │
├─────────────────────────────────────────────────────────────────┤
│ Token:  feedback.error                                          │
│ Value:  {color-functional-error-500}                            │
│ Role:   Error feedback and destructive actions                  │
│ Usage:  Error messages, delete buttons, critical warnings       │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ SEMANTIC LEVEL (Light Mode)                                     │
├─────────────────────────────────────────────────────────────────┤
│ Token:    destructive                                           │
│ Value:    {feedback.error}                                      │
│ CSS Var:  --destructive                                         │
│ Usage:    Destructive buttons, error states, critical alerts    │
│ Tailwind: bg-destructive, text-destructive                      │
└─────────────────────────────────────────────────────────────────┘
```

#### Example 5: Chart Color (Data Visualization)

```
┌─────────────────────────────────────────────────────────────────┐
│ FOUNDATION LEVEL                                                │
├─────────────────────────────────────────────────────────────────┤
│ Token:  color-accent-yellow-300                                 │
│ Hex:    #edb400                                                 │
│ OKLCH:  oklch(0.75 0.15 85)  [TBD]                              │
│ Role:   Primary brand yellow, base for chart scale              │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ CORE LEVEL                                                      │
├─────────────────────────────────────────────────────────────────┤
│ Token:  data-viz.series-1                                       │
│ Value:  {color-accent-yellow-300}                               │
│ Role:   Primary data series color                               │
│ Usage:  First series in charts, primary data visualization      │
│                                                                 │
│ Tone Progression:                                               │
│ • Lightest: {color-accent-yellow-50}   → Background fills       │
│ • Light:    {color-accent-yellow-100}  → Secondary data         │
│ • Base:     {color-accent-yellow-300}  → Primary data           │
│ • Dark:     {color-accent-yellow-400}  → Emphasis               │
│ • Darkest:  {color-accent-yellow-600}  → Labels, maximum        │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ SEMANTIC LEVEL                                                  │
├─────────────────────────────────────────────────────────────────┤
│ Token:    chart-1                                               │
│ Value:    {data-viz.series-1}                                   │
│ CSS Var:  --chart-1                                             │
│ Usage:    Primary chart/graph series                            │
│ Tailwind: stroke-chart-1, fill-chart-1                          │
│                                                                 │
│ Extended Tones (for multi-level charts):                        │
│ • chart-1-lightest  → --chart-1-lightest                        │
│ • chart-1-light     → --chart-1-light                           │
│ • chart-1-dark      → --chart-1-dark                            │
│ • chart-1-darkest   → --chart-1-darkest                         │
└─────────────────────────────────────────────────────────────────┘
```

---

### Color Role Mapping

How foundation colors map to brand roles:

```
Foundation → Core → Semantic (Light) → Semantic (Dark)
──────────────────────────────────────────────────────
base-50     → surface.subtle    → background      → base-900
base-900    → brand.primary     → primary         → base-50
base-1000   → text.primary      → foreground      → base-0

accent-yellow-300 → brand.accent → ring           → accent-yellow-200
accent-cyan-200   → interactive  → link           → accent-cyan-300

error-500   → feedback.error    → destructive    → error-400
```

### Generating Color Roles (Guidelines)

When assigning colors to roles, follow these principles:

1. **Text on Backgrounds**: Minimum APCA Lc 60 for body text, Lc 75 for small text
2. **Interactive States**: Use color scale steps for hover/active states
    - Default: Scale value
    - Hover: +100 or -100 on scale
    - Active: +200 or -200 on scale
3. **Surface Hierarchy**:
    - Level 0 (Background): Lightest/darkest
    - Level 1 (Cards): One step toward middle
    - Level 2 (Raised): Two steps toward middle
4. **Mode Inversion**: Dark mode often inverts the lightness scale
    - Light mode `background` = `base-50` (light)
    - Dark mode `background` = `base-900` (dark)

---

---

### Mode Inversion Matrix

How colors transition between light and dark modes, showing the systematic inversion strategy.

#### Light Mode → Dark Mode Mapping

**Background Surfaces** (Inverted Scale):
| Light Mode | Token | → | Dark Mode | Token | Strategy |
|------------|-------|---|-----------|-------|----------|
| `base-50` | Page BG | → | `base-900` | Page BG | Full inversion |
| `base-100` | Card | → | `base-800` | Card | One step lighter |
| `base-0` | Accent | → | `base-1000` | Accent | Maximum inversion |

**Foreground Text** (Inverted Scale):
| Light Mode | Token | → | Dark Mode | Token | Strategy |
|------------|-------|---|-----------|-------|----------|
| `base-900` | Primary text | → | `base-50` | Primary text | Near full inversion |
| `base-700` | Heading | → | `base-100` | Heading | Adjusted for readability |
| `base-600` | Body text | → | `base-200` | Body text | Maintained contrast |
| `base-500` | Secondary | → | `base-400` | Secondary | Subtle adjustment |

**Interactive Elements** (Adjusted for Dark Mode):
| Light Mode | Token | → | Dark Mode | Token | Strategy |
|------------|-------|---|-----------|-------|----------|
| `accent-yellow-300` | CTA | → | `accent-yellow-200` | CTA | Lighter for visibility |
| `accent-cyan-200` | Link | → | `accent-cyan-300` | Link | Slightly darker |
| `functional-error-500` | Error | → | `functional-error-400` | Error | Adjusted for readability |

**Borders & Dividers** (Inverted):
| Light Mode | Token | → | Dark Mode | Token | Strategy |
|------------|-------|---|-----------|-------|----------|
| `base-200` | Border | → | `base-700` | Border | Inverted for visibility |
| `base-300` | Input | → | `base-600` | Input | Adjusted contrast |

#### Complete Semantic Token Inversion Table

| Semantic Token           | Light Mode Value    | Dark Mode Value     | Inversion Rule             |
| ------------------------ | ------------------- | ------------------- | -------------------------- |
| `background`             | `base-50`           | `base-900`          | Full inversion + one step  |
| `foreground`             | `base-1000`         | `base-0`            | Complete inversion         |
| `card`                   | `base-0`            | `base-800`          | Surface level adjustment   |
| `card-foreground`        | `base-1000`         | `base-0`            | Matches foreground         |
| `primary`                | `base-900`          | `base-50`           | Near full inversion        |
| `primary-foreground`     | `base-0`            | `base-900`          | Inverse of primary         |
| `secondary`              | `base-100`          | `base-800`          | Surface to dark surface    |
| `secondary-foreground`   | `base-900`          | `base-0`            | Text on surface            |
| `muted`                  | `base-100`          | `base-800`          | Muted surface inversion    |
| `muted-foreground`       | `base-500`          | `base-400`          | Subtle text inversion      |
| `accent`                 | `base-0`            | `base-1000`         | Pure inversion             |
| `accent-foreground`      | `base-1000`         | `base-0`            | Contrasting text           |
| `destructive`            | `error-500`         | `error-400`         | Lightened for dark         |
| `destructive-foreground` | `error-50`          | `error-900`         | Background to surface      |
| `border`                 | `base-200`          | `base-700`          | Inverted with adjustment   |
| `input`                  | `base-100`          | `base-800`          | Input surface inversion    |
| `ring`                   | `accent-yellow-300` | `accent-yellow-200` | Focus indicator adjustment |

#### Inversion Principles

1. **Symmetric Lightness**: Light mode L=20 becomes dark mode L=80 (approx.)
2. **Contrast Preservation**: APCA contrast ratios maintained across modes
3. **Accent Adjustment**: Brand colors shifted 1-2 steps for optimal visibility
4. **Text Hierarchy**: Relative contrast between text levels preserved
5. **Border Visibility**: Borders adjusted to maintain separation without harshness

---

## Color Space: OKLCH

All colors export to OKLCH format for CSS, providing perceptually uniform color manipulation.

### OKLCH Format

```text
oklch  (  L C H  /  A  )
```

-   **L**: Lightness (0-1 or 0-100%)
-   **C**: Chroma/saturation (0-0.4)
-   **H**: Hue angle (0-360)
-   **A**: Alpha/opacity (optional)

### Why OKLCH?

1. **Perceptual Uniformity**: Equal numeric changes = equal perceived changes
2. **Predictable Lightness**: L value directly correlates to perceived brightness
3. **Better Contrast**: Easier to maintain WCAG/APCA contrast ratios
4. **Modern Standard**: Native CSS support, future-proof

### Example Token → CSS Export

**Token (JSON)**:

```json
{
	"base": {
		"900": {
			"$type": "color",
			"$value": "#2e2e2d"
		}
	}
}
```

**Exported CSS**:

```css
:root {
	--color-base-900: oklch(0.182 0.004 84.6);
}
```

---

## Typography System

### Font Families

-   **Sans**: Geist - Primary interface font
-   **Mono**: Geist Mono - Code, technical content
-   **Serif**: System serif stack - Reserved for special use

### Type Scale

Based on a mathematical progression for consistent hierarchy:

| Token         | Size | Usage              |
| ------------- | ---- | ------------------ |
| `heading-7xl` | 72px | Hero headlines     |
| `heading-6xl` | 60px | Page titles        |
| `heading-5xl` | 48px | Section headers    |
| `heading-4xl` | 36px | Subsection headers |
| `heading-3xl` | 30px | Card titles        |
| `heading-2xl` | 24px | Small headings     |
| `body-2xl`    | 24px | Large body text    |
| `body-xl`     | 20px | Lead paragraphs    |
| `body-lg`     | 18px | Emphasized body    |
| `body-base`   | 16px | Default body text  |
| `body-sm`     | 14px | Small body text    |
| `body-xs`     | 12px | Fine print         |
| `label-lg`    | 18px | Large labels       |
| `label-base`  | 16px | Default labels     |
| `label-sm`    | 14px | Small labels       |
| `label-xs`    | 12px | Tiny labels        |

### Composed Typography Tokens

Typography tokens combine multiple properties:

```json
{
	"heading-xl": {
		"fontFamily": "Geist",
		"fontSize": "20px",
		"fontWeight": "600",
		"lineHeight": "130%",
		"letterSpacing": "-2%"
	}
}
```

---

## Spacing System

8-point grid system for consistent spatial rhythm:

```
0    → 0px
0.5  → 2px   (0.125rem)
1    → 4px   (0.25rem)
2    → 8px   (0.5rem)
3    → 12px  (0.75rem)
4    → 16px  (1rem)
6    → 24px  (1.5rem)
8    → 32px  (2rem)
12   → 48px  (3rem)
16   → 64px  (4rem)
```

---

## Usage Guide

### For Designers

**Figma Integration** (Tokens Studio Plugin):

1. Sync tokens from repository
2. Apply semantic tokens to designs
3. Use variables for consistent application
4. Export designs with token references

**Token Selection**:

-   Use **semantic tokens** in designs (e.g., `background`, `primary`)
-   Avoid using foundation tokens directly in designs
-   Reference the color role table for appropriate contexts

### For Developers

**Tailwind CSS Classes**:

```jsx
// Use semantic color tokens via Tailwind
<div className="bg-background text-foreground">
	<h1 className="text-primary">Heading</h1>
	<p className="text-muted-foreground">Body text</p>
</div>
```

**Direct CSS Variables**:

```css
.custom-component {
	background: var(--background);
	color: var(--foreground);
	border: 1px solid var(--border);
}
```

**shadcn/ui Integration**:
All shadcn/ui components automatically use the token system via CSS variables. No additional configuration needed.

---

## Naming Conventions

### Summary Table

| Level      | Pattern                    | Example                                  | Audience   |
| ---------- | -------------------------- | ---------------------------------------- | ---------- |
| Foundation | `{type}-{variant}-{scale}` | `color-base-500`, `spacing-4`            | Both       |
| Core       | `{role}.{variant}`         | `brand.primary`, `typography.heading-xl` | Designers  |
| Semantic   | `{ui-role}`                | `background`, `primary-foreground`       | Developers |
| CSS Output | `--{semantic-name}`        | `--background`, `--primary`              | Developers |

### Naming Principles

1. **Use kebab-case** for all token names
2. **Numbers for scales**: 0, 50, 100, 200...900, 1000
3. **T-shirt sizes for relative scales**: xs, sm, base/md, lg, xl, 2xl
4. **Descriptive over generic**: `accent-yellow-300` not `color-1`
5. **Semantic at UI layer**: `destructive` not `error-red`

---

## File Structure

```
nextcoin-design-system/
├── tokens/
│   ├── foundation/
│   │   ├── colors/
│   │   │   ├── base.json           # Monochrome palette
│   │   │   ├── accent.json         # Yellow, Cyan
│   │   │   ├── supporting.json     # Blue, Purple, Pink
│   │   │   └── functional.json     # Error, Warning, Success
│   │   ├── typography/
│   │   │   ├── font-families.json
│   │   │   ├── font-sizes.json
│   │   │   ├── font-weights.json
│   │   │   ├── line-heights.json
│   │   │   └── letter-spacing.json
│   │   ├── spacing.json
│   │   ├── border-radius.json
│   │   └── effects.json
│   │
│   ├── core/
│   │   ├── colors.json            # Brand color roles
│   │   ├── typography.json        # Composed type styles
│   │   └── effects.json           # Brand effects
│   │
│   ├── semantic/
│   │   ├── light.json             # Light mode mappings
│   │   └── dark.json              # Dark mode mappings
│   │
│   ├── $metadata.json
│   └── $themes.json
│
├── dist/
│   └── css/
│       └── tokens.css             # Generated CSS output
│
├── scripts/
│   ├── build-tokens.js            # Build pipeline
│   └── validate-tokens.js         # Token validation
│
└── docs/
    ├── color-system.md
    ├── typography.md
    ├── usage-guide.md
    └── migration-guide.md
```

---

## Current Status

### ✅ Completed

-   Foundation color palettes (base, accent, supporting, error)
-   Typography scales and composed styles
-   Initial semantic token mappings

### 🚧 In Progress

-   Restructuring token organization (foundation/core/semantic)
-   Build pipeline for CSS export with OKLCH transform
-   Complete semantic token definitions for all shadcn/ui variables

### 📋 Planned

-   Component-specific token documentation
-   Figma variable sync automation
-   Extended color roles for illustrations/charts
-   Motion/animation tokens

---

## Contributing

When adding or modifying tokens:

1. **Foundation changes**: Update raw values in `tokens/foundation/`
2. **Brand changes**: Adjust role mappings in `tokens/core/`
3. **UI changes**: Modify semantic mappings in `tokens/semantic/`
4. **Test in context**: Verify changes in Tailwind/shadcn components

---

## Resources

-   [Design Tokens W3C Spec](https://design-tokens.github.io/community-group/format/)
-   [Tokens Studio Documentation](https://docs.tokens.studio/)
-   [OKLCH Color Space](https://oklch.com/)
-   [Tailwind CSS v4](https://tailwindcss.com/docs)
-   [shadcn/ui](https://ui.shadcn.com/)
-   [APCA Contrast](https://www.myndex.com/APCA/)
