# **Atlassian Design System Token Reference**

This document provides a comprehensive list of design tokens in the Atlassian Design System. Tokens are the single source of truth for all stylistic values. Always use the JS syntax (e.g., color.text) with the token() helper function from @atlaskit/tokens or directly in the xcss prop of a primitive component.

## **1\. Token Usage Rules & Standards**

### **Core Principles**

* **Strict Usage**: You must **ONLY** use tokens listed in the official system. Do not make up values or use hardcoded hex codes, as this breaks theme support (Dark Mode).  
* **Token Pairing**: Match foreground and background colors correctly. For example, when using a bold background color like color.background.brand.bold, always use color.text.inverse for text to ensure accessible contrast.  
* **Semantic Naming**: Always prefer the semantically correct token name (e.g., color.background.danger) even if a neutral color looks similar. This ensures the UI adapts correctly to different contexts.  
* **Interactive States**: Always provide visual feedback for interactions using the .hovered and .pressed variants of the base token.

## **2\. Color Tokens**

### **Text**

| Token Name (JS Syntax) | CSS Variable | Intended Usage |
| :---- | :---- | :---- |
| color.text | \--ds-text | Primary text color. |
| color.text.subtle | \--ds-text-subtle | Secondary text (captions, helper text). |
| color.text.subtlest | \--ds-text-subtlest | Tertiary text (least emphasis). |
| color.text.disabled | \--ds-text-disabled | Text in a disabled state. |
| color.text.inverse | \--ds-text-inverse | Text on bold/dark backgrounds. |
| color.text.brand | \--ds-text-brand | Text for brand elements. |
| color.text.selected | \--ds-text-selected | Text for selected elements. |
| color.text.danger | \--ds-text-danger | Critical or error text. |
| color.text.warning | \--ds-text-warning | Warning state text. |
| color.text.warning.inverse | \--ds-text-warning-inverse | Warning text on bold backgrounds. |
| color.text.success | \--ds-text-success | Success state text. |
| color.text.discovery | \--ds-text-discovery | New feature/discovery text. |
| color.text.information | \--ds-text-information | Information/in-progress text. |

### **Link**

| Token Name (JS Syntax) | Intended Usage |
| :---- | :---- |
| color.link | Default link color. |
| color.link.pressed | Pressed link color. |
| color.link.visited | Visited link color. |
| color.link.visited.pressed | Pressed visited link color. |

### **Icon**

| Token Name (JS Syntax) | Intended Usage |
| :---- | :---- |
| color.icon | Default icon color. |
| color.icon.subtle | Secondary icon color. |
| color.icon.subtlest | Tertiary icon color. |
| color.icon.inverse | Icons on bold/dark backgrounds. |
| color.icon.disabled | Icons in a disabled state. |
| color.icon.selected | Icons for selected elements. |
| color.icon.brand | Brand-colored icons. |
| color.icon.danger | Icons communicating danger or error. |
| color.icon.warning | Icons communicating a warning. |
| color.icon.warning.inverse | Warning icons on bold backgrounds. |
| color.icon.success | Icons communicating success. |
| color.icon.discovery | Discovery/new feature icons. |
| color.icon.information | Information/in-progress icons. |

### **Background**

| Token Name (JS Syntax) | Intended Usage |
| :---- | :---- |
| color.background.neutral | Default neutral backgrounds (at rest, hovered, pressed). |
| color.background.neutral.subtle | Background for transparent elements (at rest, hovered, pressed). |
| color.background.neutral.bold | Vibrant neutral backgrounds (at rest, hovered, pressed). |
| color.background.brand.bold | Brand actions with high emphasis (at rest, hovered, pressed). |
| color.background.brand.boldest | Brand actions with extreme emphasis (at rest, hovered, pressed). |
| color.background.brand.subtlest | Brand elements with low emphasis (at rest, hovered, pressed). |
| color.background.danger | Subtle backgrounds for critical info (at rest, hovered, pressed). |
| color.background.danger.bold | Vibrant danger backgrounds (at rest, hovered, pressed). |
| color.background.warning | Subtle backgrounds for caution (at rest, hovered, pressed). |
| color.background.warning.bold | Vibrant warning backgrounds (at rest, hovered, pressed). |
| color.background.success | Subtle backgrounds for success (at rest, hovered, pressed). |
| color.background.success.bold | Vibrant success backgrounds (at rest, hovered, pressed). |
| color.background.discovery | Subtle backgrounds for new info (at rest, hovered, pressed). |
| color.background.discovery.bold | Vibrant discovery backgrounds (at rest, hovered, pressed). |
| color.background.information | Subtle backgrounds for informative (at rest, hovered, pressed). |
| color.background.information.bold | Vibrant information backgrounds (at rest, hovered, pressed). |
| color.background.selected | Background for selected states (at rest, hovered, pressed). |
| color.background.selected.bold | Vibrant selected backgrounds (at rest, hovered, pressed). |
| color.background.input | Background for form inputs (at rest, hovered, pressed). |
| color.background.disabled | Background for disabled elements. |
| color.background.inverse.subtle | Overlay on bold backgrounds. |

### **Accent Backgrounds**

Used for non-semantic decorative emphasis. Available in subtlest, subtler, subtle, and bolder variants (including .hovered and .pressed states).

| Accent Color | Token Prefix |
| :---- | :---- |
| Lime | color.background.accent.lime.\* |
| Red | color.background.accent.red.\* |
| Orange | color.background.accent.orange.\* |
| Yellow | color.background.accent.yellow.\* |
| Green | color.background.accent.green.\* |
| Teal | color.background.accent.teal.\* |
| Blue | color.background.accent.blue.\* |
| Purple | color.background.accent.purple.\* |
| Magenta | color.background.accent.magenta.\* |
| Gray | color.background.accent.gray.\* |

### **Border**

| Token Name (JS Syntax) | Intended Usage |
| :---- | :---- |
| color.border | Default border color for containers. |
| color.border.bold | Emphasized borders (min 3:1 contrast). |
| color.border.brand | Brand-colored borders. |
| color.border.danger | Borders for error states. |
| color.border.disabled | Borders for disabled elements. |
| color.border.discovery | Borders for new feature info. |
| color.border.focused | Borders for focused states (keyboard nav). |
| color.border.information | Borders for in-progress info. |
| color.border.input | Specific border for form inputs. |
| color.border.inverse | Borders used on bold/dark surfaces. |
| color.border.selected | Borders for selected elements. |
| color.border.success | Borders for success/validated states. |
| color.border.warning | Borders for caution info. |

### **Interaction, Blanket & Skeleton**

| Token Name (JS Syntax) | Intended Usage |
| :---- | :---- |
| color.interaction.hovered | Hover overlay (e.g. for avatars). |
| color.interaction.pressed | Pressed overlay (e.g. for avatars). |
| color.interaction.inverse.hovered | Hover overlay for bold/inverse surfaces. |
| color.interaction.inverse.pressed | Pressed overlay for bold/inverse surfaces. |
| color.blanket | Screen overlay for modal dialogs. |
| color.blanket.selected | Overlay for selected states. |
| color.blanket.danger | Overlay for danger states. |
| color.skeleton | Base color for loading skeleton states. |
| color.skeleton.subtle | Pulse/shimmer effect for skeletons. |

### **Charts (Categorical & Semantic)**

| Token Name (JS Syntax) | Intended Usage |
| :---- | :---- |
| color.chart.categorical.1 to .8 | Discrete colors for data visualization. |
| color.chart.brand | Primary brand color for charts. |
| color.chart.neutral | Secondary color or "to-do" status. |
| color.chart.danger | Negative info (e.g. "off track"). |
| color.chart.warning | Caution (e.g. "at risk"). |
| color.chart.success | Positive info (e.g. "on track"). |
| color.chart.discovery | "New" status info. |
| color.chart.information | Low priority or in-progress info. |

## **3\. Layout & Shape Tokens**

### **Spacing**

Base unit is space.100 (8px).

| Token Name | Value (px) | Usage |
| :---- | :---- | :---- |
| space.0 | 0px | Reset default spacing. |
| space.025 | 2px | Small/Compact UI. |
| space.050 | 4px |  |
| space.075 | 6px |  |
| space.100 | 8px | Standard base unit. |
| space.150 | 12px | Less dense UI. |
| space.200 | 16px |  |
| space.250 | 20px |  |
| space.300 | 24px |  |
| space.400 | 32px | Layout elements. |
| space.500 | 40px |  |
| space.600 | 48px |  |
| space.800 | 64px | Largest UI gaps. |
| space.1000 | 80px |  |

Negative Spacing  
| Token Name | Value (px) | Usage |  
| :--- | :--- | :--- |  
| space.negative.025 | \-2px | |  
| space.negative.050 | \-4px | |  
| space.negative.075 | \-6px | |  
| space.negative.100 | \-8px | Negate parent whitespace. |  
| space.negative.150 | \-12px | |  
| space.negative.200 | \-16px | |  
| space.negative.250 | \-20px | |  
| space.negative.300 | \-24px | |  
| space.negative.400 | \-32px | |

### **Border Width & Radius**

| Token Name | Value | Usage |
| :---- | :---- | :---- |
| border.width | 1px | Default border/divider width. |
| border.width.selected | 2px | Width for active/selected items. |
| border.width.focused | 2px | Focus ring width. |
| radius.xsmall | 2px | Small detail elements: badges, checkboxes, avatar labels, keyboard shortcuts. |
| radius.small | 4px | Supporting elements: labels, lozenges, timestamps, tags, dates, tooltip containers. |
| radius.medium | 6px | Interactive elements: buttons, inputs, text areas, selects, navigation items, smart links. |
| radius.large | 8px | Containment elements: cards, in-page containers, floating UI, dropdown menus. |
| radius.xlarge | 12px | Large page elements: full-page containers, large containers, modals, Kanban columns, tables. |
| radius.xxlarge | 16px | Video player containers. |
| radius.full | 999px | Circular elements (user/people related): avatars, names, user-related UI, emoji reactions. |
| radius.tile | 25% | Tile component system only. |
| radius.focus.xsmall | 4px | Focus ring for xsmall radius elements (2px offset). |
| radius.focus.small | 6px | Focus ring for small radius elements (2px offset). |
| radius.focus.medium | 8px | Focus ring for medium radius elements (2px offset). |
| radius.focus.large | 10px | Focus ring for large radius elements (2px offset). |
| radius.focus.xlarge | 14px | Focus ring for xlarge radius elements (2px offset). |
| radius.focus.xxlarge | 18px | Focus ring for xxlarge radius elements (2px offset). |

### **Elevation & Shadows**

| Token Name | Usage |
| :---- | :---- |
| elevation.surface | Baseline flat UI surface with no visual lift. Used for body content (e.g., Confluence pages). Supports .hovered and .pressed states. |
| elevation.surface.sunken | Lowest elevation creating a backdrop or well for other content (e.g., Kanban board columns). **Only use on default surface level**, not on raised or overlay elevations. |
| elevation.surface.raised | Sits slightly higher than default elevations. Reserved for movable cards (Jira/Trello cards) or emphasis. **Always pair with elevation.shadow.raised**. Supports .hovered and .pressed states. |
| elevation.surface.overlay | Highest elevation for UI layered over other UI (modals, dialogs, dropdown menus, floating toolbars, FABs). **Always pair with elevation.shadow.overlay**. Can stack on other overlays. Supports .hovered and .pressed states. |
| elevation.shadow.raised | Shadow for cards and panels. **Must be paired with elevation.surface.raised**. Critical for dark mode differentiation. |
| elevation.shadow.overlay | Shadow for floating menus, modals, and overlays. **Must be paired with elevation.surface.overlay**. |
| elevation.shadow.overflow | Indicates scrolled content has moved outside a view (vertical or horizontal). Applied at content cut-off points. |
| elevation.shadow.overflow.perimeter | Perimeter shadow fallback when box shadows aren't technically feasible. |
| elevation.shadow.overflow.spread | Spread shadow fallback when box shadows aren't technically feasible. |

**Dark Mode Note**: In dark mode, elevated surfaces use lighter colors in addition to shadows for differentiation between layers, as shadows can be harder to see.

## **4\. Typography Tokens**

### **Heading & Body**

| Token Name | Size (rem/px) | Line Height | Intended Usage |
| :---- | :---- | :---- | :---- |
| font.heading.xxlarge | 2rem / 32px | 2.25rem / 36px | Brand and marketing content, page titles, promotions. |
| font.heading.xlarge | 1.75rem / 28px | 2rem / 32px | Page titles in apps (e.g., forms). |
| font.heading.large | 1.5rem / 24px | 1.75rem / 28px | Page titles and large components with ample space. |
| font.heading.medium | 1.25rem / 20px | 1.5rem / 24px | Component titles (e.g., in modals). |
| font.heading.small | 1rem / 16px | 1.25rem / 20px | Titles in space-constrained components. |
| font.heading.xsmall | 0.875rem / 14px | 1.25rem / 20px | Secondary headings. |
| font.heading.xxsmall | 0.75rem / 12px | 1rem / 16px | Fine print headings. |
| font.body.large | 1rem / 16px | 1.5rem / 24px | Long-form content for comfortable reading (blogs, articles). |
| font.body | 0.875rem / 14px | 1.25rem / 20px | Default UI text and descriptive content. |
| font.body.small | 0.75rem / 12px | 1rem / 16px | Secondary or fine print content. Avoid sizes smaller than 12px. |

### **Metric, Code & Weight**

| Token Name | Size (rem/px) | Line Height | Intended Usage |
| :---- | :---- | :---- | :---- |
| font.metric.large | 1.75rem / 28px | 2rem / 32px | Emphasizing numbers in large visualizations. |
| font.metric.medium | 1.5rem / 24px | 1.75rem / 28px | Emphasized numeric values in medium contexts. |
| font.metric.small | 1rem / 16px | 1.25rem / 20px | Smaller numeric emphasis in tiles. |
| font.code | 0.875em / 12px | 20px | Monospaced code snippets and inline code. |
| font.weight.regular | - | - | Default font weight (400). |
| font.weight.medium | - | - | Text next to icons, subtle emphasis (500). |
| font.weight.semibold | - | - | Emphasized text (600). |
| font.weight.bold | - | - | Strong emphasis, headings default weight (700). |
| font.family.heading | - | - | Default UI heading typeface. |
| font.family.body | - | - | Default UI body typeface. |
| font.family.code | - | - | Monospaced code typeface. |
| font.family.brand.heading | - | - | Brand heading typeface. |
| font.family.brand.body | - | - | Brand body typeface. |

#### **Works cited**

1. Atlassian Design System Tokens Documentation.  
2. Atlassian Design System Content & Accessibility Foundations.