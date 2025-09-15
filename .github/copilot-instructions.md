# Copilot Instructions for Mimir

## Project Overview
This is a SvelteKit application called "Mimir" using Svelte 5, TailwindCSS 4, TypeScript, and Vitest for testing. It's configured for Node.js deployment with a modern ESM-based build system.

## Tech Stack & Key Dependencies
- **Frontend**: Svelte 5 with SvelteKit for full-stack routing
- **Styling**: TailwindCSS 4 (latest) with Vite plugin integration
- **Testing**: Vitest with browser testing via Playwright for Svelte components
- **Build**: Vite 7 with SvelteKit integration
- **Deployment**: Node.js adapter (`@sveltejs/adapter-node`)
- **Code Quality**: ESLint 9 + Prettier with Svelte-specific configs

## File Structure Patterns
```
src/
├── routes/           # SvelteKit file-based routing
│   ├── +layout.svelte   # Root layout with favicon import
│   └── +page.svelte     # Route pages
├── lib/              # Shared utilities (use $lib alias)
│   ├── index.ts         # Library exports
│   └── assets/          # Static assets (SVG icons, etc.)
├── app.html          # HTML template with SvelteKit placeholders
└── app.css           # Global styles
```

## Development Commands
- `npm run dev` - Start development server
- `npm run build` - Production build
- `npm run test:unit` - Run all tests (watch mode)
- `npm run test` - Run tests once (CI mode)
- `npm run check` - TypeScript + Svelte type checking
- `npm run lint` - ESLint + Prettier validation

## Testing Architecture
**Dual testing setup** with separate environments:
- **Client tests**: `*.svelte.{test,spec}.{js,ts}` run in browser (Playwright)
- **Server tests**: `*.{test,spec}.{js,ts}` run in Node.js environment

Use `vitest-browser-svelte` for component testing:
```typescript
import { render } from 'vitest-browser-svelte';
import { page } from '@vitest/browser/context';
// Component testing with real DOM
```

## Key Conventions
- **Svelte 5 syntax**: Use `$props()` for component props, `{@render children?.()}` for slots
- **Import paths**: Use `$lib` alias for library imports (e.g., `import favicon from '$lib/assets/favicon.svg'`)
- **TailwindCSS**: V4 with Vite plugin, no separate config file needed
- **TypeScript**: Strict mode enabled, extends SvelteKit's generated tsconfig
- **ESLint**: No `no-undef` rule (TypeScript handles this), includes Svelte-specific rules

## Build Configuration Notes
- **Vite config**: Includes TailwindCSS plugin and dual test project setup
- **Svelte config**: Uses `vitePreprocess()` and Node.js adapter
- **ESLint**: Modern flat config with TypeScript, Svelte, and Prettier integration
- **Package.json**: ESM type, all dev dependencies (no runtime deps yet)

## Development Patterns
- Routes use SvelteKit's file-based routing (`+page.svelte`, `+layout.svelte`)
- Global styles imported in root layout (`+layout.svelte`)
- Assets managed through `$lib/assets/` with proper imports
- Component tests should test actual DOM behavior, not implementation details