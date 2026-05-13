---
version: alpha
name: Pixar
description: BlaBlaCar's design system. Defines the visual identity ensuring consistency across design sessions and between different AI agents and tools.

colors:
  # Neutral - Core UI colors for text, backgrounds, and borders
  neutral-txt-default: "#001536"
  neutral-txt-default-active: "#000C1F"
  neutral-txt-weak: "#576680"
  neutral-txt-moderate: "#576680"
  neutral-txt-inverted: "#FFFFFF"
  neutral-txt-inverted-active: "#FFFFFF"
  neutral-bg-default: "#FFFFFF"
  neutral-bg-default-active: "#F5F7FB"
  neutral-bg-deep: "#F5F7FB"
  neutral-bg-delicate: "#E9ECF0"
  neutral-bg-weak: "#E9ECF0"
  neutral-bg-moderate: "#146899"
  neutral-bg-strong: "#576680"
  neutral-bg-elevated: "#FFFFFF"
  neutral-border-default: "#3032331F"
  neutral-border-default-active: "#30323329"
  neutral-border-weak: "#30323314"
  neutral-border-moderate: "#146899"
  neutral-border-strong: "#001536CC"
  neutral-border-match-bg-default: "#FFFFFF"

  # Accent - Primary action and focus colors (blue)
  accent-txt-default: "#0066D4"
  accent-txt-default-active: "#0056B2"
  accent-txt-strong: "#02193E"
  accent-txt-strong-active: "#042E72"
  accent-txt-inverted: "#FFFFFF"
  accent-txt-inverted-active: "#FFFFFF"
  accent-bg-strong: "#0071EB"
  accent-bg-strong-active: "#0065D1"
  accent-bg-weak: "#E6F2FE"
  accent-bg-weak-active: "#C7E3FF"
  accent-bg-strongest: "#001536"
  accent-bg-strongest-active: "#001F52"
  accent-border-default: "#0071EB"
  accent-border-default-active: "#0065D1"
  accent-border-strong: "#001536"

  # Disabled - Muted states for inactive elements
  disabled-txt-default: "#B5B8BD"
  disabled-txt-moderate: "#768499"
  disabled-bg-default: "#D7DBE0"
  disabled-border-default: "#3032330A"
  disabled-border-strong: "#7A889E"

  # Success - Positive feedback (green)
  success-txt-default: "#297856"
  success-txt-inverted: "#C5FFC6"
  success-bg-strong: "#107046"
  success-bg-weak: "#C5FFC6"
  success-border-default: "#107046"
  success-border-strong: "#054F21"

  # Caution - Attention needed (yellow)
  caution-txt-default: "#DD9E0C"
  caution-txt-inverted: "#3F3506"
  caution-bg-strong: "#FFCC56"

  # Warning - Potential issue (orange)
  warning-txt-default: "#B84412"
  warning-txt-default-active: "#8B330E"
  warning-txt-inverted: "#3F2206"
  warning-txt-strong: "#423007"
  warning-txt-moderate: "#7A5F50"
  warning-bg-strong: "#FF993A"
  warning-bg-weak: "#FFE7D1"
  warning-bg-weak-active: "#F6EADA"

  # Danger - Critical issue (red)
  danger-txt-default: "#BA303B"
  danger-txt-inverted: "#FFFFFF"
  danger-bg-strong: "#C11417"
  danger-bg-strong-active: "#9D1013"
  danger-bg-weak: "#FFDAE0"

  # Promote - Sales and promotional elements (green)
  promote-txt-default: "#297856"
  promote-txt-inverted: "#C5FFC6"
  promote-txt-strong: "#054F21"
  promote-bg-weak: "#C5FFC6"
  promote-bg-strong: "#107046"

  # Space - Brand and feature-specific colors
  space-apple-txt-inverted: "#FFFFFF"
  space-apple-bg-strong: "#000000"
  space-apple-bg-strong-active: "#3F3F3F"
  space-facebook-txt-inverted: "#FFFFFF"
  space-facebook-bg-strong: "#4A66AC"
  space-facebook-bg-strong-active: "#29487D"
  space-vk-txt-inverted: "#FFFFFF"
  space-vk-bg-strong: "#2787F5"
  space-vk-bg-strong-active: "#0668D8"
  space-gpay-txt-inverted: "#FFFFFF"
  space-gpay-bg-strong: "#000000"
  space-gpay-bg-strong-active: "#3F3F3F"
  space-paypal-txt-default: "#292A30"
  space-paypal-bg-default: "#FFCC57"
  space-paypal-bg-default-active: "#F5B522"
  space-blik-txt-inverted: "#FFFFFF"
  space-blik-bg-strong: "#000000"
  space-blik-bg-strong-active: "#3F3F3F"
  space-pix-txt-inverted: "#FFFFFF"
  space-pix-bg-strong: "#33BDAD"
  space-pix-bg-strong-active: "#1CA393"
  space-ideal-txt-inverted: "#1D1C1C"
  space-ideal-bg-strong: "#FFF48D"
  space-ideal-bg-strong-active: "#FFF9C2"
  space-ob-txt-inverted: "#FFFFFF"
  space-ob-bg-strong: "#FF595A"
  space-daily-txt-inverted: "#FFFFFF"
  space-daily-bg-strong: "#30004B"
  space-boost-txt-inverted: "#FFFFFF"
  space-verified-driver-txt-default: "#0066D4"
  space-verified-driver-txt-inverted: "#FFFFFF"
  space-super-driver-txt-default: "#0066D4"
  space-super-driver-txt-inverted: "#FFFFFF"
  space-super-driver-bg-strong: "#0066D4"
  space-esc-txt-default: "#054752"
  space-esc-bg-default: "#A9E873"
  space-subscription-txt-strong: "#2A0138"
  space-subscription-txt-inverted: "#FFFFFF"
  space-subscription-bg-strong: "#2A0138"
  space-subscription-bg-strong-active: "#17001F"
  space-subscription-bg-weak: "#E4D8FF"

typography:
  hero-desktop:
    fontFamily: GT Eesti Pro Display
    fontSize: 54px
    fontWeight: 800
    lineHeight: 1.0
  hero-mobile:
    fontFamily: GT Eesti Pro Display
    fontSize: 46px
    fontWeight: 800
    lineHeight: 1.0
  title-primary-desktop:
    fontFamily: GT Eesti Pro Display
    fontSize: 38px
    fontWeight: 800
    lineHeight: 1.1
  title-primary-mobile:
    fontFamily: GT Eesti Pro Display
    fontSize: 28px
    fontWeight: 800
    lineHeight: 1.1
  title-secondary:
    fontFamily: GT Eesti Pro Display
    fontSize: 22px
    fontWeight: 500
    lineHeight: 1.1
  title-tertiary:
    fontFamily: GT Eesti Pro Display
    fontSize: 18px
    fontWeight: 500
    lineHeight: 1.1
  title-label-default:
    fontFamily: GT Eesti Pro Display
    fontSize: 16px
    fontWeight: 500
    lineHeight: 1.1
  title-label-small:
    fontFamily: GT Eesti Pro Display
    fontSize: 14px
    fontWeight: 500
    lineHeight: 1.1
  body-default:
    fontFamily: GT Eesti Pro Display
    fontSize: 16px
    fontWeight: 400
    lineHeight: 1.2
  body-small:
    fontFamily: GT Eesti Pro Display
    fontSize: 14px
    fontWeight: 400
    lineHeight: 1.2
  body-too-small:
    fontFamily: GT Eesti Pro Display
    fontSize: 12px
    fontWeight: 400
    lineHeight: 1.4
  body-too-small-mobile:
    fontFamily: GT Eesti Pro Display
    fontSize: 10px
    fontWeight: 400
    lineHeight: 1.4
  number-xl-desktop:
    fontFamily: GT Eesti Pro Display
    fontSize: 82px
    fontWeight: 500
    lineHeight: 1.0
  number-xl-mobile:
    fontFamily: GT Eesti Pro Display
    fontSize: 40px
    fontWeight: 500
    lineHeight: 1.1

rounded:
  weak: 8px
  moderate: 12px
  default: 16px
  strong: 24px
  round: 9999px

spacing:
  gap-min: 4px
  gap-narrow: 8px
  gap-smaller: 12px
  gap-default: 16px
  gap-larger: 24px
  gap-max: 48px
  horizontal-min: 2px
  horizontal-smaller: 16px
  horizontal-default: 24px
  vertical-min: 2px
  vertical-smaller: 8px
  vertical-default: 12px
  vertical-larger: 16px
  vertical-max: 24px

components:
  button-primary:
    backgroundColor: "{colors.accent-bg-strong}"
    textColor: "{colors.accent-txt-inverted}"
    typography: "{typography.title-label-default}"
    rounded: "{rounded.default}"
    height: 48px
    paddingInline: "{spacing.horizontal-smaller}"
    paddingBlock: "{spacing.vertical-default}"
  button-primary-hover:
    backgroundColor: "{colors.accent-bg-strong-active}"
  button-primary-disabled:
    backgroundColor: "{colors.disabled-bg-default}"
    textColor: "{colors.disabled-txt-default}"
  button-secondary:
    backgroundColor: "{colors.neutral-bg-default}"
    textColor: "{colors.accent-txt-default}"
    rounded: "{rounded.default}"
    height: 48px
    paddingInline: "{spacing.horizontal-smaller}"
    paddingBlock: "{spacing.vertical-default}"
  button-secondary-hover:
    backgroundColor: "{colors.neutral-bg-default-active}"
    textColor: "{colors.accent-txt-default-active}"
  input-default:
    backgroundColor: "{colors.neutral-bg-default}"
    textColor: "{colors.neutral-txt-default}"
    rounded: "{rounded.default}"
    height: 48px
    paddingInline: "{spacing.horizontal-smaller}"
    paddingBlock: "{spacing.vertical-default}"
  input-focus:
    backgroundColor: "{colors.neutral-bg-default}"
    textColor: "{colors.neutral-txt-default}"
  input-error:
    backgroundColor: "{colors.neutral-bg-default}"
    textColor: "{colors.neutral-txt-default}"
  card-default:
    backgroundColor: "{colors.neutral-bg-elevated}"
    borderColor: "{colors.neutral-border-default}"
    rounded: "{rounded.default}"
  card-selected:
    borderColor: "{colors.accent-border-default}"
  card-disabled:
    borderColor: "{colors.disabled-border-default}"
  card-interactive-hover:
    borderColor: "{colors.accent-border-default}"
  card-semantic-accent:
    backgroundColor: "{colors.accent-bg-weak}"
---

# Pixar Design System

## Overview

Pixar is BlaBlaCar's design system for web applications, embodying the brand's friendly, trustworthy, and accessible personality. The system balances professionalism with warmth, using a clean blue accent palette against neutral backgrounds to create interfaces that feel reliable and approachable.

**Brand personality:**
- **Trustworthy** — Clear visual hierarchy and consistent patterns build user confidence
- **Friendly** — Generous spacing and rounded corners create a welcoming feel
- **Accessible** — High contrast ratios and semantic color usage ensure inclusivity
- **Modern** — Clean typography and subtle shadows establish contemporary aesthetics

**Target audience:** BlaBlaCar users ranging from first-time passengers to experienced drivers, across diverse age groups and technical proficiency levels.

## Colors

The color system is organized around semantic categories rather than raw palettes. Each category serves a specific purpose in the interface, with roles (txt, bg, border) and intensities (weak, default, strong) providing granular control.

### Semantic Pairing Rules

**This is the most important concept in the color system.** Color tokens work with a "pairing" notion — a text (or icon) color must always be considered in context with its background.

#### Rule 1: Semantic Exclusivity

Colors are separated into semantic groups. **Neutral** is the base and represents "the lack of semantic importance." It is the only semantic that accepts other semantics when used as a background:

- ✓ `success-txt-default` on `neutral-bg-default` — allowed
- ✓ `accent-txt-default` on `neutral-bg-default` — allowed
- ✗ `warning-bg-weak` with `danger-txt-default` — **forbidden** (mixing semantics)

All other semantic groups (success, warning, caution, danger, promote, accent) are **exclusive**. You cannot mix colors from different semantics.

#### Rule 2: Background-to-Text Pairing

Within a semantic group, the background intensity determines which text colors are valid:

| Background | Allowed Text | Forbidden Text |
|------------|--------------|----------------|
| `bg-default` | `txt-default`, `txt-strong`, `txt-weak`, `txt-moderate` | `txt-inverted` |
| `bg-weak` | `txt-default`, `txt-strong` | `txt-weak`, `txt-inverted` |
| `bg-strong` | `txt-inverted` only | everything else |

**Why these rules exist:**
1. **Accessibility** — By limiting valid pairings, we guarantee WCAG-compliant contrast ratios without manual checking
2. **Theme resilience** — Design for light mode and be confident the experience works in dark mode

### Semantic Categories

- **Neutral** — The foundation of the UI. Deep ink (`#001536`) for primary text, soft greys for secondary content, white for elevated surfaces. The only semantic that accepts other semantics on its backgrounds.

- **Accent** — The primary action color. A vibrant blue (`#0071EB`) for buttons, links, and focus states. Use on neutral backgrounds for interactive elements.

- **Success** — Green (`#107046`) for positive outcomes: completed bookings, verified profiles, successful payments.

- **Caution** — Yellow (`#FFCC56`) for indeterminate states: something is not yet successful, but it's not up to the user to make it happen.

- **Warning** — Orange (`#FF993A`) for ambiguous information users should be aware of. Not an error, not negative (yet), but comes with urgency. Example: scarcity indicators.

- **Danger** — Red (`#C11417`) for errors and negative emotions. Example: form errors, global errors.

- **Promote** — Green (`#107046`) for sales and promotions, embodying the "good deal" mantra. Visually similar to success but semantically distinct.

- **Disabled** — Muted grey (`#D7DBE0`) for interactive components in a disabled state only. Not for muting UI elements — use `neutral-txt-weak` for that.

### Space Colors

`space/*` colors are dedicated to brands or niches. They don't follow Pixar's brand rules (e.g., `space-paypal` follows PayPal's guidelines), but the same pairing rules apply: a space's `bg-strong` expects `txt-inverted` from its own space.

- Payment providers: Apple Pay, Google Pay, PayPal, Blik, Pix, iDEAL, Open Banking
- Social login: Facebook, VK
- Product features: Boost, ESC, Super Driver, Verified Driver, Subscription, Daily

### Theming

The system supports light and dark modes. Tokens maintain semantic meaning across themes — `neutral-bg-default` adapts from white to near-black while preserving its role as the primary background. The pairing rules guarantee that designs work across themes without manual verification.

## Typography

All text uses **GT Eesti Pro Display**, a geometric sans-serif that balances warmth with precision. The type scale follows a clear hierarchy:

### Scale

| Token | Size | Weight | Use Case |
|-------|------|--------|----------|
| `hero-desktop` | 54px | Ultra (800) | Hero banners, one per page max |
| `hero-mobile` | 46px | Ultra (800) | Hero banners on mobile |
| `title-primary-desktop` | 38px | Ultra (800) | Page titles, main headings |
| `title-primary-mobile` | 28px | Ultra (800) | Page titles on mobile |
| `title-secondary` | 22px | Medium (500) | Section headers |
| `title-tertiary` | 18px | Medium (500) | Subsection headers |
| `title-label-default` | 16px | Medium (500) | Component labels, button text |
| `title-label-small` | 14px | Medium (500) | Small labels, form labels |
| `body-default` | 16px | Regular (400) | Body text, paragraphs |
| `body-small` | 14px | Regular (400) | Secondary content |
| `body-too-small` | 12px | Regular (400) | Captions, legal text |
| `body-too-small-mobile` | 10px | Regular (400) | Last resort only |
| `number-xl-desktop` | 82px | Medium (500) | Large promotional numbers |
| `number-xl-mobile` | 40px | Medium (500) | Large numbers on mobile |

### Line Heights

- **Hero/Numbers**: 100% — Tight for visual impact
- **Titles**: 110% — Slightly open for readability
- **Body**: 120% — Comfortable reading
- **Small text**: 140% — Extra spacing aids legibility at small sizes

## Layout

The layout system uses a flexible grid with consistent spacing tokens.

### Grid

- **Desktop max width**: 1320px (sectionMax)
- **Desktop large**: 1016px (sectionLarge) — Primary content width
- **Desktop centered**: 662px (sectionSmall) — Narrow content, forms
- **Sidebar**: 360px (sectionSidebar) — Fixed sidebar width
- **Gutters**: 24px on desktop, 16px on mobile

### Spacing Scale

A semantic spacing system with three axes:

**Gap** — Space between sibling elements:
| Token | Value | Use Case |
|-------|-------|----------|
| `gap-min` | 4px | Tight groupings, inline elements |
| `gap-narrow` | 8px | Related items, icon + label |
| `gap-smaller` | 12px | Form fields |
| `gap-default` | 16px | Standard component spacing |
| `gap-larger` | 24px | Section breaks |
| `gap-max` | 48px | Major section divisions |

**Horizontal** — Inline padding:
| Token | Value | Use Case |
|-------|-------|----------|
| `horizontal-min` | 2px | Micro adjustments |
| `horizontal-smaller` | 16px | Compact components |
| `horizontal-default` | 24px | Standard padding |

**Vertical** — Block padding:
| Token | Value | Use Case |
|-------|-------|----------|
| `vertical-min` | 2px | Micro adjustments |
| `vertical-smaller` | 8px | Compact components |
| `vertical-default` | 12px | Standard padding |
| `vertical-larger` | 16px | Generous padding |
| `vertical-max` | 24px | Section padding |

### Breakpoints

| Name | Width | Context |
|------|-------|---------|
| `detailedMobile` | 640px | Small tablets |
| `defaultDesktop` | 800px | Standard desktop breakpoint |
| `detailedDesktop` | 960px | Wide desktop |
| `detailedDesktopWide` | 1272px | Full desktop experience |

## Elevation & Depth

Elevation is conveyed through box shadows rather than color changes. The shadow scale creates a clear sense of depth:

| Token | Value | Use Case |
|-------|-------|----------|
| `weak` | 0px 1px 2px rgba(0,0,0,0.12) | Subtle cards |
| `default` | 0px 1px 8px rgba(0,0,0,0.16) | Standard elevation |
| `default-active` | 0px 4px 16px rgba(0,0,0,0.16) | Hover/active states |
| `moderate-mobile` | 0px 9px 8px -8px rgba(0,0,0,0.16) | Directional shadow (mobile) |
| `moderate-desktop` | 0px 16px 16px -16px rgba(0,0,0,0.16) | Directional shadow (desktop) |
| `strong-desktop` | 0px 4px 14px rgba(0,0,0,0.2) | Prominent elevation |
| `elevated` | 0px 36px 36px rgba(0,0,0,0.3) | Modals, overlays |
| `sticky-bottom` | 0px -4px 8px rgba(0,0,0,0.16) | Bottom-anchored elements |
| `onmap` | 0px 1px 8px rgba(0,0,0,0.16) | Map markers |

### Z-Index Layers

A structured layer system prevents stacking conflicts:

| Layer | z-index | Use Case |
|-------|---------|----------|
| `1-bottom` | 10 | Non-interactive absolute elements |
| `2-banners` | 20 | Promotional banners |
| `3-belowNavigation` | 25 | Above banners, below nav |
| `4-menus` | 30 | Dropdowns, popovers, drawers |
| `5-topBar` | 50 | Main navigation |
| `6-belowModals` | 55 | Toast notifications |
| `7-modals` | 60 | Modal dialogs |
| `8-nestedModals` | 65 | Modals within modals |
| `9-blockers` | 70 | Third-party overlays (Braze) |
| `10-aboveEverything` | 80 | Global errors |

## Shapes

The shape language uses rounded corners to convey friendliness while maintaining clarity:

| Token | Value | Use Case |
|-------|-------|----------|
| `weak` | 8px | Subtle rounding, small elements |
| `moderate` | 12px | Tags, chips |
| `default` | 16px | Buttons, cards, inputs |
| `strong` | 24px | Prominent containers |
| `round` | 9999px | Pills, circular buttons, avatars |

### Control Sizes

Standard heights for interactive elements:
- **Button**: 48px
- **Input**: 48px
- **Search form**: 56px

### Avatar Sizes

| Size | Dimension | Use Case |
|------|-----------|----------|
| `xxs` | 20px | Inline mentions |
| `xs` | 24px | Compact lists |
| `s` | 40px | List items |
| `m` | 48px | Standard display |
| `l` | 96px | Profile headers |
| `xl` | 156px | Profile pages |

### Icon Sizes

| Size | Dimension |
|------|-----------|
| `min` | 16px |
| `s` | 18px |
| `default` | 24px |
| `m` | 32px |
| `l` | 40px |
| `xl` | 48px |
| `xxl` | 56px |
| `max-mobile` | 96px |
| `max-desktop` | 104px |

## Components

Component tokens define consistent styling for common UI elements. Use token references to maintain design coherence.

### Buttons

Primary buttons use the accent color for maximum visibility. Secondary buttons use neutral backgrounds with accent text. All buttons share the same height (48px) and corner radius (16px).

### Inputs

Form inputs maintain a consistent 48px height with default rounded corners. The neutral background provides contrast for text while the accent border indicates focus.

### Cards

Cards use an elevated background (`neutral-bg-elevated`) with a subtle border (`neutral-border-default`) and default corner radius. **Spacing is not embedded in the Card component** — content containers handle their own padding. Cards support multiple states: selected (accent border), disabled (muted border), interactive (accent border on hover), and semantic accent (accent-bg-weak background).

## Do's and Don'ts

- **Do** use the accent color only for the primary action per screen
- **Do** maintain WCAG AA contrast ratios (4.5:1 for normal text, 3:1 for large text)
- **Do** use semantic color tokens (`success`, `danger`) rather than raw hex values
- **Do** test layouts across all breakpoints
- **Don't** mix rounded and sharp corners in the same view
- **Don't** use `body-too-small-mobile` except as an absolute last resort
- **Don't** rely on color alone to convey information — always include text or icons
- **Don't** use `neutral-bg-moderate` for backgrounds — use accent semantic instead
