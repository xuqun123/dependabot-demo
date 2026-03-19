# How This Service Works

## Overview

This repository is a **demo project** used to illustrate how [GitHub Dependabot](https://docs.github.com/en/code-security/dependabot) detects and fixes outdated or vulnerable dependencies.

It intentionally includes outdated dependencies across two ecosystems — **npm** (JavaScript) and **Bundler** (Ruby) — so that Dependabot has visible work to do when you fork it.

## Architecture

The repository is intentionally simple. There is no running service or application — it exists purely to demonstrate dependency management tooling.

```
┌─────────────────────────────────────────┐
│            dependabot-demo              │
│                                         │
│  ┌─────────────┐   ┌─────────────────┐  │
│  │  javascript/│   │     ruby/       │  │
│  │  (npm)      │   │  (Bundler)      │  │
│  └─────────────┘   └─────────────────┘  │
│                                         │
│  ┌─────────────────────────────────────┐│
│  │  .github/dependabot.yml             ││
│  │  (monitors npm, bundler, actions)   ││
│  └─────────────────────────────────────┘│
└─────────────────────────────────────────┘
```

## Key Components

| Path | Purpose |
|------|---------|
| `javascript/package.json` | npm dependency manifest with intentionally old packages |
| `ruby/Gemfile` | Bundler manifest with intentionally old gems |
| `.github/dependabot.yml` | Tells Dependabot which ecosystems and directories to scan |
| `.github/workflows/android.yml` | Sample workflow (intentionally uses old action versions) |

## Dependabot Configuration

Dependabot is configured in `.github/dependabot.yml` to monitor three ecosystems weekly:

- **github-actions** — root directory
- **npm** — `/javascript`
- **bundler** — `/ruby`

## Intentional Vulnerabilities

The `hot-formula-parser` npm package (used in `javascript/`) contains a known critical vulnerability ([GHSA-rc77-xxq6-4mff](https://github.com/advisories/GHSA-rc77-xxq6-4mff)). This is intentional — it exists so Dependabot security updates have something to detect and patch.

## Further Reading

- [Dependabot documentation](https://docs.github.com/en/code-security/dependabot)
- [Configuring Dependabot version updates](https://docs.github.com/en/code-security/dependabot/dependabot-version-updates/configuring-dependabot-version-updates)
- [Dependabot security updates](https://docs.github.com/en/code-security/dependabot/dependabot-security-updates/about-dependabot-security-updates)
