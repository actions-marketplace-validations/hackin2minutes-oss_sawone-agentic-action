# SawOne-Agentic: DevSecOps for Agentic AI, MCP, LLMs and ML

[![GitHub Release](https://img.shields.io/github/v/release/hackin2minutes-oss/sawone-agentic-action?color=purple)](https://github.com/hackin2minutes-oss/sawone-agentic-action/releases)
[![Marketplace](https://img.shields.io/badge/GitHub-Marketplace-blue.svg)](https://github.com/marketplace/actions/sawone-agentic-ai-agent-security)

**SawOne-Agentic** is a comprehensive, phase-wise DevSecOps security scanner purpose-built for the AI era:
- **Agentic AI & Multi-Agent Systems**: LangGraph, CrewAI, AutoGen, PydanticAI, OpenAI Agents SDK, Semantic Kernel.
- **Model Context Protocol (MCP)**: Tool privilege analysis, arbitrary shell/filesystem command injection, unpinned servers, plaintext secrets.
- **LLM Applications & RAG**: Prompt injection, hidden HTML comment / zero-width indirect injection, PII & Saudi national identifiers (PDPL), sensitive data leakage.
- **ML Models & Supply Chain**: Safe model format validation (blocking unsafe pickle / torch load execution), CycloneDX ML-BOM generation.
- **AI Cloud IaC**: Hardening AWS Bedrock, SageMaker, Azure OpenAI, and Google Vertex AI.
- **Bilingual Executive Reports**: Automated English (`security-report.pdf`) and Arabic (`security-report-ar.pdf`) PDF & HTML reports with full compliance mappings (OWASP LLM Top 10, MITRE ATLAS, SDAIA AI Ethics, NIST AI RMF).

---

## Quick Start

Add this step to your GitHub Actions workflow:

```yaml
name: Security Scan

on:
  push:
    branches: [main]
  pull_request:

jobs:
  ai-security:
    runs-on: ubuntu-latest
    permissions:
      contents: read
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Run SawOne-Agentic
        uses: hackin2minutes-oss/sawone-agentic-action@v1
        with:
          severity: 'HIGH,CRITICAL'
          enforce: true
          languages: 'en,ar'

      - name: Upload Security Reports
        if: always()
        uses: actions/upload-artifact@v4
        with:
          name: sawone-agentic-reports
          path: sawone-agentic-reports/
```

---

## Action Inputs

| Input | Description | Default |
|---|---|---|
| `path` | Path to scan in repository | `.` |
| `config` | Path to `.sawone.yml` configuration | `.sawone.yml` |
| `phases` | DevSecOps phases to execute (`all`, or subset e.g. `plan,code,build,test,release`) | `all` |
| `severity` | Minimum severity level that breaks the build | `HIGH,CRITICAL` |
| `enforce` | If `true`, gate violations fail CI. If `false`, report-only mode | `true` |
| `languages` | Report languages to generate (`en`, `ar`, or `en,ar`) | `en,ar` |
| `redteam-endpoint` | Optional live LLM endpoint to attack (NVIDIA garak + promptfoo) | `""` |
| `redteam-profile` | Red-teaming probe intensity (`quick` or `full`) | `quick` |

---

## Outputs

| Output | Description |
|---|---|
| `passed` | `true` if all security gates passed, `false` otherwise |
| `failed` | Total count of blocking security gate failures |
| `reports-dir` | Directory path containing generated PDF, HTML, and SARIF artifacts |

---

## Audit & Compliance Mappings

Reports automatically map identified vulnerabilities to:
- **OWASP Top 10 for LLMs & Generative AI** (2025)
- **MITRE ATLAS** (Adversarial Threat Landscape for AI Systems)
- **SDAIA AI Ethics Principles** (Kingdom of Saudi Arabia)
- **NIST AI Risk Management Framework** (AI RMF 1.0)
- **Saudi Personal Data Protection Law (PDPL)**

---

## License

SawOne-Agentic is distributed under the MIT License by [hackin2minutes-oss](https://github.com/hackin2minutes-oss).
