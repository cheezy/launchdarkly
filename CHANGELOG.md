# Changelog

All notable changes to the LaunchDarkly plugin will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.1.0]

Initial release of the standalone, local-only LaunchDarkly Claude Code plugin.

### Added

- Repository scaffold: `.claude-plugin/plugin.json` manifest, `skills/`,
  `agents/`, and `commands/` directories, README, LICENSE, and `.gitignore`.
- **Skills (6):**
  - `launchdarkly-fundamentals` — SDK-agnostic concepts: flags & variations,
    evaluation contexts, the safe default value, streaming vs polling & local
    evaluation, and the flag lifecycle with the design-for-removal principle.
  - `launchdarkly-java-sdk` — server-side Java SDK usage.
  - `launchdarkly-typescript-node` — server-side Node SDK usage in TypeScript.
  - `launchdarkly-typescript-client` — browser JS SDK and React SDK usage.
  - `launchdarkly-flag-structure` — structuring flag-gated code for cheap
    removal (single-boundary read, stable seam, named constants, removal note).
  - `launchdarkly-testing` — testing both flag states deterministically in
    Java, TypeScript, and React.
- **Commands (2):**
  - `/ld-scaffold` — scaffold a removable, both-states-tested flag-gated code
    path in Java or TypeScript.
  - `/ld-remove-flag` — safely retire a flag, collapsing the seam to the chosen
    winning variation and reporting non-conforming usages.
- **Agent (1):**
  - `launchdarkly-reviewer` — audits a diff or files for LaunchDarkly
    anti-patterns, grouped by severity.
- Full README with a component index, supported-SDK list, local install
  instructions, and a security section.
