# Organization Agent Guidelines for DIVMORA Technologies

Welcome to the **DIVMORA Technologies** organization-level agent guidelines. These instructions apply to all AI coding agents (Antigravity, Cursor, GitHub Copilot, Claude Code, etc.) and developers working on or scaffolding repositories within the `divmora` GitHub organization.

---

## 1. Core Engineering Standards

### Conventional Commits & Versioning
All commits and Pull Request titles **MUST** strictly follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:
- `feat:` for new features (bumps minor version in Release Please).
- `fix:` for bug fixes (bumps patch version).
- `docs:` for documentation updates.
- `refactor:` for refactoring without behavior changes.
- `test:` for test additions or updates.
- `chore:` for dependencies, tooling, or internal configuration.
- `feat!:` or `fix!:` (or `BREAKING CHANGE:` in commit footer) for breaking changes (bumps major version).

### Documentation & Examples Synchronization
- **Keep docs in sync:** When modifying code, tool schemas, CLI flags, or APIs, always update corresponding documentation in `docs/`, `README.md`, and `examples/`. Outdated documentation is treated as a bug.
- **Single Source of Truth Versioning:** For Go projects, maintain the version constant in source code as `0.0.0-dev` (e.g. `internal/config/config.go`) and let CI/CD inject the actual release version at build time via `-ldflags`.

---

## 2. Licensing Policy (BSL 1.1)

All core Divmora repositories must adopt the **Business Source License 1.1 (BSL 1.1)** unless explicitly requested otherwise:
- **Parameters:**
  - `Licensor`: DIVMORA Technologies
  - `Licensed Work`: `<Project Name>`
  - `Additional Use Grant`: Free for non-production use (development, staging, QA, CI/CD, evaluation, proof-of-concept). Production deployments and commercial services require an enterprise commercial license (EULA) from DIVMORA Technologies (`licensing@divmora.com`).
  - `Change Date`: Three (3) years from the release date of the specific version.
  - `Change License`: Apache License, Version 2.0.
- **Reference:** See [LICENSING.md](https://github.com/divmora/.github/blob/main/LICENSING.md) for the authoritative license template and policy.

---

## 3. Standard Repository Structure Checklist

When creating or standardizing a repository in the `divmora` organization, ensure the following files and configurations exist:

### Essential Files
- [ ] **`LICENSE`**: Parameterized BSL 1.1 license file.
- [ ] **`README.md`**: Comprehensive overview, feature list, configuration parameters, IAM policies (if cloud-related), and License summary.
- [ ] **`AGENTS.md`**: Project-specific architecture, dry-run safety guarantees, and domain logic notes.
- [ ] **`CONTRIBUTING.md`**: Local developer prerequisites, make targets, and PR workflow.
- [ ] **`SECURITY.md`**: Vulnerability disclosure instructions pointing to `security@divmora.com`.
- [ ] **`Makefile`**: Standard build targets (`build`, `test`, `fmt`, `lint`, `clean`).
- [ ] **`.gitignore`**: Standard ignore rules for the language runtime (Go, TypeScript, Python, Rust, etc.).

### Release & CI/CD Automation
- [ ] **`.release-please-config.json`**: Package configuration for Google Release Please.
- [ ] **`.release-please-manifest.json`**: Baseline version tracker (initialized at `"0.1.0"`).
- [ ] **`.goreleaser.yaml`**: Multi-architecture binary compilation and checksum generation (for Go projects).
- [ ] **`.github/workflows/release-please.yml`**: Integrated Release Please automation (calling org reusable workflow).
- [ ] **`.github/workflows/semantic-pull-request.yml`**: Semantic PR title linting (calling org reusable workflow).
- [ ] **`.github/workflows/ci.yml`**: Continuous Integration (calling `go-ci.yml`, `node-ci.yml`, or `python-ci.yml`).
- [ ] **`.github/workflows/docker-publish.yml`**: Container image compilation and GHCR publishing (if containerized).
- [ ] **`.github/dependabot.yml`**: Dependency update configuration.

### README Standards & Badges
Every repository `README.md` must feature standard status badges right below the `# <Project Title>` header:
- **Latest Release:** `[![Latest Release](https://img.shields.io/github/v/release/divmora/<repo-name>?logo=github)](https://github.com/divmora/<repo-name>/releases)`
- **License:** `[![License: BSL 1.1](https://img.shields.io/badge/License-BSL_1.1-blue.svg)](https://github.com/divmora/.github/blob/main/LICENSING.md)`
- **CI/CD Status:** `[![CI/CD](https://github.com/divmora/<repo-name>/actions/workflows/ci.yml/badge.svg)](https://github.com/divmora/<repo-name>/actions)`
- **Language Version:**
  - Go: `[![Go Version](https://img.shields.io/github/go-mod/go-version/divmora/<repo-name>)](go.mod)`
  - Node: `[![Node Version](https://img.shields.io/node/v/divmora/<package-name>)](package.json)`
  - Python: `[![Python Version](https://img.shields.io/pypi/pyversions/<package-name>)](pyproject.toml)`
- **Documentation (if available):** `[![Documentation: DeepWiki](https://img.shields.io/badge/docs-DeepWiki-blue.svg)](<deepwiki-url>)`
- **Security Policy:** `[![Security Policy](https://img.shields.io/badge/Security-Policy-green.svg)](SECURITY.md)`

### Organization Profile Maintenance
- [ ] **`profile/README.md` (`divmora/.github`)**: Whenever a new repository is created, open-sourced, or decommissioned, update the project list under **🛠️ Open & Source-Available Tools** in `divmora/.github/profile/README.md` with its title, repository link, and a concise 1-line description. Maintain strict alphabetical order (A–Z by repository/project name).

---

## 4. Multi-Ecosystem Guidelines

### 4.1 Go Services & Lambda Bots
1. **Structured Logging (`log/slog`)**: Use Go standard library `log/slog` with JSON output. Avoid unstructured `fmt.Println` or `log.Printf`.
2. **Safety & Dry-Run Guarantee**: Every destructive, cleanup, or mutating function **MUST** support a dry-run mode (e.g. `approve bool`). Write operations against AWS or third-party cloud resources must only execute when `approve == true`.
3. **AWS SDK v2 Patterns**:
   - Always propagate `context.Context`.
   - Initialize region-specific clients explicitly (`awsConfig.WithRegion(region)`).
   - Handle API pagination properly to prevent silent truncation.
4. **Error Handling**: Always wrap errors with context using `fmt.Errorf("action failed: %w", err)`.
5. **Embedded Assets**: Embed frontend distributions or static templates directly into the Go binary using `embed.FS` (e.g., `//go:embed dist/*`).
6. **Live Reloading**: Support live reload during local development using `air` (`.air.toml`).

### 4.2 Node.js, TypeScript & Modern Frontend
1. **Package Management**: Prefer `pnpm` (version 9/10) with frozen lockfiles (`pnpm-lock.yaml`) in CI.
2. **Module System**: Maintain clean module boundaries. Use pure ES Modules (`import`/`export`) for modern Vite/React/Next.js projects, or CommonJS (`require`/`module.exports`) only when required by legacy runtimes. Do not mix module syntaxes within the same package.
3. **Strict TypeScript**: Enable `strict: true` in `tsconfig.json`. Avoid `any` types; prefer explicit interfaces and zod/valibot schemas for API boundaries.
4. **UI Styling & Theming**: Standardize on Tailwind CSS with dark-mode first design tokens. Use Lucide icons and headless accessible primitives (Radix UI / Shadcn).
5. **Testing**: Use Node's built-in `node:test` or `vitest` with explicit test isolation.

### 4.3 Python Projects & Agent Tooling
1. **Packaging**: Standardize on `pyproject.toml` (PEP 621) with modern build backends (e.g., Hatch, Flit, or Poetry).
2. **Linting & Formatting**: Use `ruff` for ultra-fast linting and code formatting.
3. **Testing**: Write unit tests using `pytest` with fixtures in `tests/conftest.py`.
4. **Typing**: Use static type annotations and verify with `mypy` or `pyright`.

### 4.4 AWS Serverless & Cloud Infrastructure
1. **Functionless Service Integration**: Prefer direct AWS API Gateway VTL request/response mapping templates to DynamoDB or SQS over Lambda functions when compute is unnecessary.
2. **Least Privilege IAM**: Maintain least-privilege IAM policies and document all required actions in `README.md`.
3. **Non-Destructive Deployments**: Always validate templates and execute changesets (`sam deploy --no-execute-changeset`).

### 4.5 Protocol Buffers & gRPC
1. **Schema-Driven Development**: Maintain `.proto` definitions in `proto/` managed by Buf (`buf.yaml`, `buf.gen.yaml`).
2. **Protected Code Generation**: Code in `gen/` is strictly machine-generated. **NEVER** edit generated files directly; always run `make proto`.

### 4.6 AI Agent Skills & Extensions (`agentskills.io`)
1. **Specification Conformity**: All agent skills must reside in `.agents/skills/<skill-name>/` or `skills/<skill-name>/` with a valid `SKILL.md` containing YAML frontmatter (`name`, `description`) and standardized markdown sections.
2. **Automated Verification**: Run skill validation (`python3 scripts/validate_skills.py`) and catalog synchronization (`python3 scripts/generate_catalog.py`) after adding or editing skills.
3. **Link Integrity**: All relative markdown links within `references/` or `scripts/` must resolve to existing files.

### 4.7 AI Code Review & Multi-VCS Standards
1. **AST Scope Slicing**: When reviewing large PRs/MRs, slice syntax trees to analyze only enclosing scopes around changed lines. Replace untouched code blocks with `# ... skipped N lines ...`.
2. **Anti-Hallucination Directives**: Instruct models that enclosing context lines are read-only reference lines. Evaluate only lines modified by the author.
3. **Comment Budgeting**: Cap inline PR review comments to the top 10–15 highest-priority findings (High > Medium > Low) to prevent reviewer fatigue. Skip lockfiles (`go.sum`, `pnpm-lock.yaml`) and generated code (`*.pb.go`).
4. **Duplicate Prevention**: Include review tracking markers (e.g., `<!-- review_sha: <sha> -->`) to prevent duplicate bot comments on re-runs.

---

## 5. Organization Reusable Workflows Index

All repositories in `divmora` should call the centralized reusable workflows hosted in `divmora/.github/.github/workflows/`:

| Reusable Workflow | Purpose | Caller Example |
|:---|:---|:---|
| **`go-ci.yml`** | Go linting (`golangci-lint`) and unit testing. | `uses: divmora/.github/.github/workflows/go-ci.yml@main` |
| **`node-ci.yml`** | Node.js / TypeScript testing, linting, and building with pnpm/npm caching. | `uses: divmora/.github/.github/workflows/node-ci.yml@main` |
| **`python-ci.yml`** | Python testing (`pytest`) and linting (`ruff`). | `uses: divmora/.github/.github/workflows/python-ci.yml@main` |
| **`docker-publish.yml`** | Multi-arch Docker image build and GHCR publishing. | `uses: divmora/.github/.github/workflows/docker-publish.yml@main` |
| **`pages-deploy.yml`** | Static documentation and web app deployment to GitHub Pages. | `uses: divmora/.github/.github/workflows/pages-deploy.yml@main` |
| **`go-release.yml`** | Release Please + GoReleaser binary release automation for Go. | `uses: divmora/.github/.github/workflows/go-release.yml@main` |
| **`release-please.yml`** | General Release Please versioning and changelog generator. | `uses: divmora/.github/.github/workflows/release-please.yml@main` |
| **`semantic-pr.yml`** | PR title validation against Conventional Commits. | `uses: divmora/.github/.github/workflows/semantic-pr.yml@main` |

---

## 6. Standard Verification Commands Matrix

Always verify code changes before finalizing tasks:

| Ecosystem | Format | Lint | Test | Build / Validate |
|:---|:---|:---|:---|:---|
| **Go** | `make fmt` (`go fmt ./...`) | `make lint` (`golangci-lint run`) | `make test` (`go test -v ./...`) | `make build` (`go build ./cmd/...`) |
| **Node / TS** | `pnpm format` | `pnpm lint` | `pnpm test` | `pnpm build` |
| **Python** | `ruff format .` | `ruff check .` | `pytest -v` | `pip install -e .` |
| **AWS SAM** | - | `sam validate` | `make test` | `sam build` |
| **Protobuf** | `buf format -w` | `buf lint` | - | `make proto` (`buf generate`) |
