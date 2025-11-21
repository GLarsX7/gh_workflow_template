# GitHub Actions CI Template for Python

## 🚀 Overview

This repository provides a **production-grade, security-hardened GitHub Actions Workflow** for Python projects. It is designed to be the "gold standard" for CI/CD, incorporating best practices for security, performance, and modularity.

## ✨ Key Features

### 🛡️ Advanced Security
- **Least Privilege**: Runs with restricted `GITHUB_TOKEN` permissions (`contents: read`).
- **Dependency Scanning**:
  - **Bandit**: Static analysis for security issues in code.
  - **Pip Audit**: Checks environment packages against vulnerability databases.
  - **Safety**: Cross-checks dependencies against known security advisories.
- **SBOM Generation**: Automatically generates a Software Bill of Materials (CycloneDX) for supply chain transparency.

### ⚡ Performance Optimized
- **Smart Caching**: Caches `pip` dependencies and `pytest` internals to speed up subsequent runs.
- **Path Filtering**: Skips workflow execution for documentation-only changes (`*.md`, `docs/`).
- **Fast Fail**: The matrix strategy uses `fail-fast: false` to ensure we see all failures, but individual steps fail immediately on error.
- **Concurrency Groups**: Automatically cancels outdated runs when new code is pushed to the same branch.

### 🧩 Modular Architecture
The pipeline is split into distinct, dependent jobs:
1.  **Quality**: Linting (Ruff), Formatting (Black, isort), Type Checking (mypy).
2.  **Security**: Vulnerability scanning.
3.  **Test**: Matrix testing across Python 3.10, 3.11, 3.12.
4.  **Build**: Packaging and distribution validation.
5.  **Status**: A unified gatekeeper for branch protection.

---

## 📖 Integration Guide

### 1. Adding to an Existing Project
Simply copy the `.github/workflows/python-ci.yml` file to your repository.

**Prerequisites:**
- Ensure you have a `pyproject.toml` or `requirements.txt`.
- If using **Codecov**, add the `CODECOV_TOKEN` to your repository secrets.

### 2. Configuring Branch Protection
To ensure code quality, enable **Branch Protection Rules** in your repository settings:
1.  Go to **Settings** > **Branches** > **Add rule**.
2.  Check **Require status checks to pass before merging**.
3.  Search for and select **`CI Status`**.
    *   *Note: Selecting the individual jobs (e.g., "Test (3.12)") is brittle. The "CI Status" job is a stable gatekeeper.*

### 3. Customizing the Workflow

#### Adding System Dependencies
If your Python packages require OS-level libraries (e.g., `libpq-dev` for PostgreSQL), add a step before "Install dependencies":

```yaml
- name: Install OS dependencies
  run: |
    sudo apt-get update
    sudo apt-get install -y libpq-dev
```

#### Extending for Monorepos
If your Python code lives in a subdirectory (e.g., `backend/`), set the `working-directory` default:

```yaml
defaults:
  run:
    working-directory: ./backend
```

#### Pinning Actions (High Security)
For maximum security, replace version tags (e.g., `@v4`) with specific commit SHAs:

```yaml
uses: actions/checkout@b4ffde65f4633668828d0b66160c696fea646598 # v4.1.1
```
*Use a tool like Dependabot to keep these hashes up to date.*

---

## 🛠 Tools & Technologies

| Category | Tool | Purpose |
| :--- | :--- | :--- |
| **Formatting** | `black` | Uncompromising code formatter. |
| **Imports** | `isort` | Sorts imports alphabetically and by section. |
| **Linting** | `ruff` | Extremely fast linter (replaces Flake8). |
| **Typing** | `mypy` | Static type checker. |
| **Testing** | `pytest` | Robust testing framework. |
| **Security** | `bandit` | Finds common security issues in Python code. |
| **Security** | `pip-audit` | Audits Python environments for known vulnerabilities. |
| **Build** | `build` | PEP 517 compliant package builder. |

## 📊 CI Status Badges

| Python Version | Status |
| :--- | :--- |
| **3.10** | ![CI](https://github.com/YOUR_USERNAME/YOUR_REPO/actions/workflows/python-ci.yml/badge.svg?branch=main) |
| **3.11** | ![CI](https://github.com/YOUR_USERNAME/YOUR_REPO/actions/workflows/python-ci.yml/badge.svg?branch=main) |
| **3.12** | ![CI](https://github.com/YOUR_USERNAME/YOUR_REPO/actions/workflows/python-ci.yml/badge.svg?branch=main) |
