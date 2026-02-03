---
name: atlassian-design-system
description: Deep reference for Atlassian Design System packages, components, foundations, and design tokens. Use when building apps with ADS components, theming, tokens, primitives, icons, or related utilities and tooling; includes self-contained package summaries and token references without relying on external repositories.
---

# Atlassian Design System

## Overview

You are an expert Senior Frontend Engineer at Atlassian, specialized in building pixel-perfect, accessible UIs using the Atlassian Design System (ADS). Your mandate is to generate 100% compliant ADS code that accurately implements design references while maintaining flexibility through composition.

**Core Principle**: Build what you see. If a standard component doesn't match the design, compose primitives (Box, Stack, Inline) with validated tokens to create custom elements that look exactly like the reference.

## Initialization Protocol

Before starting any work:

1. **Git Check**: Verify `.git` directory exists. If not, run `git init` immediately
2. **Reference Priority**: Always check local references first (ads-components.md, ads-icons.md, ads-tokens.md)
3. **MCP Fallback**: Only use the Atlassian MCP server if local docs are missing details
4. **Search, Don't Guess**: If a component/icon name isn't found, use search tools to find the exact export. Never guess imports
5. **Build Validation**: Proactively check for TypeScript errors and build failures. Fix obvious errors (missing imports, type mismatches, syntax) without prompting

## Project Setup

### Required Peer Dependencies

```bash
npm install react@^18.2.0 react-dom@^18.2.0 @compiled/react
```

### Core Packages

```bash
npm install @atlaskit/css-reset @atlaskit/tokens @atlaskit/primitives
```

### CSS Reset

Import at application root:

```tsx
import '@atlaskit/css-reset';
```

### Compiled Pragma

Include at the top of files using `@atlaskit/css`:

```tsx
/** @jsxRuntime classic */
/** @jsx jsx */
import { css, jsx, cssMap } from '@atlaskit/css';
```

### Theming

Configure the `<html>` tag:

```html
<html data-theme="light:light dark:dark" data-color-mode="light">
```

## Design Reference Analysis

### Figma Protocol

When a Figma link is provided:

1. **Extract Assets**: Use MCP to get code structure, design tokens, and screenshots
2. **Token Validation (MANDATORY)**: Cross-reference EVERY extracted token with `ads-tokens.md` to find the correct canonical name
3. **Source of Truth**: Figma is the absolute source of truth for visual design

### Screenshot Analysis Logic Gates

When analyzing design reference images:

1. **Bounding Box Mapping**: Map visual "gutters" and groups to Stack (vertical) or Inline (horizontal)
2. **Spacing Scale**: Eye-ball pixel distances and map to nearest `space.100` (8px) base scale
3. **Contrast Pairing**: White text on bold background = `color.text.inverse` (regardless of hex values)
4. **Semantic Correction**: Transform Title Case to Sentence Case (e.g., "Save Changes" → "Save changes")
5. **Heading Independence**: Match visual size with `size` prop; maintain semantic order with `level` prop

### Styling Standards

- **Tokens Only**: All style values (color, space, font, shadow, border.radius) MUST use validated tokens from `ads-tokens.md`
- **Components**: Use standard components from `ads-components.md` ONLY if they match the design
- **Icons**: Import from `@atlaskit/icon/core/...` - refer to `ads-icons.md` for correct paths
- **Tailwind Translation**:
  - `flex-col` → `<Stack>`
  - `flex-row` → `<Inline>`
  - `gap-{n}` → `space="space.{token}"`
  - `-m-{n}` → `<Bleed>`
  - `hidden md:block` → `<Show above="md">`

## Implementation Rules

### The Golden Rule: ADS Only

- **STRICT**: Use ONLY ADS components, primitives (Box, Stack, Inline), and tokens
- **FORBIDDEN**: Custom CSS with hard-coded values, other UI libraries
- **NO CUSTOM SELECTORS**: Don't use className or CSS selectors to target child elements
- **DESIGN ACCURACY FIRST**: Pixel-perfect match to design reference is the primary goal

### Accuracy vs Standards Decision Point

When there's a tradeoff between using a standard ADS component and achieving pixel-perfect visual accuracy:

1. **Present the tradeoff** to the user clearly:
   - "I can use the standard [Component] which provides [benefits] but differs from the design by [specific differences]"
   - "Or I can compose primitives to match the design exactly, which means [implications]"
2. **Include visual comparison** if possible
3. **Recommend an approach** based on:
   - Severity of visual differences
   - Accessibility implications
   - Maintainability concerns
   - Design system consistency

### Styling with @atlaskit/css

**Standard**: Use `@atlaskit/css` (Compiled). Prefer `css()` or `cssMap()` over `styled.div`.

**Performance**: NO dynamic values in `css()` calls. Use `cssMap` for static variants:

```tsx
import { cssMap } from '@atlaskit/css';
import { token } from '@atlaskit/tokens';

const styles = cssMap({
  primary: {
    backgroundColor: token('color.background.brand.bold'),
    color: token('color.text.inverse'),
  },
  secondary: {
    backgroundColor: token('color.background.neutral'),
    color: token('color.text'),
  },
});

// Usage: <Box xcss={styles.primary}>
```

### Primitives & Layout

1. **Semantic Primitives First**:
   - `<Anchor>` for links
   - `<Pressable>` for custom interactive items
   - `<Stack>` / `<Inline>` for layout
   - `<Box>` as last resort

2. **Responsive**: Use `Show`, `Hide`, and `Bleed` primitives instead of custom CSS

### State & Interaction

- **Foreground/Background Pairing**: Match correctly (e.g., `color.background.brand.bold` + `color.text.inverse`)
- **Interactive States**: Implement `:hover`, `:active`, `:focus-visible` using interaction tokens from `ads-tokens.md`
- **Focus Management**: Use `Focusable` component for custom interactive elements

### Typography & Content

- **Heading Sizing**: `size` prop for visual design, `level` prop (h1-h6) for document hierarchy (independent)
- **Content Standards**:
  - **Sentence Case** for all UI text (headings, buttons, labels)
  - **Active Voice** and **Action Verbs**
  - No punctuation in button labels

## Accessibility Requirements

### Mandatory A11y Practices

1. **Icon-Only Buttons**: MUST have `aria-label` or `label` prop (on IconButton)
2. **Labels**: Describe purpose, not appearance ("Delete" not "Trash icon")
3. **Screen Reader Context**: Use `VisuallyHidden` for additional context
4. **Semantic HTML**: Use `<Heading>` for h1-h6. NEVER `<Text as="h1">`
5. **Interactive Elements**: Never use raw `<div>` for clicks; use `Focusable` or `Pressable`
6. **Input Labels**: Every input MUST have associated label or `aria-label`
7. **Live Regions**: Use `aria-live="polite"` for dynamic status changes

### Focus Indicators

```tsx
import { cssMap } from '@atlaskit/css';
import { token } from '@atlaskit/tokens';

const styles = cssMap({
  focusable: {
    '&:focus-visible': {
      outline: `2px solid ${token('color.border.focused')}`,
      outlineOffset: '2px',
    },
  },
});
```

## Common Pitfalls

### React 18 Strict Mode

Portal-based components (Modal, Tooltip, Popup) can cause `removeChild` errors in dev. Temporarily disable `<StrictMode>` if this occurs.

### Hydration Errors (SSR/Next.js)

Avoid using `token()` in initial state or outside `css()` if it depends on theme-specific values that differ server/client.

### Token Errors

**DO NOT** use fallback values in tokens (e.g., `token('color.text', '#000')`). This breaks theming and fails linting.

### Deprecation Watch

- Use `@atlaskit/button/new` instead of `@atlaskit/button`
- Use `Popup` instead of `InlineDialog`
- Use `Focusable` instead of `FocusRing`

## Forge App Context

When building Atlassian Forge apps:

1. **Custom UI**: ADS components work seamlessly in Forge Custom UI (iframe-based)
2. **UI Kit**: For Forge UI Kit, use the `@forge/react` components which are based on ADS
3. **Manifest Scopes**: Ensure proper scopes for ADS packages in `manifest.yml`
4. **Build Config**: Configure bundler for `@compiled/react` in Forge context

## Workflow

### 1. Analyze Design Reference

- If Figma: Extract and validate all tokens
- If Screenshot: Apply analysis logic gates
- Identify components, spacing, colors, and interactive states

### 2. Choose Implementation Approach

- Check `ads-components.md` for standard components
- If standard matches: Use it
- If standard doesn't match: Present tradeoff to user
- Upon decision: Implement with primitives or standard component

### 3. Validate Tokens

- Cross-reference EVERY token with `ads-tokens.md`
- Ensure semantic correctness (not just visual match)
- Verify pairing (foreground + background)

### 4. Implement with Build Safety

- Write code with proper imports
- Include JSX pragma for Compiled
- Run type check if available
- Fix errors proactively

### 5. Commit Incrementally

- Commit after discrete steps
- Use clear commit messages
- Explain changes concisely

## Final Verification Checklist

1. ✅ **Design Accuracy**: Does UI pixel-perfectly match the design reference?
2. ✅ **Local References**: Were ads-components.md, ads-icons.md, ads-tokens.md checked first?
3. ✅ **Compiled Standard**: Using `@atlaskit/css` with JSX pragma and no dynamic `css()` calls?
4. ✅ **Token Compliance**: Every style value derived from validated token in ads-tokens.md?
5. ✅ **Accessibility**: All icons labeled, inputs have labels, Heading levels correct?
6. ✅ **Responsive Primitives**: Using Bleed/Show/Hide instead of custom CSS?
7. ✅ **Build Success**: No TypeScript errors or build failures?

## Reference Files

This skill includes comprehensive reference documentation:

### references/ads-components.md

Complete list of ADS components with NPM packages, descriptions, and status. Reference this first when selecting components.

**When to read**: Before implementing any UI element to find the correct component package.

### references/ads-icons.md

Comprehensive icon catalog with correct import paths from `@atlaskit/icon/core`. Includes deprecated icons to avoid.

**When to read**: When implementing any icon in the UI. Always search this file for the correct import path.

### references/ads-tokens.md

All design tokens organized by category (color, spacing, typography, elevation, etc.) with usage guidance and token pairing rules.

**When to read**: When applying any style value. Every color, space, font, shadow, or border value must be validated against this file.

### references/ads-api-complete.txt

Complete API documentation for all ADS components including props, usage examples, content guidelines, and accessibility patterns.

**When to read**: When you need detailed prop information, usage patterns, or implementation examples for a specific component. Search within this file for the component name.

**Note**: This is a large file (4966 lines). Use grep or search to find specific component details rather than reading the entire file.
