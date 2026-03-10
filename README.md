# Style Token Adaptation (Svelte 5)

This project demonstrates an adaptation of Ethan Gardner's Web Component style token approach to **Svelte 5** and **SvelteKit**. It implements a hierarchical design system using CSS Custom Properties (tokens) to ensure visual consistency while allowing for granular component-level overrides.

## Core Intent

The primary goal is to show how to structure CSS tokens in a modern Svelte application to support:
- **System-level constants**: Foundation colors, spacing, and typography.
- **Theme-level aliases**: Semantic tokens for backgrounds, text colors, and spacing.
- **Component-level tokens**: Public APIs for component-specific overrides.
- **Local overrides**: Using CSS Custom Properties to "pierce" component scoping without complex prop drilling.
- **Dark mode support**: Automatic theme switching using `prefers-color-scheme` and token reassignment.
- **Dynamic hover states**: Using OKLCH relative color syntax for lightness-aware hover effects.

## Critical Files

### Design System & Tokens
- **`src/lib/styles/system.css`**: Defines the foundational system tokens (colors, sizes, fonts). These are the primitive values.
- **`src/lib/styles/theme.css`**: Maps system tokens to semantic theme variables (e.g., `--eg-t-body-background`). Handles light/dark mode logic.
- **`src/lib/styles/app.css`**: The main entry point that organizes styles into `@layer system, theme`.

### Components
- **`src/lib/components/StepIndicator.svelte`**: A navigation component demonstrating status-based color tokens.
- **`src/lib/components/Button.svelte`**: A flexible button component using OKLCH for lightness manipulation on hover (darker in light mode, lighter in dark mode).

### Routing & Showcase
- **`src/routes/+page.svelte`**: The main demo page showcasing default component usage and local token overrides for specialized theming.
- **`src/routes/+layout.svelte`**: The root layout that imports global styles and manages the document head.

## Development

```bash
npm install
npm run dev
```

Run `npx svelte-check` to verify TypeScript and Svelte 5 syntax correctness.
