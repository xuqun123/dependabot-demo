# Contributing to Dependabot Demo

Thank you for your interest in contributing to the Dependabot Demo repository! This repository serves as a demonstration of Dependabot's dependency management capabilities.

## Purpose

This repository contains intentionally outdated dependencies to showcase Dependabot's security and version update features. It includes:

- **JavaScript project** (`/javascript`) - Node.js dependencies managed by npm
- **Ruby project** (`/ruby`) - Ruby gems managed by Bundler

## Getting Started

### Prerequisites

- **Node.js** (v18 or later) and npm
- **Ruby** (v3.0 or later) and Bundler
- **Git**

### Setup

1. Fork this repository to your GitHub account
2. Clone your fork locally:
   ````bash
   git clone https://github.com/YOUR-USERNAME/dependabot-demo.git
   cd dependabot-demo
   ````

3. Install dependencies:
   ````bash
   # JavaScript project
   cd javascript
   npm install
   
   # Ruby project
   cd ../ruby
   bundle install
   ````

## Testing Dependabot

### Security Updates

1. Navigate to your fork's **Settings** → **Code security and analysis**
2. Enable **Dependabot security updates**
3. Wait ~5 minutes for Dependabot to scan and create PRs
4. Check the **Security** tab → **Dependabot** to see active alerts

### Version Updates

1. Navigate to **Insights** → **Dependency Graph** → **Dependabot**
2. Click **Enable Dependabot**
3. Dependabot will use the included `.github/dependabot.yml` configuration
4. PRs will be created for outdated dependencies

## Making Changes

### Reporting Issues

If you find bugs or have suggestions:
- Check existing [Issues](../../issues) to avoid duplicates
- Provide clear reproduction steps and context
- Include relevant logs or screenshots

### Pull Requests

1. Create a feature branch: `git checkout -b feature/your-feature-name`
2. Make your changes with clear, focused commits
3. Test your changes thoroughly
4. Push to your fork and submit a pull request

#### PR Guidelines

- Use descriptive commit messages
- Keep changes focused and minimal
- Update documentation if needed
- Reference related issues using `#issue-number`

## Project Structure

````
dependabot-demo/
├── .github/
│   ├── dependabot.yml       # Dependabot configuration
│   └── workflows/           # GitHub Actions workflows
├── javascript/              # Node.js demo project
│   ├── package.json         # npm dependencies
│   └── package-lock.json    # Lockfile
├── ruby/                    # Ruby demo project
│   ├── Gemfile              # Ruby dependencies
│   └── Gemfile.lock         # Lockfile
└── README.md                # Getting started guide
````

## Dependency Management

This demo uses Dependabot with the following configuration:
- **GitHub Actions**: Weekly updates
- **npm (JavaScript)**: Weekly updates for `/javascript`
- **Bundler (Ruby)**: Weekly updates for `/ruby`

## Questions?

- Review the main [README](README.md) for Dependabot setup instructions
- Check [Dependabot documentation](https://docs.github.com/code-security/dependabot)
- Open an [Issue](../../issues) for help

## License

This project is available under the MIT License.
