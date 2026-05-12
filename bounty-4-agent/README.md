# Claude PR Review Agent

An AI-powered PR reviewer that generates structured Markdown reviews using Claude.
Available as both a **CLI tool** and a **GitHub Action**.

## CLI Usage

### Prerequisites

- [GitHub CLI (`gh`)](https://cli.github.com) — authenticated
- [Claude Code CLI (`claude`)](https://docs.anthropic.com/en/docs/claude-code) — installed

### Setup

```bash
cp bounty-4-agent/claude-review.sh /usr/local/bin/claude-review
chmod +x /usr/local/bin/claude-review
```

### Run

```bash
# Print review to stdout
claude-review --pr https://github.com/owner/repo/pull/123

# Print review AND post as a PR comment
claude-review --pr https://github.com/owner/repo/pull/123 --post-comment

# Use a specific model
claude-review --pr https://github.com/owner/repo/pull/123 --model opus
```

### Output

The review includes:

- **Summary** — 2-3 sentence overview of the changes
- **Risk Assessment** — table of identified risks with severity ratings
- **Suggestions** — actionable improvements with file/line references
- **What Looks Good** — positive feedback on well-written code
- **Confidence Score** — Low / Medium / High with justification

## GitHub Action Usage

### Setup

1. Copy `.github/workflows/pr-review.yml` to your repository
2. Add `ANTHROPIC_API_KEY` as a repository secret
3. PRs will be automatically reviewed on open and update

### Configuration

The workflow triggers on `pull_request` events (`opened`, `synchronize`).
Edit the workflow file to customize the model, max diff size, or trigger conditions.

## Sample Reviews

See the `sample-reviews/` directory for example outputs:

- `sample-review-1.md` — Review of a small API endpoint addition
- `sample-review-2.md` — Review of an authentication refactor
