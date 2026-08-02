# helm-repo

A personal Helm chart repository for Kubernetes applications, published as OCI artifacts to GitHub Container Registry (GHCR).

## Overview

This repository contains Helm charts for self-hosted services and personal projects. Charts are packaged and published automatically on every push to `main` that modifies files under `charts/`.

## Available Charts

| Chart | Description | Chart Version | App Version |
|-------|-------------|---------------|-------------|
| [affine](charts/affine) | AFFiNE — an open-source knowledge management and collaboration platform | 0.27.3 | 0.27.3 |
| [countdown](charts/countdown) | Simple countdown web application | 1.16.0 | 1.16.0 |
| [discord-bot](charts/discord-bot) | Custom Discord bot with scheduled reminders | 0.5.1 | 0.5.1 |
| [dyndns-cf](charts/dyndns-cf) | Dynamic DNS updater for Cloudflare | 1.0.1 | 1.0.1 |

## Usage

### Add the OCI registry

These charts are published to GHCR as OCI artifacts. You can pull and install a chart directly:

```bash
helm install my-release oci://ghcr.io/fgasquez/charts/<chart-name> --version <chart-version>
```

For example:

```bash
helm install my-affine oci://ghcr.io/fgasquez/charts/affine --version 0.1.4
```

### Install from local source

```bash
cd charts/<chart-name>
helm dependency update
helm install my-release . -f values.yaml
```

## Development

### Prerequisites

- [Helm](https://helm.sh/docs/intro/install/) 3.x
- A Kubernetes cluster (or a local tool like [kind](https://kind.sigs.k8s.io/) / [minikube](https://minikube.sigs.k8s.io/))

### Lint a chart

```bash
helm lint charts/<chart-name>
```

### Template a chart

```bash
helm template charts/<chart-name>
```

### Package a chart locally

```bash
helm package charts/<chart-name>
```

## Release Workflow

The `.github/workflows/release.yml` workflow handles automated publishing:

1. Triggers on pushes to `main` that modify `charts/**`
2. Packages each chart under `charts/`
3. Logs into GHCR using the built-in `GITHUB_TOKEN`
4. Pushes the packaged charts to `oci://ghcr.io/fgasquez/charts`

No manual intervention is required for publishing after a chart change is merged.

## Repository Structure

```
.
├── .github/
│   └── workflows/
│       └── release.yml       # OCI publish workflow
├── charts/
│   ├── affine/               # AFFiNE knowledge base
│   ├── countdown/            # Countdown web app
│   ├── discord-bot/          # Discord bot
│   └── dyndns-cf/            # Cloudflare dynamic DNS updater
└── README.md
```

## License

This repository is provided as-is for personal use. See individual charts for any application-specific licensing.
