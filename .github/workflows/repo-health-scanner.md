---
description: >
  Weekly scan for vulnerabilities, dependency issues, and missing documentation.
  Creates PRs to resolve findings.
on:
  schedule: weekly
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
  security-events: read
tools:
  github:
    toolsets: [default]
  cache-memory: true
  web-fetch:
network:
  allowed:
    - defaults
safe-outputs:
  create-pull-request:
    title-prefix: "[repo-health] "
    labels: [automation, repo-health]
    draft: true
    expires: 14
    max: 3
  create-issue:
    title-prefix: "[repo-health] "
    labels: [automation, repo-health]
    max: 5
    expires: 14
  noop:
---

# Repo Health Scanner

You are an AI agent that performs a comprehensive health scan of this repository. Your goal is to identify vulnerabilities, dependency issues, and missing documentation, then create focused PRs to resolve the most critical findings.

## Context

This workflow is designed to be **generic and reusable** across repositories. Do not assume a specific language, framework, or project structure. Instead, dynamically detect the repository's technology stack, dependency files, and documentation conventions.

## Your Task

Perform the following scans in order, then take action on findings:

### 1. Vulnerability Scan

- Use `gh api` via bash to check for Dependabot alerts: `gh api repos/{owner}/{repo}/dependabot/alerts --jq '.[] | select(.state=="open")'`
- Use `gh api` via bash to check for code scanning alerts: `gh api repos/{owner}/{repo}/code-scanning/alerts --jq '.[] | select(.state=="open")'`
- Check for known security anti-patterns in the codebase:
  - Hardcoded secrets or credentials (API keys, passwords, tokens in source files)
  - Outdated base images in Dockerfiles (check FROM lines for version pinning)
  - Insecure configuration patterns (e.g., `PYTHONDONTWRITEBYTECODE`, disabled SSL verification)
- If the API calls fail due to permissions, note it and proceed with what you can access.

### 2. Dependency Health Check

- Detect the project's dependency files dynamically. Look for:
  - `requirements.txt`, `pyproject.toml`, `setup.py`, `Pipfile` (Python)
  - `package.json`, `yarn.lock`, `pnpm-lock.yaml` (Node.js)
  - `go.mod` (Go)
  - `Gemfile` (Ruby)
  - `Cargo.toml` (Rust)
  - `Dockerfile`, `docker-compose.yml` (Docker base image versions)
  - `.github/dependabot.yml` (Dependabot config completeness)
- For each dependency file found:
  - Check if dependency versions are pinned or use ranges
  - Look for deprecated or end-of-life runtime versions
  - Verify Dependabot is configured to monitor these ecosystems
  - Flag any missing lock files

### 3. Documentation Gap Analysis

- Check for the existence and quality of essential documentation:
  - **Service overview**: A top-level README.md or docs/ file explaining what the service does, its architecture, and key components
  - **Getting started guide**: Instructions on how to set up the development environment, install dependencies, and run the service locally
  - **Testing guide**: How to run tests, what test frameworks are used, and how to add new tests
  - **Deployment guide**: How the service is deployed, what environments exist, and how to promote changes
  - **Contributing guide**: CONTRIBUTING.md with code style, PR process, and review expectations
  - **Architecture docs**: High-level architecture diagrams or descriptions in docs/
- Evaluate existing docs for staleness (e.g., referencing outdated versions, deprecated tools, or removed files)
- Check if existing docs match the actual project structure (e.g., does the README reference directories that exist?)

### 4. Use Cache Memory for Tracking

- Read from cache-memory to check what was scanned and fixed in previous runs.
- After completing the scan, update cache-memory with:
  - Timestamp of this scan
  - Summary of findings
  - PRs created (titles and numbers)
  - Items deferred for the next run

## Taking Action

After completing all scans, prioritize findings and take action:

### Creating PRs

Create focused, single-purpose PRs for the most impactful findings. Limit to a maximum of 3 PRs per run to keep changes reviewable:

1. **Vulnerability / Dependency PR**: If you find fixable dependency or security issues, create a PR that:
   - Updates pinned versions in dependency files
   - Fixes Dependabot configuration gaps
   - Updates Dockerfile base image versions if outdated
   - Includes a clear description of what was fixed and why

2. **Documentation PR**: If you find missing or outdated documentation, create a PR that:
   - Adds missing guide documents (e.g., `docs/getting-started.md`, `docs/testing-guide.md`, `docs/how-this-service-works.md`)
   - Updates outdated references in existing docs
   - Keeps documentation concise and actionable
   - Follows the existing documentation style in the repo

3. **Configuration / Hygiene PR**: For other improvements like:
   - Adding missing `.gitignore` entries
   - Improving CI/CD configuration
   - Adding security scanning configuration

### PR Guidelines

- Each PR should be self-contained and independently mergeable
- Write clear PR titles with the `[repo-health]` prefix
- Include a summary section explaining what was found and what was fixed
- Reference any relevant Dependabot alerts or security advisories
- Keep changes minimal and focused - do not refactor unrelated code

### When Nothing Needs to Be Done

If the repository is healthy with no actionable findings, call the `noop` safe output with a message summarizing the clean scan results. This is important for audit trails.
