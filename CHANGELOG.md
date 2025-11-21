# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.0.1] - 2025-11-20

### Added
- **CI Workflow**: Initial release of the production-grade GitHub Actions workflow (`.github/workflows/python-ci.yml`).
- **Quality Checks**:
    - Formatting with `black` and `isort`.
    - Linting with `ruff` (replacing Flake8).
    - Static type checking with `mypy`.
- **Security Scanning**:
    - `bandit` for code security analysis.
    - `pip-audit` and `safety` for dependency vulnerability scanning.
    - Least privilege permissions (`contents: read`) for `GITHUB_TOKEN`.
- **Testing**:
    - Matrix testing support for Python 3.10, 3.11, and 3.12.
    - Automated test discovery and execution with `pytest`.
    - Coverage reporting with `pytest-cov` and Codecov support.
- **Build System**:
    - Automated package building (`build`).
    - Package validation with `twine` and `check-wheel-contents`.
- **SBOM**: Automated Software Bill of Materials generation using `cyclonedx-py`.
- **Smart Detection**: Workflow now automatically detects if it's running in a Python project and adjusts steps accordingly.
- **Documentation**: Comprehensive `README.md` with integration guides and tool descriptions.
