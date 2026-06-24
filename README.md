# LaunchDarkly Plugin for Claude Code

A Claude Code plugin that teaches Claude to generate **correct, testable, and
removable** [LaunchDarkly](https://launchdarkly.com/) feature-flag code.

> **Status:** early scaffold (v0.1.0). The manifest and directory skeleton are
> in place; skills, commands, and the review agent are added in subsequent
> tasks. This README is a stub and will be expanded once the plugin's
> capabilities land.

## What it will cover

- **Server-side Java SDK** and the **TypeScript SDKs** — Node server, browser
  client-side JS, and React.
- Structuring flag-gated code behind a **single removable boundary**.
- Always writing tests for **both the flag-on and flag-off branches**.

## Planned capabilities

- Knowledge skills for the LaunchDarkly fundamentals/lifecycle and each SDK.
- A code-structuring skill for removable flag boundaries.
- A testing skill for validating both toggle states.
- A `/ld-scaffold` command for flag-gated code.
- A flag-removal command.
- A review agent that audits code for LaunchDarkly anti-patterns.

## Installation

This is a standalone, local-only plugin (not published to a marketplace).
Install it from a local path in Claude Code once the capabilities are in place.

## License

[MIT](LICENSE) © Jeff Morgan
