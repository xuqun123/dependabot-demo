# Contributing to Dependabot Demo

Thank you for your interest in contributing! This repository is a demo project for showcasing [Dependabot](https://docs.github.com/en/code-security/dependabot) features.

## Project Structure

```
dependabot-demo/
├── javascript/       # Node.js sample project with npm dependencies
│   ├── package.json
│   └── package-lock.json
├── ruby/             # Ruby sample project with Bundler dependencies
│   ├── Gemfile
│   └── Gemfile.lock
├── .github/
│   ├── dependabot.yml  # Dependabot version update configuration
│   └── workflows/      # GitHub Actions CI workflows
└── README.md
```

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (v16+) for the JavaScript project
- [Ruby](https://www.ruby-lang.org/) (v3+) and [Bundler](https://bundler.io/) for the Ruby project

### Setup

**JavaScript project:**
```bash
cd javascript
npm install
```

**Ruby project:**
```bash
cd ruby
bundle install
```

## Making Changes

1. Fork the repository.
2. Create a feature branch: `git checkout -b my-feature`
3. Make your changes and commit them with a clear message.
4. Push your branch and open a Pull Request against `main`.

## Pull Request Guidelines

- Keep PRs focused and small — one logical change per PR.
- Include a description of *what* changed and *why*.
- Reference any related issues with `Closes #<issue-number>`.

## Code Style

- **JavaScript**: Follow standard Node.js conventions; no specific linter is enforced.
- **Ruby**: Follow the [Ruby Style Guide](https://rubystyle.guide/).

## Running Tests

There are no automated tests in this demo repository. It is intended to illustrate Dependabot behavior, not as a production application.

## Reporting Issues

Open a [GitHub Issue](../../issues) describing the problem. Include reproduction steps if applicable.

## License

By contributing, you agree that your contributions will be licensed under the repository's [MIT License](LICENSE).
