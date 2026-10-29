# AGENTS.md

Weather CLI app built with Bun + OpenMeteo. Currently a scaffold: `index.ts` only prints a placeholder; the real spec lives in `README.MD` (Spanish).

## Commands

- `bun run index.ts` — run the CLI (no `start`/`dev` script exists)
- `bun run typecheck` — `bun check`, Bun's native TypeScript checker (not `tsc`)
- `bun test` — test runner, but no tests exist yet

There is no lint, formatter, or build script configured. Don't invent one; verify a new script runs before documenting it.

## Toolchain quirks

- ESM (`"type": "module"`) with TypeScript run directly by Bun — no compile step for development.
- TypeScript is v7 (native `tsgo`) via a `peerDependencies` entry; don't switch to `tsc` for checks.
- `tsconfig.json` is strict with `noUncheckedIndexedAccess`, `verbatimModuleSyntax`, and `allowImportingTsExtensions`: relative imports must include `.ts`, and type-only imports must use `import type`.
- `noEmit: true`; final deliverable is a compiled binary (`bun build --compile`), not emitted JS.
- `bun.lock` is the lockfile; use `bun install`, never npm/pnpm lockfiles.

## App conventions

- User-facing strings are Spanish, matching the menu and option names in `README.MD`.
- Weather lookup is two API calls with no key: geocoding first for lat/lon, then forecast. See the example URLs in `README.MD`.
- No config/state layer exists yet; persisted default city and city list still need to be designed (keep them in one module rather than inline in `index.ts`).
