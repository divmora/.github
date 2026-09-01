---
name: divmora-repo-standardizer
description: >-
  Standardizes and scaffolds repositories across the DIVMORA Technologies GitHub organization.
  Use this skill when auditing, creating, or refactoring any repository in Divmora to enforce
  consistent BSL 1.1 licensing, README badges, reusable GitHub workflows, Release Please,
  GoReleaser, AGENTS.md, CONTRIBUTING.md, and SECURITY.md files.
---

# Divmora Repository Standardizer Skill

This skill guides AI agents and developers through creating or standardizing repositories within the **DIVMORA Technologies** GitHub organization (`divmora`).

---

## Standardization Checklist & File Map

When standardizing an existing repository or scaffolding a new one, apply the following standards file-by-file:

```
<repo-root>/
├── LICENSE                       # Parameterized BSL 1.1 license
├── README.md                     # Status badges, architecture, IAM & License sections
├── AGENTS.md                     # Workspace-specific guidelines & dry-run safety
├── CONTRIBUTING.md               # Local dev setup, make targets, conventional commits
├── SECURITY.md                   # Supported versions table & security@divmora.com
├── Makefile                      # Standardized targets (build, test, fmt, lint, clean)
├── .gitignore                    # Standard language ignore rules
├── .release-please-config.json   # Package config for Release Please
├── .release-please-manifest.json # Version baseline tracker ("0.1.0")
├── .goreleaser.yaml              # Multi-arch binary and lambda compilation (for Go)
└── .github/
    └── workflows/
        ├── docker-publish.yml    # Calls divmora/.github/.github/workflows/docker-publish.yml@main
        ├── release-please.yml    # Calls divmora/.github/.github/workflows/go-release.yml@main
        └── semantic-pull-request.yml # Calls divmora/.github/.github/workflows/semantic-pr.yml@main
```

---

## 1. `LICENSE` File Configuration

Every repository **MUST** contain a root `LICENSE` file based on **Business Source License 1.1 (BSL 1.1)**.

### Action:
1. Copy the master BSL 1.1 template from `https://github.com/divmora/.github/blob/main/LICENSING.md`.
2. Fill in the parameters:
   - **`Licensor`**: `DIVMORA Technologies`
   - **`Licensed Work`**: `<Project Display Name>, including all source code, documentation, and associated files in this repository.`
   - **`Additional Use Grant`**: `You may use the Licensed Work free of charge for non-production purposes, including local development, testing, staging, QA, CI/CD automated validation, educational purposes, and proof-of-concept evaluation. You may not deploy or execute the Licensed Work in a production environment, sell, resell, sublicense, or offer the Licensed Work as a commercial product or hosted/managed service without obtaining a separate commercial license (EULA) from the Licensor.`
   - **`Change Date`**: `Three (3) years from the date of release of the specific version of the Licensed Work.`
   - **`Change License`**: `Apache License, Version 2.0 (as published by the Apache Software Foundation).`

---

## 2. `README.md` Badges & Structure

### Standard Badges:
Place these badges immediately below the `# <Project Title>` header:

```markdown
[![Latest Release](https://img.shields.io/github/v/release/divmora/<repo-name>?logo=github)](https://github.com/divmora/<repo-name>/releases)
[![Go Version](https://img.shields.io/github/go-mod/go-version/divmora/<repo-name>)](go.mod)
[![Documentation: DeepWiki](https://img.shields.io/badge/docs-DeepWiki-blue.svg)](https://deepwiki.com/divmora/<repo-name>)
[![CI/CD](https://github.com/divmora/<repo-name>/actions/workflows/docker-publish.yml/badge.svg)](https://github.com/divmora/<repo-name>/actions)
[![License: BSL 1.1](https://img.shields.io/badge/License-BSL_1.1-blue.svg)](https://github.com/divmora/.github/blob/main/LICENSING.md)
[![Security Policy](https://img.shields.io/badge/Security-Policy-green.svg)](SECURITY.md)
```

*(Note: Omit DeepWiki if unavailable for that project; omit Go version for non-Go repositories.)*

### Required Sections:
1. **Overview & Features**: What the project does, key capabilities.
2. **Configuration / Environment Variables**: Table of all configuration variables with examples.
3. **IAM Permissions (for AWS projects)**: JSON least-privilege policy.
4. **Development & Building**: Common `make` commands and prerequisites.
5. **Community Links**: Direct links to `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md` (inherited from `.github`), and `SECURITY.md`.
6. **License & Commercial Use**: Summary of BSL 1.1, non-production evaluation rights, 3-year Apache 2.0 conversion, and commercial contact (`licensing@divmora.com` / `https://divmora.com`).

---

## 3. `AGENTS.md` Workspace Guidelines

Create an `AGENTS.md` in the project root containing:
- **Project Architecture Layout**: Map of directories and entrypoints.
- **Safety & Dry-Run Guarantee**: All destructive or cloud mutating operations **MUST** support dry-run (`approve bool`).
- **Structured Logging**: Standard Go `log/slog` in JSON format.
- **Conventional Commits**: Enforce Conventional Commits specification.
- **Verification Commands**: Document `make fmt`, `make lint`, `make test`, `make build`.

---

## 4. `CONTRIBUTING.md` & `SECURITY.md`

### `CONTRIBUTING.md`:
- Document prerequisites (e.g. `Go 1.25+`, `Make`, `Docker`, `golangci-lint`).
- List all available `make` targets.
- Detail Conventional Commits (`feat:`, `fix:`, `docs:`, `chore:`, `refactor:`, `test:`).
- Document that contributions fall under the project's BSL 1.1 license.

### `SECURITY.md`:
- Include the supported versions table (e.g., `0.1.x` supported).
- Direct vulnerability reports privately to `security@divmora.com` and GitHub Security Advisories.
- State the 48-hour response SLA.

---

## 5. Build Automation (`Makefile`)

Provide standard targets:
```makefile
.PHONY: build clean test test-coverage dev-setup fmt lint lambda-package docker-build

build:
	@go build -o bin/<binary-name> ./cmd/...

test:
	@go test -v ./...

fmt:
	@go fmt ./...

lint:
	@golangci-lint run

clean:
	@rm -rf bin/
```

---

## 6. Automated Release Automation

### `.release-please-config.json`:
```json
{
  "packages": {
    ".": {
      "release-type": "go",
      "package-name": "<repo-name>",
      "include-component-in-tag": false
    }
  }
}
```

### `.release-please-manifest.json`:
```json
{
  ".": "0.1.0"
}
```

### `.goreleaser.yaml` (for Go repositories):
Configure binaries for `linux`, `darwin`, and `windows` (`amd64`, `arm64`), Lambda `bootstrap` archives (if applicable), SHA256 `checksums.txt`, and release changelog groups (`✨ Features`, `🐛 Bug Fixes`, `⚡ Performance Improvements`, `🔒 Security Updates`, `♻️ Refactoring`, `📚 Documentation`, `🧪 Testing & QA`, `🔧 Tooling & CI`).

---

## 7. Reusable GitHub Workflows

In `.github/workflows/`, replace large boilerplate workflows with thin callers referencing `divmora/.github`:

### `.github/workflows/docker-publish.yml` (if containerized):
```yaml
name: CI/CD

on:
  push:
    branches: [ "**" ]
    tags: [ 'v*.*.*' ]
  pull_request:
    branches: [ "main" ]
  workflow_dispatch:
    inputs:
      sha:
        description: 'Commit SHA'
        required: false
        type: string
      tag_name:
        description: 'Tag Name'
        required: false
        type: string

jobs:
  ci-cd:
    uses: divmora/.github/.github/workflows/docker-publish.yml@main
    with:
      sha: ${{ inputs.sha || '' }}
      tag_name: ${{ inputs.tag_name || '' }}
    secrets: inherit
```

### `.github/workflows/release-please.yml`:
```yaml
name: Release Please & GoReleaser

on:
  push:
    branches:
      - main

permissions:
  contents: write
  pull-requests: write
  packages: write

jobs:
  release:
    uses: divmora/.github/.github/workflows/go-release.yml@main
    secrets: inherit
```

### `.github/workflows/semantic-pull-request.yml`:
```yaml
name: "Lint PR"

on:
  pull_request_target:
    types:
      - opened
      - edited
      - synchronize

jobs:
  validate:
    uses: divmora/.github/.github/workflows/semantic-pr.yml@main
```

---

## 8. Post-Scaffolding Step: Update Org Profile

When the new repository is published to GitHub:
- Open `divmora/.github/profile/README.md`.
- Add the project to the **🛠️ Open & Source-Available Tools** section with a concise 1-line description.
