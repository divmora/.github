# DIVMORA Technologies Licensing Policy & Templates

**DIVMORA Technologies** maintains a two-tier licensing architecture designed to balance developer freedom, community ecosystem growth, and sustainable enterprise tooling:

1. **Permissive Open Source (Apache License 2.0):** Applied to developer utilities, adapters, proxies, relays (e.g. `cloudflare-smtp-relay`), SDKs, GitHub Actions, and scaffolding templates where zero-friction community adoption and uninhibited production/commercial use is intended.
2. **Business Source License 1.1 (BSL 1.1):** Applied to core enterprise platforms, governance systems, and proprietary automation tools where production deployment requires a commercial license (EULA) and converts to Apache 2.0 after three (3) years.

---

## 1. Project Licensing Classification

| License Tier | Applicable Project Types | Commercial / Production Usage | Example Projects |
|---|---|---|---|
| **Apache License 2.0** *(Permissive Open Source)* | Developer utilities, SMTP/API relays, client SDKs, CLIs, integrations, middleware, and GitHub Actions. | **100% Free** in any environment (production, commercial, internal, homelabs). **No EULA or payment required.** | `cloudflare-smtp-relay`, developer SDKs, action runners. |
| **BSL 1.1** *(Source-Available)* | Core enterprise platforms, governance bots, security scanning engines, and proprietary cloud orchestrators. | **Free for non-production use** (local dev, staging, QA, CI/CD). **Requires commercial EULA for production deployments.** | `aws-guardduty-archive-bot`, `gitlab-fleet-governor`. |

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
