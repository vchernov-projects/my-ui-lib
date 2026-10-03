# my-ui-lib

A React component library built with Vite, TypeScript, React 19, and Material UI (MUI) v7.
It is published as an ES module package that other projects can consume.
Storybook is used for component development and documentation.

## Commands

```bash
npm run storybook        # Storybook for component development
npm run build            # Build the library (Vite bundle + type declarations)
npm run build-storybook  # Build Storybook for deployment
npm run lint             # Lint with ESLint
npm run fmt              # Format with Prettier
npm run fmt:check        # Check formatting without writing
npm run dev              # Vite dev server (rarely needed)
npm run preview          # Preview the built library
```

## Code Style

- Formatting is handled by Prettier and `.editorconfig`.
  Run `npm run fmt` before committing.
- Linting is handled by ESLint (`eslint.config.js`). Run `npm run lint`.

## Build

The project uses a dual build:

1. **Vite** bundles the code into `dist/my-ui-lib.es.js` (ES module only).
   React, React-DOM, MUI, and Emotion are external peer dependencies (`vite.config.ts`).
2. **TypeScript** emits type declarations into `dist/types/`.
   Configured in `tsconfig.build.json`, which extends `tsconfig.app.json`.

Package exports in `package.json` point to both the bundle and the type definitions.

## Project Structure

- `src/index.ts`: entry point exporting all public components
- `src/components/`: components with their `.stories.tsx` files
- `.storybook/`: Storybook configuration
  - `main.ts`: core config (stories location, addons, framework)
  - `preview.tsx`: global decorators and parameters (MUI ThemeProvider and CssBaseline)
- `dist/`, `storybook-static/`: generated output, not in source control

## Architecture Notes

- **Peer dependencies**: React and React-DOM (>=19), Material UI, and Emotion are not bundled.
  Consuming projects must install them.
- **Module format**: ES modules only (no CommonJS).
- **TypeScript**: strict mode, with project references for the app (`tsconfig.app.json`),
  node tooling (`tsconfig.node.json`), and Storybook (`tsconfig.storybook.json`).
- **Compilation**: SWC via `@vitejs/plugin-react-swc`.
- **Storybook**: React-Vite framework, with `addon-docs` for automatic documentation.

## Adding a Component

1. Create the component in `src/components/`.
2. Add a `.stories.tsx` file next to it.
3. Export it from `src/index.ts`.
4. Run `npm run build` to verify the bundle and type declarations.
