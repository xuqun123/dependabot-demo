# Testing Guide

## Overview

This guide explains how to test Dependabot functionality using this demo repository. While this repository doesn't contain application code to test in the traditional sense, it serves as a testing ground for Dependabot features.

## Prerequisites

Before testing, ensure you have:
- A GitHub account
- A fork of this repository
- Basic understanding of dependency management
- Familiarity with npm (Node.js) and/or Bundler (Ruby)

## Testing Dependabot Security Updates

### Setup

1. Fork the `dependabot-demo` repository to your GitHub account
2. Navigate to your fork's **Settings** → **Code security and analysis**
3. Enable **Dependabot security updates** or **Grouped security updates**

### Test Cases

#### TC-1: Verify Security Alert Detection

**Objective**: Confirm Dependabot identifies known vulnerabilities

**Steps**:
1. Navigate to **Security** → **Dependabot alerts**
2. Wait 5 minutes for initial scan
3. Verify alerts are displayed with severity ratings

**Expected Result**: 
- At least one critical/high severity alert for outdated dependencies
- Alert details include CVE information and affected versions

#### TC-2: Verify Security Update PR Creation

**Objective**: Confirm Dependabot creates pull requests for vulnerabilities

**Steps**:
1. Wait 5 minutes after enabling security updates
2. Navigate to **Pull requests** tab
3. Look for PRs created by `dependabot[bot]`

**Expected Result**:
- PRs with titles like "Bump [package] from [old] to [new] in /[directory]"
- PR description includes security advisory details
- PR shows changed dependency files

#### TC-3: Verify Fix Application

**Objective**: Confirm merging PR resolves the security alert

**Steps**:
1. Review a Dependabot security PR
2. Merge the pull request
3. Return to **Security** → **Dependabot alerts**

**Expected Result**:
- Security alert status changes to "Fixed"
- Alert shows which PR resolved it
- Dependency version updated in repository

## Testing Dependabot Version Updates

### Setup

1. Ensure you have a fork of this repository
2. Navigate to **Insights** → **Dependency Graph**
3. Click the **Dependabot** tab
4. Click **Enable Dependabot**

### Test Cases

#### TC-4: Verify Configuration Loading

**Objective**: Confirm Dependabot reads `.github/dependabot.yml`

**Steps**:
1. After enabling, refresh the Dependabot tab
2. Check for "Last checked" timestamp
3. Verify ecosystems being monitored

**Expected Result**:
- Shows monitoring status for npm, bundler, and github-actions
- Displays configured update schedule (weekly)
- No configuration errors

#### TC-5: Verify Version Update PR Creation

**Objective**: Confirm Dependabot creates PRs for outdated dependencies

**Steps**:
1. Wait for scheduled update cycle (or trigger manually if permitted)
2. Check **Pull requests** tab
3. Review created PRs

**Expected Result**:
- PRs for outdated dependencies in `/javascript` and `/ruby`
- PR titles indicate version bumps
- No security urgency (unless also a security issue)

#### TC-6: Test Update Merging

**Objective**: Verify version updates can be successfully merged

**Steps**:
1. Select a version update PR
2. Review changes to dependency files
3. Merge the pull request
4. Verify CI/CD passes (if configured)

**Expected Result**:
- Dependency file updated to new version
- Lock files regenerated correctly
- No breaking changes introduced

## Testing Custom Configurations

### TC-7: Modify Dependabot Schedule

**Objective**: Test configuration changes

**Steps**:
1. Edit `.github/dependabot.yml` in your fork
2. Change update schedule (e.g., from "weekly" to "daily")
3. Commit changes
4. Monitor Dependabot behavior

**Expected Result**:
- Dependabot respects new schedule
- Update frequency changes accordingly

### TC-8: Test Ignore Rules

**Objective**: Verify dependency ignore functionality

**Steps**:
1. Add ignore rule to `.github/dependabot.yml`:
   ````yaml
   - package-ecosystem: "npm"
     directory: "/javascript"
     schedule:
       interval: "weekly"
     ignore:
       - dependency-name: "lodash"
   ````
2. Commit and wait for next update cycle

**Expected Result**:
- No PRs created for ignored dependency
- Other dependencies still receive updates

## Manual Testing Commands

### JavaScript Project

````bash
cd javascript

# Check for outdated packages
npm outdated

# Check for vulnerabilities
npm audit

# Update specific package
npm update hot-formula-parser

# Install updates
npm install
````

### Ruby Project

````bash
cd ruby

# Check for outdated gems
bundle outdated

# Update specific gem
bundle update business

# Install updates
bundle install
````

## Troubleshooting Tests

### Issue: No Security Alerts Appear

**Possible Causes**:
- Dependabot security updates not enabled
- Dependencies already up-to-date
- GitHub Security Advisory delay

**Solution**:
- Verify settings in **Code security and analysis**
- Check if dependencies are actually vulnerable
- Wait additional time for scanning

### Issue: No Version Update PRs Created

**Possible Causes**:
- Dependabot not enabled via Dependency Graph
- Update schedule not yet triggered
- Configuration file errors

**Solution**:
- Enable Dependabot in **Insights** → **Dependency Graph**
- Check `.github/dependabot.yml` for syntax errors
- Wait for scheduled interval or check job logs

### Issue: PRs Fail CI/CD Checks

**Possible Causes**:
- Breaking changes in new dependency version
- Test failures with updated dependencies
- Build configuration issues

**Solution**:
- Review PR checks and failure logs
- Test dependency updates locally
- Consider pinning to compatible versions

## Continuous Testing

To maintain this demo repository:
- Periodically reset dependencies to outdated versions
- Test new Dependabot features as released
- Verify documentation matches current GitHub UI
- Ensure sample projects remain functional

## Automated Testing

This repository includes GitHub Actions workflows for:
- Repository health scanning
- Dependency monitoring
- Documentation validation

Check `.github/workflows/` for automation details.

## Additional Resources

- [Dependabot Test Repository](https://github.com/dependabot/dependabot-core)
- [GitHub Docs: Testing Dependabot](https://docs.github.com/code-security/dependabot)
- [Security Advisory Database](https://github.com/advisories)
