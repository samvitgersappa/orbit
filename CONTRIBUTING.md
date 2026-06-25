# Contributing to ORBIT

Thank you for your interest in contributing to ORBIT! This guide will help you get started.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [Project Structure](#project-structure)
- [Coding Standards](#coding-standards)
- [Submitting Changes](#submitting-changes)
- [Areas for Contribution](#areas-for-contribution)
- [Reporting Bugs](#reporting-bugs)
- [Requesting Features](#requesting-features)

---

## Code of Conduct

This project adheres to the [Contributor Covenant Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code. Please report unacceptable behavior via GitHub Issues.

---

## Getting Started

1. **Fork** the repository on GitHub.
2. **Clone** your fork locally:
   ```bash
   git clone https://github.com/<your-username>/orbit.git
   cd orbit
   ```
3. **Add the upstream remote:**
   ```bash
   git remote add upstream https://github.com/samvitgersappa/orbit.git
   ```

---

## Development Setup

### Prerequisites

- macOS on Apple Silicon (M-series recommended)
- Python 3.12+
- Node.js 20+
- [Ollama](https://ollama.com) installed and running
- [uv](https://github.com/astral-sh/uv) package manager

### Backend

```bash
# Install all dependencies including dev extras
uv sync --all-extras --dev

# Verify installation
uv run orbit --help
```

### Frontend

```bash
cd frontend
npm install
npm run dev
```

### Running Tests

```bash
# Python tests
uv run pytest

# Linting
uv run ruff check .
uv run ruff format --check .

# Type checking
uv run mypy src
```

---

## Project Structure

```
orbit/
├── src/orbit/              # Python package
│   ├── analytics/          # ARI evaluator & failure detection
│   ├── arena/              # Agent Arena engine
│   ├── backend/            # FastAPI app & API routes
│   ├── cli/                # Typer CLI
│   ├── database/           # SQLAlchemy models & session
│   ├── examples/           # Example LangGraph agents
│   ├── integrations/       # LangGraph & Ollama integrations
│   ├── replay/             # Failure replay engine
│   └── security/           # Security Guard (injection, content safety)
├── frontend/               # React + TypeScript dashboard
│   └── src/
├── docs/                   # Documentation
├── docker/                 # Dockerfiles
└── .github/                # CI workflows & templates
```

---

## Coding Standards

### Python

- **Type hints** are required on all functions and methods.
- **Async** APIs throughout — use `async`/`await` for all I/O operations.
- **Pydantic v2** models for API input/output.
- **SQLAlchemy 2.0** mapped classes for database models.
- **structlog** for logging (structured JSON logs).
- Format with `ruff format` and lint with `ruff check`.
- Type-check with `mypy`.

### TypeScript / React

- Use **functional components** with hooks.
- Use **TypeScript** strict mode.
- Use **shadcn/ui** for UI components.
- Follow the existing Tailwind CSS patterns.

### General

- Keep modules small and focused — no God classes.
- Prefer dependency injection over global singletons.
- Write docstrings for public functions and classes.
- Preserve existing comments and docstrings when modifying code.

---

## Submitting Changes

### Branching

```bash
# Create a feature branch
git checkout -b feature/your-feature-name

# Or a bugfix branch
git checkout -b fix/description-of-fix
```

### Commit Messages

Use clear, descriptive commit messages:

```
feat: add /runs/{id} endpoint with trace details
fix: handle missing Ollama model in arena engine
docs: add API endpoint documentation
test: add unit tests for ARI evaluator
chore: update dependencies
```

### Pull Request Process

1. **Ensure all checks pass:**
   ```bash
   uv run ruff check .
   uv run mypy src
   uv run pytest
   ```
2. **Update documentation** if your change affects user-facing behavior.
3. **Open a Pull Request** against `main` with a clear description.
4. **Link related issues** in the PR description.
5. Wait for review — maintainers aim to review within 48 hours.

### For Major Changes

Please **open an Issue first** to discuss your proposal before investing significant time. This helps avoid duplicated effort and ensures alignment with the project direction.

---

## Areas for Contribution

Here are some high-impact areas where contributions are especially welcome:

### 🟢 Good First Issues

- Add missing `__init__.py` re-exports for public API
- Add input validation to CLI commands
- Write unit tests for existing modules

### 🟡 Medium Complexity

- Implement missing API endpoints (`/runs/{id}`, `/arena`, `/models`, `/metrics`)
- Add `orbit report`, `orbit runs`, `orbit models`, `orbit security` CLI commands
- Wire dashboard pages to live API data
- Add `research_agent.py` and `retrieval_agent.py` examples
- Implement remaining failure detectors (hallucinated tool, infinite loop, low-confidence)

### 🔴 Advanced

- Build the Replay page with ReactFlow graph + timeline slider
- Add CrewAI / AutoGen integration (Phase 2)
- Implement PII regex detector in security module
- Add OpenTelemetry export support

---

## Reporting Bugs

Use the [Bug Report template](.github/ISSUE_TEMPLATE/bug_report.md) and include:

- Steps to reproduce
- Expected vs actual behavior
- Python/Node version, OS, Ollama version
- Relevant log output

---

## Requesting Features

Use the [Feature Request template](.github/ISSUE_TEMPLATE/feature_request.md) and describe:

- The problem you're trying to solve
- Your proposed solution
- Any alternatives you've considered

---

## Thank You!

Every contribution — whether it's code, documentation, bug reports, or feature ideas — helps make ORBIT better for everyone. 🪐
