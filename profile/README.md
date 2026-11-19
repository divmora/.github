# Welcome to DIVMORA Technologies 👋

**DIVMORA Technologies** builds high-performance cloud governance, security automation, and developer infrastructure tooling.

---

## 🏷️ What's Free and What's Paid

| | What you can do for free | What needs a licence | Projects |
| :--- | :--- | :--- | :--- |
| **Open source** (Apache 2.0) | Everything, in any environment, including production and commercial use | Nothing. Paid setup and support are offered for some projects | code-review-bot, owlflow, functionless-url-shortener, show-and-tell, and the other Apache 2.0 repositories below |
| **Free core + paid features** (Elastic License 2.0) | Run the core in any environment, production included | Paid features need a Divmora licence key in every environment | code-review-console |
| **Commercial licence for production** (BSL 1.1) | Development, testing, CI and evaluation | Production use; each release becomes Apache 2.0 after three years | gitlab-fleet-governor, otel-aws-log-processor, aws-das-processor, and the other BSL 1.1 repositories below |

Each project below is tagged with its licence. Details: [Licensing Policy & FAQ](https://github.com/divmora/.github/blob/main/LICENSING.md). To buy a licence or support, email **licensing@divmora.com**.

---

## 🛠️ Open & Source-Available Tools

### 🤖 AI Engineering & Autonomous Agents

- **[agent-skills](https://github.com/divmora/agent-skills)**: Canonical registry and harness for production-grade AI engineering skills and plugins adhering to `agentskills.io`.
- **[code-review-bot](https://github.com/divmora/code-review-bot)** · *Apache 2.0* · [website](https://divmora.github.io/code-review-bot/): AI code review for GitHub, GitLab and Bitbucket with any LLM provider, as a CLI, GitHub Action, GitLab CI job or Bitbucket Pipelines step.
- **[code-review-console](https://github.com/divmora/code-review-console)** · *ELv2, free core + paid features* · [website](https://divmora.github.io/code-review-console/): Self-hosted control plane that runs code-review-bot for every repository, with webhooks, a review queue, Docker and Kubernetes executors and an admin panel.
- **[jules-ai-agent](https://github.com/divmora/jules-ai-agent)** · *Apache 2.0*: Autonomous repository maintenance and AI coding agent for background task execution.
- **[localharness](https://github.com/divmora/localharness)** · *Apache 2.0*: Universal multi-agent orchestration harness and developer desktop GUI for agentic workflows.
- **[zenith](https://github.com/divmora/zenith)**: Enterprise unified AI developer platform, orchestration engine, and multi-provider code assistant.

### 🛡️ Cloud Governance & Security Automation

- **[authpin](https://github.com/divmora/authpin)** · *BSL 1.1*: Standalone, encrypted-at-rest OTP generation and blind verification service with pluggable database adapters and multi-channel dispatch.
- **[aws-guardduty-archive-bot](https://github.com/divmora/aws-guardduty-archive-bot)** · *BSL 1.1*: Automated Amazon GuardDuty security findings archival & organization management bot.
- **[cloudformation-staksets](https://github.com/divmora/cloudformation-staksets)** · *Apache 2.0*: Curated collection of AWS CloudFormation StackSet templates for multi-account governance, security baseline enforcement, and compliance automation.
- **[cloudformation-templates](https://github.com/divmora/cloudformation-templates)** · *Apache 2.0*: Production-ready AWS CloudFormation infrastructure-as-code templates for application and service workloads (Lambda, ECS Fargate, VPCs).
- **[gitlab-fleet-governor](https://github.com/divmora/gitlab-fleet-governor)** · *BSL 1.1* · [website](https://divmora.github.io/gitlab-fleet-governor/): Fleet governance and infrastructure automation for GitLab environments.

### ⚡ Workflow Automation & Serverless Systems

- **[cloudflare-smtp-relay](https://github.com/divmora/cloudflare-smtp-relay)** · *Apache 2.0, maintenance mode*: SMTP relay for clients that can't use Cloudflare's own SMTP submission (port 465), forwarding plain SMTP or STARTTLS on port 587 through the Cloudflare Email Sending API. Run it on a private network.
- **[functionless-url-shortener](https://github.com/divmora/functionless-url-shortener)** · *Apache 2.0*: High-performance, zero-compute URL shortener and redirect engine on AWS API Gateway and DynamoDB.
- **[owlflow](https://github.com/divmora/owlflow)** · *Apache 2.0* · [website](https://divmora.github.io/owlflow/): Lightweight, high-performance workflow automation engine in Go with event-driven triggers, DAG execution, dynamic templating, and interactive developer studio.

### 📊 Observability & Developer Tooling

- **[aws-das-processor](https://github.com/divmora/aws-das-processor)** · *BSL 1.1* · [website](https://divmora.github.io/aws-das-processor/): High-performance Go AWS Lambda decrypting, filtering, and converting AWS RDS Database Activity Streams (DAS) into Parquet in S3.
- **[license-go](https://github.com/divmora/license-go)** · *Apache 2.0*: Unified Go licensing framework, Ed25519 token engine, and administrative CLI across Divmora products.
- **[otel-aws-log-processor](https://github.com/divmora/otel-aws-log-processor)** · *BSL 1.1* · [website](https://divmora.github.io/otel-aws-log-processor/): High-performance Go Lambda converting AWS ALB, NLB, WAF, and CloudFront logs to OpenTelemetry (OTLP).
- **[periscope](https://github.com/divmora/periscope)** · *BSL 1.1*: High-performance telemetry, request monitoring, and observability lakehouse for Laravel applications.
- **[show-and-tell](https://github.com/divmora/show-and-tell)** · *Apache 2.0* · [website](https://divmora.github.io/show-and-tell/): Standalone JavaScript screen recording SDK with real-time audio mixing, configurable duration limits, and browser reload resilience.

---

## 🔒 Security & Responsible Disclosure

Security is fundamental to everything we engineer. If you discover a potential vulnerability across any Divmora software or service, please review our [Security Policy](https://github.com/divmora/.github/blob/main/SECURITY.md) or email us directly at **security@divmora.com**.

---

## 🤝 Community, Licensing & Standards

- **[Licensing Policy & FAQ](https://github.com/divmora/.github/blob/main/LICENSING.md)**: Our Apache 2.0, BSL 1.1 and Elastic License 2.0 tiers, what each allows for free, and commercial licensing.
- **[Code of Conduct](https://github.com/divmora/.github/blob/main/CODE_OF_CONDUCT.md)**: We are committed to an open, welcoming, and harassment-free community.
- **[Contributing Guide](https://github.com/divmora/.github/blob/main/CONTRIBUTING.md)**: How to get involved, submit PRs, and follow our Conventional Commits standard.
- **Commercial & Enterprise Inquiries**: Reach out at **licensing@divmora.com** or visit [divmora.com](https://divmora.com).
