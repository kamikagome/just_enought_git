# Pre-commit Learning Project

A small learning project created to understand and implement pre-commit hooks.

## Overview [AI genetated]

This project demonstrates how to set up and use pre-commit hooks to maintain code quality and consistency. Pre-commit hooks automatically check your code before each commit, ensuring standards are met before changes are pushed to the repository.

## Tutorial Reference

Based on this YouTube tutorial: [Pre-commit Hooks Tutorial](https://www.youtube.com/watch?v=shco0WL69hU&t=2609s)

## Getting Started

### Prerequisites

- Python 3.x
- Git

### Installation

1. Install pre-commit:

```bash
python3 -m pip install pre-commit
```

2. Verify installation:

```bash
pre-commit --version
# pre-commit 3.5.0
```

3. Install the git hook scripts:

```bash
pre-commit install
# pre-commit installed at .git/hooks/pre-commit
```

## Configuration

Create a `.pre-commit-config.yaml` file in your project root:

```yaml
repos:
-   repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v3.4.0  # Use the latest version
    hooks:
    -   id: trailing-whitespace
    -   id: end-of-file-fixer
    -   id: check-yaml
```

### Available Hooks

This configuration includes:
- **trailing-whitespace**: Removes trailing whitespace from files
- **end-of-file-fixer**: Ensures files end with a newline
- **check-yaml**: Validates YAML file syntax

## Testing

Run pre-commit on all files to test your setup:

```bash
pre-commit run --all-files
```

## GitHub Actions Integration

Automate pre-commit checks in your CI/CD pipeline with GitHub Actions.

1. Create the workflow directory:

```bash
mkdir -p .github/workflows
```

2. Create the workflow file:

```bash
touch .github/workflows/pre_commit.yml
```

3. Add the following configuration to `.github/workflows/pre_commit.yml`:

```yaml
name: Pre-Commit

on: [push, pull_request]

jobs:
  pre-commit:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - uses: actions/setup-python@v2
      with:
        python-version: '3.x'
    - name: Install pre-commit
      run: pip install pre-commit
    - name: Run pre-commit on all files
      run: pre-commit run --all-files
```

4. Commit and push the workflow:

```bash
git add .github/workflows/pre_commit.yml
git commit -m "Add GitHub Actions workflow for pre-commit"
git push
```

## How It Works

1. **Local Development**: When you run `git commit`, pre-commit automatically runs the configured hooks on staged files
2. **CI/CD**: GitHub Actions runs the same checks on every push and pull request
3. **Consistency**: Ensures code quality standards are maintained across all contributions

## Learning Outcomes

- Understanding pre-commit hooks and their purpose
- Setting up automated code quality checks
- Integrating pre-commit with GitHub Actions
- Maintaining consistent code standards across a project

## Resources

- [Pre-commit Official Documentation](https://pre-commit.com/)
- [Pre-commit Hooks Repository](https://github.com/pre-commit/pre-commit-hooks)
