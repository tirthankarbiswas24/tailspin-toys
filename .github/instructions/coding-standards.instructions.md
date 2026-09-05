---
description: 'Shared coding, commenting, documentation, and TypeScript formatting standards'
applyTo: '**/*.{ts,astro,css}'
---

# Coding Standards

## Comments and Documentation

- Comment **why** code exists: document intent, invariants, trade-offs, and non-obvious decisions.
- Do not add comments that merely restate what the next line or small block already says.
- Keep comments accurate. Update or remove a comment when the related code changes; stale documentation is a bug.
- Prefer the clearest code over explanatory comments for straightforward control flow.

### Data-layer API documentation

Every exported function in `db/` and `src/lib/` must have a TSDoc/JSDoc block that:

- Summarizes the function's purpose.
- Documents every parameter with `@param`, including the injectable `db` argument.
- Documents the return value with `@returns`, including meaningful `null` or empty-collection behavior.

Document exported types when their purpose or constraints are not obvious from their names. Keep implementation comments focused on decisions rather than mechanics.

```ts
/**
 * Returns all games in stable title order for static page generation.
 *
 * @param db - Injectable Drizzle database used by pages and tests.
 * @returns Games mapped to the app-facing shape.
 */
export async function getAllGames(db: Database): Promise<Game[]> {
  // ...
}
```

### Astro component contracts

Every reusable `.astro` component must define and document its `Props` interface in frontmatter. Each property needs a short description when its purpose, optionality, or expected format is not self-evident.

```astro
---
interface Props {
  /** Page title shown in the document head. */
  title: string;
}
---
```

Page-only `Props` interfaces should still be typed; document them when they form a meaningful contract or contain non-obvious values.

## TypeScript Formatting

- Follow the repository's existing indentation and quote conventions; use semicolons.
- Include trailing commas in multiline lists, objects, imports, and function parameters.
- Use one statement per line and keep braces/spaces consistent with the surrounding code.
- Prefer explicit parameter and return types for exported functions and data-layer helpers.
- Run ESLint after TypeScript changes. The repository ESLint configuration enforces semicolons and trailing commas in multiline constructs for `.ts` files.
- Do not introduce a formatter or reformat unrelated files as part of a focused change.
