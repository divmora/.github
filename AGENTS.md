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

---


## 2. Licensing Policy (BSL 1.1)

All core Divmora repositories must adopt the **Business Source License 1.1 (BSL 1.1)** unless explicitly requested otherwise:
- **Parameters:**
  - `Licensor`: DIVMORA Technologies
  - `Licensed Work`: `<Project Name>`
  - `Additional Use Grant`: Free for non-production use (development, staging, QA, CI/CD, evaluation). Production deployments and commercial services require an enterprise commercial license (EULA) from DIVMORA Technologies (`licensing@divmora.com`).
  - `Change Date`: Three (3) years from release.
  - `Change License`: Apache License, Version 2.0.
- Reference: See [LICENSING.md](https://github.com/divmora/.github/blob/main/LICENSING.md) for the authoritative license template and policy.

---

## 3. Standard Repository Structure Checklist

When creating or standardizing a repository in the `divmora` organization, ensure the following files and configurations exist:

### Essential Files
- [ ] **`LICENSE`**: Parameterized BSL 1.1 license file.
- [ ] **`README.md`**: Comprehensive overview, feature list, configuration parameters, IAM policies (if cloud-related), and License summary.
- [ ] **`AGENTS.md`**: Project-specific architecture, dry-run safety guarantees, and domain logic notes.
- [ ] **`CONTRIBUTING.md`**: Local developer prerequisites and PR workflow.
- [ ] **`SECURITY.md`**: Vulnerability disclosure instructions pointing to `security@divmora.com`.
- [ ] **`Makefile`**: Standard build targets (`build`, `test`, `fmt`, `lint`, `clean`).
- [ ] **`.gitignore`**: Standard ignore rules for the language runtime (Go, TypeScript, Python, etc.).

### Release & CI/CD Automation
- [ ] **`.release-please-config.json`**: Package configuration for Google Release Please.
- [ ] **`.release-please-manifest.json`**: Baseline version tracker (initialized at `"0.1.0"`).
- [ ] **`.goreleaser.yaml`**: Multi-architecture binary compilation and checksum generation (for Go projects).
- [ ] **`.github/workflows/release-please.yml`**: Integrated Release Please & GoReleaser automation workflow.
- [ ] **`.github/workflows/semantic-pull-request.yml`**: Semantic PR title linting.
- [ ] **`.github/workflows/docker-publish.yml`**: Container image compilation and GHCR publishing (if containerized).

---

## 4. Go Project Guidelines

For Go-based services and Lambda bots:
1. **Structured Logging**: Use Go standard library `log/slog` with JSON output. Avoid unstructured `fmt.Println` or `log.Printf`.
2. **Safety & Dry-Run Guarantee**: Every destructive, cleanup, or mutating function **MUST** support a dry-run mode (e.g. `approve bool`). Write operations against AWS/cloud resources must only execute when `approve == true`.
3. **AWS SDK v2 Patterns**:
   - Always propagate `context.Context`.
   - Initialize region-specific clients explicitly (`awsConfig.WithRegion(region)`).
   - Handle API pagination properly to prevent silent truncation.
4. **Code Verification**:
   Always verify code changes before finishing:
   ```bash
   make fmt
   make lint
   make test
   make build
   ```
