# Nextflow Lint Pre-commit Hook

A [pre-commit](https://pre-commit.com/) hook for running [`nextflow lint`](https://www.nextflow.io/docs/latest/reference/cli.html#lint) on Nextflow pipeline files.

## Prerequisites

- [Nextflow](https://www.nextflow.io/) (v25.04+) installed and available in your `PATH`
- [pre-commit](https://pre-commit.com/) installed

## Setup

1. Add this to your `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/adamrtalbot/nf-lint-pre-commit
    rev: v0.1.0  # Use the latest release tag
    hooks:
      - id: nextflow-lint
```

2. Install the hook:

```bash
pre-commit install
```

The hook will now run `nextflow lint` on any staged `.nf` and `.config` files when you commit.

## Configuration

Pass any [`nextflow lint` arguments](https://www.nextflow.io/docs/latest/reference/cli.html#lint) via `args`:

```yaml
hooks:
  - id: nextflow-lint
    args: [-format]                      # Auto-format files

  - id: nextflow-lint
    args: [-output, concise]             # Concise output

  - id: nextflow-lint
    args: [-format, -sort-declarations]  # Format + sort

  - id: nextflow-lint
    args: [-output, json]                # JSON output for CI
```

> **Note:** Each example above is an alternative configuration — use only one `id: nextflow-lint` entry.

## Manual Execution

```bash
# Run on all files
pre-commit run nextflow-lint --all-files

# Run on specific files
pre-commit run nextflow-lint --files main.nf
```

## Troubleshooting

**Nextflow not found:** Ensure Nextflow is installed and on your `PATH`:

```bash
curl -s https://get.nextflow.io | bash
nextflow -version
```

**Skip hook temporarily:**

```bash
git commit -m "message" --no-verify
```

## Development

```bash
# Test the hook directly
chmod +x nextflow-lint-hook
./nextflow-lint-hook main.nf
./nextflow-lint-hook -format main.nf nextflow.config

# Test with pre-commit
pip install pre-commit
pre-commit run --all-files
```

## License

MIT