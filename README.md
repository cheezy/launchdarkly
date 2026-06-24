# LaunchDarkly Plugin for Claude Code

A Claude Code plugin that teaches Claude to generate **correct, testable, and
removable** [LaunchDarkly](https://launchdarkly.com/) feature-flag code, and
gives it tools to scaffold, audit, and retire flags.

It encodes LaunchDarkly best practices so flag-gated code is:

- **Correct** — every evaluation passes a safe default; browser code uses a
  client-side ID, never a server SDK key.
- **Testable** — both the flag-on and flag-off branches are covered before a
  change is done.
- **Removable** — each flag is read at a single boundary behind a stable seam,
  so retiring it is a mechanical edit, not an archaeology project.

> **Status:** v0.1.0. This plugin is built and used **locally only** — it is not
> published to a marketplace.

## Supported SDKs

- **Java** — server-side SDK (`com.launchdarkly:launchdarkly-java-server-sdk`).
- **TypeScript / Node** — server-side SDK (`@launchdarkly/node-server-sdk`).
- **TypeScript / browser** — client-side JS SDK (`launchdarkly-js-client-sdk`).
- **React** — React SDK (`launchdarkly-react-client-sdk`).

## Installation (local only)

This plugin is a standalone, local directory — there is no marketplace entry.
Install it from its local path in Claude Code:

```
/plugin install /path/to/launchdarkly
```

After installing, the skills activate automatically when you work with
LaunchDarkly code, and the commands and agent below become available. Supply
SDK keys via **environment variables / config**, never hardcoded or committed
(see Security).

## What's in this plugin

- **6 skills** — the LaunchDarkly knowledge base (fundamentals + per-SDK +
  structuring + testing).
- **2 commands** — `/ld-scaffold` and `/ld-remove-flag`.
- **1 agent** — `launchdarkly-reviewer`.

## Skills

| Skill | What it covers |
|---|---|
| [`launchdarkly-fundamentals`](skills/launchdarkly-fundamentals/SKILL.md) | SDK-agnostic concepts: flags & variations, evaluation contexts, the safe default value, streaming vs polling & local evaluation, and the flag lifecycle with the design-for-removal principle. The base the other skills build on. |
| [`launchdarkly-java-sdk`](skills/launchdarkly-java-sdk/SKILL.md) | Server-side Java SDK: one shared `LDClient` closed on shutdown, building an `LDContext`, defaulted variations, offline mode, and the `TestData` source. |
| [`launchdarkly-typescript-node`](skills/launchdarkly-typescript-node/SKILL.md) | Server-side Node SDK in TypeScript: `init` + `waitForInitialization`, typed defaulted variations, flush/close, and the `TestData` source. |
| [`launchdarkly-typescript-client`](skills/launchdarkly-typescript-client/SKILL.md) | Browser JS SDK + React SDK: client-side-ID init, `identify`, bootstrapping, streaming, `LDProvider`/`useFlags`/`useLDClient`, and SSR/hydration. |
| [`launchdarkly-flag-structure`](skills/launchdarkly-flag-structure/SKILL.md) | Structuring flag-gated code for cheap removal: single-boundary reads, a stable seam, named constants, a removal note, independently testable branches (Java + TS). |
| [`launchdarkly-testing`](skills/launchdarkly-testing/SKILL.md) | Testing **both** flag states deterministically with no network: Java/JUnit, TS Jest/Vitest, and React via `jest-launchdarkly-mock`. |

## Commands

| Command | What it does |
|---|---|
| [`/ld-scaffold`](commands/ld-scaffold.md) | Scaffold a removable, both-states-tested flag-gated code path. Takes `<flag-key> <java\|typescript> [description]` and generates a single-boundary seam, stub on/off behaviors, a named flag-key constant + removal note, and a both-states test via the `TestData` source. |
| [`/ld-remove-flag`](commands/ld-remove-flag.md) | Safely retire a flag. Takes `<flag-key> <winning-variation>`, collapses single-boundary seams to the winner (inline winner, delete loser, delete the constant), removes branch-only dead tests, and **reports** any usage it cannot safely collapse instead of guessing. |

## Agent

| Agent | What it does |
|---|---|
| [`launchdarkly-reviewer`](agents/launchdarkly-reviewer.md) | Audits a diff or set of files for LaunchDarkly anti-patterns — missing default values, server SDK keys in browser code, scattered (non-single-boundary) reads, missing both-states tests, raw string-literal flag keys, and flags with no removal note — and returns findings grouped by severity. |

## Security

- Supply SDK keys via **environment variables or your config system**, never
  hardcoded literals, and never commit them (`.env` and `*.local` are
  gitignored).
- **Server SDK keys are secrets**; browser/React code must use the **client-side
  ID**. Never embed a server SDK key in a frontend bundle, and never gate
  secret-dependent logic purely on a client-side flag value (those values are
  visible to users).

## Local install validation

The plugin layout was validated against the on-disk component set for v0.1.0:

- `.claude-plugin/plugin.json` is valid JSON (v0.1.0).
- All **6 skills** have valid `name`/`description` frontmatter and are indexed
  above.
- Both **commands** (`/ld-scaffold`, `/ld-remove-flag`) have valid frontmatter
  and are indexed above.
- The **agent** (`launchdarkly-reviewer`) has valid frontmatter and is indexed
  above.

The README component index matches the files on disk one-to-one; there are no
unindexed components and no indexed-but-missing components.

### Follow-ups

- None outstanding for v0.1.0. Future work (a marketplace entry, additional SDK
  languages, or end-to-end install automation) is intentionally out of scope for
  this local-only release.

## License

[MIT](LICENSE) © Jeff Morgan
