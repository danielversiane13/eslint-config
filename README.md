# @danielversiane13/eslint-config

Shared ESLint flat config, built on top of [`neostandard`](https://github.com/neostandard/neostandard), [`typescript-eslint`](https://typescript-eslint.io/) and [`eslint-plugin-perfectionist`](https://perfectionist.dev/).

## Install

```sh
pnpm add -D eslint @danielversiane13/eslint-config
```

`eslint` is a peer dependency (`>=9 <10`). TypeScript is optional — only needed if you lint `.ts`/`.tsx` files.

## Usage

Create an `eslint.config.mjs` at the root of your project.

**Base config** (any JS/TS project):

```js
import config from '@danielversiane13/eslint-config'

export default config
```

**Node config** (adds Node.js globals on top of the base config):

```js
import config from '@danielversiane13/eslint-config/node'

export default config
```

## What's included

- `@eslint/js` recommended rules
- `typescript-eslint` recommended rules
- `neostandard` (StandardJS-style rules via `@stylistic`), ignoring whatever is in your `.gitignore`
- `eslint-plugin-perfectionist` — `perfectionist/sort-imports` enforces natural, ascending, grouped import ordering, with a blank line between groups (builtin, external, internal, parent, sibling, index, etc.)
- A few `@stylistic` overrides on top of `neostandard`'s defaults:
  - `comma-dangle`: trailing commas on multiline arrays, objects, imports, exports and function parameters
  - `max-len`: 80 columns (warning), ignoring URLs
  - `space-before-function-paren`: space before `(` for anonymous/async-arrow functions, none for named functions
  - `jsx-quotes`: double quotes in JSX attributes

## Overriding rules

Every export is a flat config array, so consuming projects can spread it and append their own overrides — later entries win over earlier ones for the same files:

```js
import config from '@danielversiane13/eslint-config/node'

export default [
  ...config,
  {
    rules: {
      // full rule config, not a partial merge
      'perfectionist/sort-imports': [
        'error',
        {
          type: 'alphabetical',
          order: 'desc',
          newlinesBetween: 0,
        },
      ],
    },
  },
]
```

## Format on save (VS Code)

Install the [ESLint extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) and add to your `settings.json`:

```json
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  }
}
```
