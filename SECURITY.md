# Security Policy

## Purpose

This is a **demo repository** designed for testing [Dependabot](https://docs.github.com/en/code-security/dependabot) security and version updates. It intentionally contains outdated dependencies to demonstrate Dependabot's capabilities.

## Reporting a Vulnerability

If you discover a security vulnerability in this repository's infrastructure (workflows, configurations), please report it by [opening an issue](https://github.com/xuqun123/dependabot-demo/issues/new).

**Note:** Vulnerabilities in the demo dependencies (e.g., `javascript/` and `ruby/` directories) are expected and intentional — they exist to demonstrate Dependabot's detection and remediation features.

## Supported Versions

| Component | Supported |
| --------- | --------- |
| GitHub Actions workflows | Yes |
| Demo dependencies | No (intentionally outdated) |

## Security Best Practices for Forks

When forking this repository for learning purposes:

1. **Enable Dependabot** security updates in your fork's Settings > Code security
2. **Review and merge** Dependabot PRs to practice the remediation workflow
3. **Do not use** the demo dependencies in production applications
