# How This Repo Works

## What It Demonstrates

This repository is a playground for [GitHub Dependabot](https://docs.github.com/en/code-security/dependabot). It contains intentionally outdated dependencies so Dependabot can detect them and open pull requests for **security updates** and **version updates**.

## Project Structure

| Directory | Ecosystem | Dependencies |
|-----------|-----------|-------------|
| `javascript/` | npm | `lodash`, `hot-formula-parser` |
| `ruby/` | Bundler | `business`, `uk_phone_numbers` |

Each directory has its own lock file so Dependabot can track and update packages independently.

## Dependabot Configuration

The file `.github/dependabot.yml` tells Dependabot what to monitor:

- **npm** -- checks `javascript/` weekly for outdated npm packages.
- **bundler** -- checks `ruby/` weekly for outdated Ruby gems.
- **github-actions** -- checks the repo root weekly for outdated GitHub Actions versions.

All three ecosystems are scanned on a **weekly** schedule.

## How to Fork and Enable Dependabot

1. **Fork** this repository to your own GitHub account.
2. Go to **Settings > Code security and analysis**.
3. Enable **Dependabot alerts** and **Dependabot security updates**.
4. Dependabot will start scanning your fork and opening PRs for outdated or vulnerable dependencies.

You can also edit `.github/dependabot.yml` to change the schedule, add ecosystems, or adjust other options. See the [Dependabot docs](https://docs.github.com/en/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file) for all available settings.
