# How This Repository Works

## Overview

The **Dependabot Demo** repository is designed to help developers understand and test GitHub's Dependabot features for automated dependency management. It contains sample projects with intentionally outdated dependencies.

## Architecture

### Project Structure

The repository consists of two independent demo projects:

````
dependabot-demo/
├── javascript/    # Node.js project with npm dependencies
└── ruby/          # Ruby project with Bundler dependencies
````

Each project serves as a minimal example to demonstrate Dependabot's capabilities across different ecosystems.

### JavaScript Project

**Location**: `/javascript`  
**Ecosystem**: npm (Node.js)  
**Purpose**: Demonstrates npm dependency management

**Dependencies**:
- `hot-formula-parser`: Formula parsing library
- `lodash`: Utility library

**Configuration**: Uses `package.json` for dependency declarations and `package-lock.json` for version locking.

### Ruby Project

**Location**: `/ruby`  
**Ecosystem**: Bundler (Ruby)  
**Purpose**: Demonstrates Ruby gem management

**Dependencies**:
- `business`: Business day calculations
- `uk_phone_numbers`: UK phone number validation

**Configuration**: Uses `Gemfile` for dependency declarations and `Gemfile.lock` for version locking.

## Dependabot Configuration

Dependabot is configured via `.github/dependabot.yml` with the following update schedules:

| Ecosystem       | Directory     | Update Frequency |
|----------------|---------------|------------------|
| GitHub Actions | `/`           | Weekly           |
| npm            | `/javascript` | Weekly           |
| Bundler        | `/ruby`       | Weekly           |

### How Dependabot Works

1. **Scanning**: Dependabot scans dependency files for known vulnerabilities and outdated versions
2. **Analysis**: Compares current versions against security advisories and latest releases
3. **PR Creation**: Creates pull requests to update dependencies
4. **Grouping**: Can group related updates into single PRs (configurable)

### Types of Updates

#### Security Updates
- **Trigger**: When a vulnerability is detected in a dependency
- **Priority**: High - created immediately when enabled
- **Source**: GitHub Security Advisories and CVE database

#### Version Updates
- **Trigger**: When a new version is available (based on schedule)
- **Priority**: Normal - follows configured schedule
- **Source**: Package registry (npm, RubyGems, etc.)

## Testing Dependabot

### Prerequisites
- Fork this repository to your GitHub account
- Ensure you have maintainer access to your fork

### Enabling Security Updates

1. Go to **Settings** → **Code security and analysis**
2. Enable **Dependabot security updates** (or grouped updates)
3. Navigate to **Security** → **Dependabot alerts**
4. Dependabot will scan and create PRs for vulnerabilities
5. Merge PRs to close security alerts

**Expected Results**: Within ~5 minutes, you should see:
- Security alerts listed in the Security tab
- Pull requests created to fix vulnerabilities
- Detailed vulnerability information and fix recommendations

### Enabling Version Updates

1. Go to **Insights** → **Dependency Graph**
2. Click the **Dependabot** tab
3. Click **Enable Dependabot**
4. Dependabot reads `.github/dependabot.yml` automatically
5. Version update PRs are created based on the schedule

**Expected Results**: Within a few minutes:
- Dependabot job appears in the Dependency Graph
- Pull requests for outdated dependencies
- Weekly update schedule (per configuration)

## Workflow

### Typical User Journey

1. **Fork** the demo repository
2. **Enable** Dependabot security updates
3. **Wait** ~5 minutes for initial scan
4. **Review** generated pull requests
5. **Merge** PRs to apply fixes
6. **Enable** version updates for ongoing maintenance
7. **Observe** weekly version update PRs

## Maintenance

### Keeping Dependencies Outdated

Since this is a demo repository, dependencies are intentionally kept outdated to showcase Dependabot's capabilities. When merging Dependabot PRs in the upstream repository:

- Consider whether updates serve the demo purpose
- Retain some outdated dependencies for testing
- Balance between demo functionality and security

### Repository Health

This repository includes automated health scanning via GitHub Actions to:
- Monitor for new vulnerabilities
- Check dependency configuration
- Ensure documentation remains current
- Report on repository health metrics

## Learning Resources

- [Dependabot Documentation](https://docs.github.com/code-security/dependabot)
- [Dependabot Configuration Reference](https://docs.github.com/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file)
- [GitHub Security Advisories](https://github.com/advisories)
- [Dependency Graph](https://docs.github.com/code-security/supply-chain-security/understanding-your-software-supply-chain/about-the-dependency-graph)

## FAQ

**Q: Why are dependencies outdated?**  
A: This is intentional to demonstrate Dependabot's update capabilities.

**Q: Should I use this in production?**  
A: No, this is a demo repository. Apply Dependabot learnings to your own projects.

**Q: How often does Dependabot run?**  
A: Security updates run when vulnerabilities are detected. Version updates follow the configured schedule (weekly for this demo).

**Q: Can I customize the update schedule?**  
A: Yes, edit `.github/dependabot.yml` in your fork to change schedules, grouping, and other options.
