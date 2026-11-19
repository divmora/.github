# DIVMORA Technologies Licensing Policy & Templates

**DIVMORA Technologies** maintains a three-tier licensing architecture designed to balance developer freedom, community ecosystem growth, and sustainable enterprise tooling:

1. **Permissive Open Source (Apache License 2.0):** Applied to developer utilities, adapters, proxies, relays (e.g. `cloudflare-smtp-relay`), SDKs, GitHub Actions, and scaffolding templates where zero-friction community adoption and uninhibited production/commercial use is intended.
2. **Business Source License 1.1 (BSL 1.1):** Applied to core enterprise platforms, governance systems, and proprietary automation tools where production deployment requires a commercial license (EULA) and converts to Apache 2.0 after three (3) years.
3. **Elastic License 2.0 (ELv2):** Applied to products with a free core and paid features unlocked by a Divmora license key (e.g. `code-review-console`). The free core is free in every environment, production included; paid features need a license key in every environment, development and CI/CD included. The line between free and paid is drawn by feature, not by environment.

---

## 1. Project Licensing Classification

| License Tier | Applicable Project Types | Commercial / Production Usage | Example Projects |
|---|---|---|---|
| **Apache License 2.0** *(Permissive Open Source)* | Developer utilities, SMTP/API relays, client SDKs, CLIs, integrations, middleware, and GitHub Actions. | **100% Free** in any environment (production, commercial, internal, homelabs). **No EULA or payment required.** | `cloudflare-smtp-relay`, developer SDKs, action runners. |
| **BSL 1.1** *(Source-Available)* | Core enterprise platforms, governance bots, security scanning engines, and proprietary cloud orchestrators. | **Free for non-production use** (local dev, staging, QA, CI/CD). **Requires commercial EULA for production deployments.** | `aws-guardduty-archive-bot`, `gitlab-fleet-governor`. |
| **Elastic License 2.0** *(Source-Available, free core + license keys)* | Products sold by feature: a useful free core plus paid features protected by a Divmora license key ([license-go](https://github.com/divmora/license-go), issued by the license portal). | **Free core: free in any environment**, production included, except as a hosted/managed service for third parties. **Paid features: license key required in every environment** (dev, CI/CD, staging, production). Circumventing the license key is not permitted. Never converts to open source. | `code-review-console`. |

---

## 2. Licensing FAQ

### What projects do NOT need a Commercial EULA?
Any project licensed under **Apache License 2.0** (such as `cloudflare-smtp-relay`, developer toolkits, or client libraries) does not require any commercial license or EULA. You are completely free to deploy, integrate, modify, and run them in any production, SaaS, or commercial setup.

### What is permitted for free under BSL 1.1?
- Local development, experimentation, and testing on developer machines.
- Automated testing in CI/CD pipelines (GitHub Actions, GitLab CI, etc.).
- Pre-production environments (staging, sandbox, development VPCs, QA clusters).
- Security audits, educational usage, and proof-of-concept evaluation.

### What requires a Commercial EULA under BSL 1.1?
- Deploying the BSL 1.1 software in any production AWS account, Kubernetes cluster, or server.
- Using the software to manage, audit, or operate live production customer environments.
- Offering the software (or derivative work) as a paid SaaS, managed service, or hosted offering.
- Embedding the software into commercial proprietary products.

### What is permitted for free under the Elastic License 2.0?
- Using, running, modifying and distributing the software's free core, in any environment, including production and commercial use.
- Reading the source, including the code of paid features, for example for security review.

### What is not permitted under the Elastic License 2.0?
- Providing the software to third parties as a hosted or managed service that gives them access to a substantial set of its features.
- Using any paid feature without a valid license key, including in development, testing or CI/CD: moving, changing, disabling or circumventing the license key functionality, or removing or obscuring anything it protects, is prohibited.
- Altering or removing licensing, copyright or other notices.

### When should a new project use ELv2 instead of BSL 1.1?
Use ELv2 when the product should be adopted freely (including in production) at a basic level, and sold by **feature**. Use BSL 1.1 when the whole product is sold for **production use** and free use is limited to non-production environments. Do not combine BSL with a separate proprietary license for paid code: ELv2 covers both the free core and the key-protected features in one standard license.

### How do I obtain a Commercial License?
Please contact our licensing team at **licensing@divmora.com** or visit **[divmora.com](https://divmora.com)** to discuss licensing, enterprise support tiers, and custom SLAs.

---

## 3. Standard BSL 1.1 Repository License Template

When creating a new BSL 1.1 repository in the **divmora** organization, copy the template below into your repository's root `LICENSE` file and replace `<Repository / Software Name>` with your project's name.


```text
Business Source License 1.1

Parameters

Licensor: DIVMORA Technologies
Licensed Work: <Repository / Software Name>, including all source code, documentation, and associated files in this repository.
Additional Use Grant: You may use the Licensed Work free of charge for non-production purposes, including local development, testing, staging, QA, CI/CD automated validation, educational purposes, and proof-of-concept evaluation. You may not deploy or execute the Licensed Work in a production environment, sell, resell, sublicense, or offer the Licensed Work as a commercial product or hosted/managed service without obtaining a separate commercial license (EULA) from the Licensor.
Change Date: Three (3) years from the date of release of the specific version of the Licensed Work.
Change License: Apache License, Version 2.0 (as published by the Apache Software Foundation).

Notice

The Business Source License 1.1 (the "License") is not an Open Source license, but it permits certain free uses and converts to an Open Source license on the Change Date.

The Licensor hereby grants you the right to copy, modify, create derivative works, redistribute, and make non-production use of the Licensed Work. The Licensor also grants you an Additional Use Grant as defined above.

Effective on the Change Date, or the fourth anniversary of the first publicly available distribution of a specific version of the Licensed Work under this License (whichever is earlier), the Licensor grants you a non-exclusive, royalty-free, worldwide license to use the version of the Licensed Work distributed under this License under the terms of the Change License.

Conditions

1. You may make use of the Licensed Work only under the terms of this License or the Change License (as applicable).

2. You must reproduce this License, including the Parameters and Notice, and all copyright and other proprietary notices in any copy, modification, or derivative work of the Licensed Work that you make or distribute.

3. If you make modifications or derivative works of the Licensed Work, you must license such modifications or derivative works under this License (or, once the Change Date has occurred for that version, under the Change License).

4. Any use of the Licensed Work in a production environment, or offering the Licensed Work as a commercial product or hosted/managed service, requires a valid commercial license (EULA) from the Licensor. For commercial inquiries and enterprise licensing, please contact licensing@divmora.com or visit https://divmora.com.

DISCLAIMER

THE LICENSED WORK IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE LICENSED WORK OR THE USE OR OTHER DEALINGS IN THE LICENSED WORK.
```

---

## 4. Elastic License 2.0 Repository Setup

For a new ELv2 repository in the **divmora** organization:

1. Copy [`license-templates/ELASTIC-LICENSE-2.0.txt`](license-templates/ELASTIC-LICENSE-2.0.txt) **unchanged** to the repository's root `LICENSE` file. It is the official text from <https://www.elastic.co/licensing/elastic-license>; do not edit it. Put the copyright line (`Copyright <year> DIVMORA Technologies`) in the README's license section, not in `LICENSE`.
2. Gate every paid feature behind a Divmora license key using [license-go](https://github.com/divmora/license-go), and add the product and its features (modules) to the license portal's product catalog.
3. In the README, list what is free and what needs a key, and link `LICENSE`. Use the badge `[![License: ELv2](https://img.shields.io/badge/License-Elastic_2.0-blue.svg)](LICENSE)`.
4. Container images: set `org.opencontainers.image.licenses="Elastic-2.0"` (the SPDX identifier).

