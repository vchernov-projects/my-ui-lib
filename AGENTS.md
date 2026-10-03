# AGENTS.md

Instructions for AI coding agents.
For project overview, commands, and architecture, see `README.md`.

## Code Style

- Do not hand-format code. Run `npm run fmt` after changes and `npm run lint` to verify.
- Follow `.editorconfig` and the existing ESLint/Prettier setup. Do not add style overrides.

## Adding New Components

1. Create the component file in `src/components/` using a const + separate named export pattern:

```tsx
import React from "react";

const MyComponent = () => {
  return <div>My component</div>;
};

export { MyComponent };
```

2. Create a corresponding `.stories.tsx` file in the same directory.
   - Import types from `@storybook/react-vite` (not `@storybook/react`) to satisfy ESLint rules.
3. Export the component from `src/index.ts` using the pattern:
   `export { MyComponent } from "./components/MyComponent";`
4. Run `npm run build` to ensure both JS and type declarations are generated correctly.
