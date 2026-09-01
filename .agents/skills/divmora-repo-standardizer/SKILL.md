---
name: divmora-repo-standardizer
description: >-
  Standardizes and scaffolds repositories across the DIVMORA Technologies GitHub organization.
  Use this skill when auditing, creating, or refactoring any repository in Divmora to enforce
  consistent BSL 1.1 licensing, README badges, reusable GitHub workflows (Go, Node, Python, Pages, Docker),
  Release Please, GoReleaser, AGENTS.md, CONTRIBUTING.md, and SECURITY.md files.
---

# Divmora Repository Standardizer Skill

This skill guides AI agents and developers through creating, standardizing, or auditing repositories within the **DIVMORA Technologies** GitHub organization (`divmora`).

---

## Standardization Checklist & File Map

When standardizing an existing repository or scaffolding a new one, apply the following standards file-by-file:

```
<repo-root>/
├── LICENSE                       # Parameterized BSL 1.1 license
├── README.md                     # Status badges, architecture, config table, IAM & License sections
├── AGENTS.md                     # Workspace-specific guidelines & dry-run safety
├── CONTRIBUTING.md               # Local dev setup, make targets, conventional commits
├── SECURITY.md                   # Supported versions table & security@divmora.com
├── Makefile                      # Standardized targets (build, test, fmt, lint, clean)
├── .gitignore                    # Standard language ignore rules
├── .release-please-config.json   # Package config for Release Please
├── .release-please-manifest.json # Version baseline tracker ("0.1.0")
├── .goreleaser.yaml              # Multi-arch binary and lambda compilation (for Go)
└── .github/
    ├── dependabot.yml            # Automated weekly dependency updates
    └── workflows/
        ├── ci.yml                # Calls divmora/.github/.github/workflows/{go-ci,node-ci,python-ci}.yml@main
        ├── docker-publish.yml    # Calls divmora/.github/.github/workflows/docker-publish.yml@main
        ├── pages.yml             # Calls divmora/.github/.github/workflows/pages-deploy.yml@main (if documentation/website)
        ├── release-please.yml    # Calls divmora/.github/.github/workflows/{go-release,release-please}.yml@main
        └── semantic-pull-request.yml # Calls divmora/.github/.github/workflows/semantic-pr.yml@main
```

---

## 1. `LICENSE` File Configuration

Every repository **MUST** contain a root `LICENSE` file according to the organization's two-tier licensing policy:

### Licensing Tier Selection:
1. **Tier 1: Permissive Open Source (Apache License 2.0)**
   - **For:** Developer utilities, relays/proxies (e.g., `cloudflare-smtp-relay`), client SDKs, CLIs, integrations, and GitHub Actions.
   - **Usage:** 100% free for use in any environment (including commercial, production, and SaaS) without requiring a commercial license (EULA) or payment.
   - **Action:** Apply the standard **Apache License, Version 2.0** with copyright `Copyright 2026 DIVMORA Technologies`.

2. **Tier 2: Business Source License 1.1 (BSL 1.1)**
   - **For:** Core enterprise platforms, governance bots, security scanning engines, and proprietary cloud orchestrators.
   - **Usage:** Free for non-production development/testing/QA; requires commercial EULA from DIVMORA for production deployments; converts to Apache 2.0 after 3 years.
   - **Action:** Copy the master BSL 1.1 template from `https://github.com/divmora/.github/blob/main/LICENSING.md` and fill in:
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
[![License: BSL 1.1](https://img.shields.io/badge/License-BSL_1.1-blue.svg)](https://github.com/divmora/.github/blob/main/LICENSING.md)
[![CI/CD](https://github.com/divmora/<repo-name>/actions/workflows/ci.yml/badge.svg)](https://github.com/divmora/<repo-name>/actions)
[![Security Policy](https://img.shields.io/badge/Security-Policy-green.svg)](SECURITY.md)
```

**Language / Runtime Badges:**
- Go: `[![Go Version](https://img.shields.io/github/go-mod/go-version/divmora/<repo-name>)](go.mod)`
- Node: `[![Node Version](https://img.shields.io/node/v/divmora/<package-name>)](package.json)`
- Python: `[![Python Version](https://img.shields.io/pypi/pyversions/<package-name>)](pyproject.toml)`
- Documentation (if available): `[![Documentation: DeepWiki](https://img.shields.io/badge/docs-DeepWiki-blue.svg)](<deepwiki-url>)`

### Required Sections:
1. **Overview & Key Features**: What the project does, key architecture and value proposition.
2. **Configuration / Environment Variables**: Table of all configuration parameters with defaults and examples.
3. **IAM Permissions (for AWS projects)**: JSON least-privilege policy.
4. **Development & Building**: Common `make` / `pnpm` / `pytest` commands and local prerequisites.
5. **Community Links**: Direct links to `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md` (inherited from `.github`), and `SECURITY.md`.
6. **License & Commercial Use**: Summary of BSL 1.1, non-production evaluation rights, 3-year Apache 2.0 conversion, and commercial contact (`licensing@divmora.com` / `https://divmora.com`).

---

## 3. `AGENTS.md` Workspace Guidelines

Create an `AGENTS.md` in the project root containing:
- **Project Architecture Layout**: Map of directories, entrypoints, and core subsystems.
- **Safety & Dry-Run Guarantee**: Mandatory dry-run mode (`approve bool` or `--no-execute-changeset`) for all mutating operations.
- **Structured Logging / Error Handling**: Standard library `log/slog` (JSON) for Go, wrapped errors `%w`.
- **Ecosystem Best Practices**:
  - Go: `log/slog`, `embed.FS`, Air live-reload, AWS SDK v2 context propagation.
  - Node/TS: `pnpm`, strict TypeScript, Vite/Vitest, Tailwind CSS dark aesthetic.
  - Python: `pyproject.toml`, `pytest`, `ruff` linting.
  - SAM: 100% Functionless direct integrations, VTL mapping, IAM SigV4.
  - Protobuf: Schema-driven development with Buf (`buf.yaml`), machine-generated `gen/`.
- **Conventional Commits**: Enforce Conventional Commits specification.
- **Verification Commands**: Document verification commands (`make fmt`, `make lint`, `make test`, `make build`).

---

## 4. `CONTRIBUTING.md` & `SECURITY.md`

### `CONTRIBUTING.md`:
- Document prerequisites (e.g. `Go 1.25+`, `Node.js 24+`, `pnpm 10`, `Python 3.11+`, `Make`, `Docker`).
- List all available `make` targets.
- Detail Conventional Commits (`feat:`, `fix:`, `docs:`, `chore:`, `refactor:`, `test:`, `feat!:`).
- Document that contributions fall under the project's BSL 1.1 license.

### `SECURITY.md`:
- Include the supported versions table (e.g., `0.1.x` supported).
- Direct vulnerability reports privately to `security@divmora.com` and GitHub Security Advisories.
- State the 48-hour response SLA.

---

## 5. Build Automation (`Makefile`)

Provide standard targets tailored to the project runtime:

### Go Projects:
```makefile
.PHONY: build clean test test-coverage dev-setup fmt lint lambda-package docker-build docker-build-multiarch

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

docker-build:
	@docker build -t <image-name>:latest .

docker-build-multiarch:
	@docker buildx build --platform linux/amd64,linux/arm64 -t <image-name>:latest .
```

### Node.js / TypeScript Projects:
```makefile
.PHONY: install build test lint format clean docker-build docker-build-multiarch

install:
	@pnpm install

build:
	@pnpm build

test:
	@pnpm test

lint:
	@pnpm lint

format:
	@pnpm format

clean:
	@rm -rf dist node_modules

docker-build:
	@docker build -t <image-name>:latest .

docker-build-multiarch:
	@docker buildx build --platform linux/amd64,linux/arm64 -t <image-name>:latest .
```

---

## 6. Automated Release Automation

### `.release-please-config.json`:
For Go repositories:
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

For Node.js / TypeScript repositories:
```json
{
  "packages": {
    ".": {
      "release-type": "node",
      "package-name": "<repo-name>",
      "include-component-in-tag": false
    }
  }
}
```

For Python repositories:
```json
{
  "packages": {
    ".": {
      "release-type": "python",
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

### `.goreleaser.yaml` (for Go binary/CLI repositories):
Configure binaries for `linux`, `darwin`, and `windows` (`amd64`, `arm64`), Lambda `bootstrap` archives (if applicable), SHA256 `checksums.txt`, and release changelog groups.

---

## 7. Reusable GitHub Workflows

In `.github/workflows/`, replace large boilerplate workflows with thin callers referencing `divmora/.github`:

### `.github/workflows/ci.yml`:
**For Go:**
```yaml
name: CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  ci:
    uses: divmora/.github/.github/workflows/go-ci.yml@main
```

**For Node.js / TypeScript:**
```yaml
name: CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  ci:
    uses: divmora/.github/.github/workflows/node-ci.yml@main
    with:
      package-manager: 'pnpm'
      node-version: '24'
```

**For Python:**
```yaml
name: CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  ci:
    uses: divmora/.github/.github/workflows/python-ci.yml@main
```

### `.github/workflows/docker-publish.yml` (if containerized):
```yaml
name: CI/CD

on:
  push:
    branches: [ "**" ]
    tags: [ 'v*.*.*', 'v*' ]
  pull_request:
    branches: [ "main" ]
  workflow_dispatch:

jobs:
  ci-cd:
    uses: divmora/.github/.github/workflows/docker-publish.yml@main
    with:
      enable-go-quality: true  # set false for Node/Python containers
    secrets: inherit
```

### `.github/workflows/pages.yml` (if GitHub Pages documentation or static site):
```yaml
name: Deploy GitHub Pages

on:
  push:
    branches: [ "main" ]
  workflow_dispatch:

jobs:
  deploy:
    uses: divmora/.github/.github/workflows/pages-deploy.yml@main
    with:
      artifact-path: './docs'  # or './dist'
```

### `.github/workflows/release-please.yml`:
**For Go repositories with GoReleaser:**
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

**For general / Node / Python / SAM repositories:**
```yaml
name: Release Please

on:
  push:
    branches:
      - main

permissions:
  contents: write
  pull-requests: write

jobs:
  release:
    uses: divmora/.github/.github/workflows/release-please.yml@main
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
- **Alphabetical Order**: Maintain strict alphabetical order (A–Z by repository/project name) within the tool list.
