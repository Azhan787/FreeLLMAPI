# 🤝 Contributing to FreeLLMAPI

<p align="center">
  <strong>Built by the community. Improved through collaboration.</strong>
</p>

Thank you for your interest in contributing to **FreeLLMAPI**!

FreeLLMAPI is a local-first aggregator for free-tier LLM APIs, designed to bring multiple providers, endpoints, and routing capabilities together in one place.

We welcome contributions from developers, designers, testers, documentation writers, and AI-assisted development enthusiasts. Whether you're fixing a bug, adding a provider, improving the dashboard, or refining the developer experience, your contribution matters.

**Project Maintainer:** Muhammad Azhan

---

## 📑 Table of Contents

- [Getting Started](#-getting-started)
- [Development Workflow](#-development-workflow)
- [Contribution Guidelines](#-contribution-guidelines)
- [Database Migrations](#-database-migrations)
- [Translations and Internationalization](#-translations-and-internationalization)
- [Optional Commit Checklist Hook](#-optional-commit-checklist-hook)
- [AI-Assisted Contributions](#-ai-assisted-contributions)
- [Reporting Issues](#-reporting-issues)
- [Community Improvements](#-community-improvements)
- [Acknowledgments](#-acknowledgments)

---

## 🚀 Getting Started

Before contributing, make sure you have the required development tools installed and have cloned the repository.

Install the project dependencies:

```bash
npm install
```

For a repeatable local setup, use the bootstrap script for your shell. It installs dependencies when `package-lock.json` has changed and creates `.env` if it does not already exist.

**Windows PowerShell**

```powershell
.\scripts\dev-bootstrap.ps1
```

**Linux / macOS / Bash**

```bash
./scripts/dev-bootstrap.sh
```

> Follow the repository's setup instructions and configure any required environment variables before starting the application.

## 💻 Development Workflow

Use the following commands to develop, test, and build the project.

### Start the development environment

```bash
npm run dev
```

The development environment runs the server on port `3001` and the dashboard on port `5173`, with hot module replacement (HMR).

### Apply database migrations

```bash
npm run db:migration:up
```

### Run tests

```bash
npm test
```

This runs the server's Vitest suite and also runs client tests when available.

### Build the project

```bash
npm run build
```

Compile the server and dashboard to verify that your changes build successfully.

---

## 📋 Contribution Guidelines

Every pull request should follow these principles:

- **Include tests:** Add relevant tests and keep the existing test suite passing with `npm test`.
- **Follow project conventions:** Respect `.editorconfig` and the existing TypeScript configuration defaults.
- **Keep changes focused:** Make each pull request address one clear improvement or fix.
- **Protect project quality:** Avoid unrelated formatting changes, unnecessary refactoring, or generated noise.
- **Verify provider information:** Confirm model IDs, API endpoints, rate limits, and free-tier requirements against reliable provider documentation.
- **Keep free-tier claims accurate:** Do not add services that require payment or a credit card to begin using. The catalog is intended to list genuinely free-to-start tiers.
- **Document meaningful changes:** Update the relevant documentation when behavior, configuration, or setup requirements change.

### Suggested contribution areas

Contributions are especially welcome in these areas:

- Adding or updating LLM providers.
- Integrating additional API endpoints.
- Improving routing and provider selection.
- Enhancing the dashboard and user experience.
- Fixing bugs and improving reliability.
- Expanding automated test coverage.
- Improving documentation and translations.
- Strengthening security and performance.

Check the README's **Good First PRs** section for ideas suitable for getting started.

---

## 🗄️ Database Migrations

All database schema changes must use individual migration files located in:

```text
server/src/db/migrations/
```

**Important rules:**

- Create a new migration for every schema change.
- Do not modify migration files that have already been applied.
- Ensure that schema changes can be applied and, where supported, rolled back safely.

Refer to [`server/src/db/README.md`](server/src/db/README.md) for detailed migration instructions.

### Available migration commands

Create a migration:

```bash
npm run db:migration:create --name=add_embedding_index
```

Apply migrations:

```bash
npm run db:migration:up
```

Roll back a migration:

```bash
npm run db:migration:down
```

---

## 🌍 Translations and Internationalization

The dashboard supports **60 locales**.

The English translation file, `en.json`, is the source of truth. Other locale files should mirror its keys.

Before submitting translation changes, run the internationalization check from the `client/` directory:

```bash
npm run check:i18n
```

For translation conventions, terminology, and detailed guidance, see [`docs/TRANSLATION.md`](docs/TRANSLATION.md).

---

## 🛡️ Optional Commit Checklist Hook

The repository includes an optional checklist hook for [Claude Code](https://claude.com/claude-code).

When enabled, the hook reads the contribution rules and reminds the agent to review its changes before running `git commit` or `git push`. It provides guidance rather than blocking the operation.

### Preview the checklist

Run this command from the repository root:

```bash
node .claude/hooks/contributing-check.mjs --preview
```

### Enable the hook locally

Add the following configuration to your personal `.claude/settings.local.json` file:

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "node \"${CLAUDE_PROJECT_DIR:-.}/.claude/hooks/contributing-check.mjs\""
          }
        ]
      }
    ]
  }
}
```

This configuration is optional and is not enabled automatically.

The hook reads the contribution rules when it runs, so changes to this document do not require a regeneration step.

---

## 🤖 AI-Assisted Contributions

AI-assisted contributions are welcome. Regardless of whether you use an AI coding assistant or write everything manually, the same quality standards apply.

Contributors remain responsible for the correctness, security, and maintainability of their submissions.

### Expectations for AI-assisted pull requests

- **Understand your changes.** Be prepared to explain your diff and the reasoning behind it.
- **Test the implementation.** Run the actual code and verify that the tests exercise the intended behavior.
- **Review generated output.** Remove unrelated refactoring, unnecessary formatting changes, and accidental file modifications.
- **Verify factual claims.** Do not rely on an AI model's memory for provider limits, endpoint URLs, model IDs, or pricing details. Check the provider's documentation.
- **Maintain focused scope.** Keep each pull request limited to its intended purpose.
- **Prioritize quality over quantity.** A small, verified contribution is more valuable than a large, unreviewed change.

You do not need to label a pull request as AI-assisted. The focus is on the quality and reliability of the result.

Pull requests containing clearly unreviewed generated output, fabricated provider details, or tests that do not run may be returned for revision or closed.

---

## 🐛 Reporting Issues

Clear bug reports help maintainers investigate and resolve problems efficiently.

When reporting an issue, include as much of the following information as possible:

- Project version or commit hash.
- Operating system and relevant runtime versions.
- The provider or endpoint involved.
- Steps to reproduce the problem.
- Expected behavior versus actual behavior.
- Relevant request and response details, with secrets removed.
- Server logs surrounding the failure, especially for routing or verification issues.

**Security reminder:** Never publish API keys, access tokens, passwords, private credentials, or other sensitive information in an issue or pull request.

---

## 🧪 Community Improvements and Existing Work

Before starting a substantial change, review relevant community forks, branches, and existing implementations to avoid duplicating work.

The following community work was referenced in the original project documentation:

| Branch | Improvement |
|---|---|
| `fix-loopback-only` | Restricts admin API access to localhost to reduce external exposure. |
| `fix-35-admin-security` | Adds optional `ADMIN_PASSWORD` HMAC authentication for remote admin API access. |
| `fix-101-markdown` | Improves Markdown rendering in the Playground UI. |
| `fix-119-atomic-ratelimits` | Uses atomic SQLite `BEGIN IMMEDIATE` transactions to address rate-limit race conditions. |
| `feature-122-auto-routing` | Adds per-request `smart`, `fast`, and `cheap` routing strategies. |

These references are not a guarantee that the branches are currently available or merged. Check the repository before relying on them.

If you port an existing community contribution into a pull request, credit the original author in the pull request description.

---

## 🙌 Acknowledgments

FreeLLMAPI benefits from the work of open-source developers, community contributors, maintainers, and everyone who reports issues or shares constructive feedback.

Thank you for helping make the project more useful, reliable, and accessible.

---

## 👨‍💻 Project Maintainer

**Muhammad Azhan**

Maintainer of this repository.

For project questions, bug reports, and proposed improvements, please use the repository's GitHub Issues and Pull Requests.

---

<p align="center">
  <strong>FreeLLMAPI</strong><br/>
  <sub>Open collaboration. Verified contributions. Better developer experiences.</sub>
</p>
