# 🧭 Helm Template Review Action

> **Renders Helm chart templates, parses generated resources, and posts a comprehensive Pull Request comment.**

[![GitHub Marketplace](https://img.shields.io/badge/GitHub%20Marketplace-Helm%20Template%20Review%20Action-blue.svg)](https://github.com/marketplace/actions/helm-template-review-action)
[![GitHub license](https://img.shields.io/github/license/your-org/helm-template-review-action.svg)](LICENSE)
[![GitHub release](https://img.shields.io/github/v/release/your-org/helm-template-review-action)](https://github.com/your-org/helm-template-review-action/releases)

---

## 🚀 Executive Summary

The **Helm Template Review Action** provides developers with instant, precise feedback on the Kubernetes manifests rendered by their Helm charts during Pull Request workflows.

It executes `helm template` on a specified chart, parses the generated YAML, and posts a **structured Markdown summary** as a PR comment — including a collapsible block containing the full rendered manifest.

---

## 🔍 Why Use This Action?

| Use Case | Benefit |
|-----------|----------|
| **Configuration Review** | Assess infrastructure configuration changes without deploying to a live cluster. |
| **Error Mitigation** | Detect Helm rendering or templating errors early in CI. |
| **Logic Verification** | Validate Helm conditionals and chart logic directly from PRs. |

---

## ✨ Core Features

- 🧩 **Real-Time Template Visualization** — Runs `helm template` and posts a preview as a Pull Request comment.
- 📊 **Resource Summary** — Lists resource kinds (e.g., Deployment, Service, Ingress) for quick inspection.
- 📦 **Comprehensive YAML Access** — Collapsible block with complete rendered YAML.
- 🔁 **Smart Comment Updating** — Detects and updates previous comments to keep PRs clean.
- ⚙️ **Custom Helm Arguments** — Supports `--values`, `--set`, or any additional Helm CLI options.

---

## ⚙️ Example Workflow

```yaml
name: Helm Review

on:
  pull_request:
    branches:
      - main

jobs:
  template_preview:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Generate Helm Template Preview
        uses: fulgas/helm-template-review-action:v1
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          chart-path: ./my-app/helm-chart
          helm-args: "--namespace staging --values values/staging.yaml"
