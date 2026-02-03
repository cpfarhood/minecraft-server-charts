# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Kubernetes Helm chart repository for Minecraft-related services. Contains five charts under `charts/`:

- **minecraft** — Java Edition server (itzg/minecraft-server)
- **minecraft-bedrock** — Bedrock Edition server (itzg/minecraft-bedrock-server)
- **minecraft-proxy** — Velocity proxy server
- **mc-router** — Minecraft connection router (itzg/mc-router)
- **rcon-web-admin** — Web-based RCON administration UI

## Common Commands

### Linting

```bash
# Lint all changed charts (requires chart-testing CLI: https://github.com/helm/chart-testing)
ct lint

# Lint a specific chart
helm lint charts/minecraft
```

### Testing

```bash
# Run integration tests against changed charts (requires a running Kind cluster)
ct install

# Create a Kind cluster for testing
kind create cluster

# Template a chart locally to inspect rendered output
helm template my-release charts/minecraft -f charts/minecraft/ci/test-values.yaml
```

Each chart has a `ci/test-values.yaml` with minimal overrides used by CI for installation tests.

### Releasing

Releases are automated. Pushing to `master` triggers `.github/workflows/release.yaml`, which packages all charts and publishes them to the Gitea Helm registry at `git.farh.net`. Pushes to other branches run the package step without publishing.

## Architecture

### Chart Structure (per chart)

```
charts/<name>/
├── Chart.yaml              # Version, metadata, dependencies
├── values.yaml             # Default configuration
├── values.schema.json      # JSON Schema validation (where present)
├── templates/
│   ├── _helpers.tpl        # Template helper functions
│   ├── deployment.yaml     # Main workload (Deployment or StatefulSet)
│   ├── *-svc.yaml          # Service definitions
│   └── ...                 # Other resources (PVCs, secrets, ingress, RBAC)
└── ci/
    └── test-values.yaml    # Minimal values for CI testing
```

### Key Design Patterns

**Workload toggle**: The `minecraft` chart supports both Deployment and StatefulSet via `workloadAsStatefulSet` in values.yaml. This affects PVC handling and update strategy.

**Template helpers** (`_helpers.tpl`): Charts use helpers for name generation, Kubernetes version-aware API selection (e.g., `minecraft.ingress.apiVersion`), and OCI-compatible chart naming (replacing `+` with `_`).

**Dual-stack networking**: Services support IPv4/IPv6 dual-stack via `minecraftServer.serviceAnnotations` and `ipFamilyPolicy`/`ipFamilies` fields. The chart avoids imposing defaults, relying on Kubernetes defaults instead.

**Backup methods**: The `minecraft` chart supports three backup strategies (tar, rclone, restic), each with distinct volume mount and sidecar patterns. The helper `isResticWithRclone` detects when restic uses rclone as a backend.

**Security contexts**: Default pod security uses `runAsUser: 1000`, `runAsNonRoot: true`, `readOnlyRootFilesystem: true`, and seccomp RuntimeDefault profile.

### CI Pipeline

PRs trigger `.github/workflows/lint-test.yaml`:
1. `ct list-changed` to detect modified charts
2. `ct lint` for Helm linting
3. Kind cluster creation with MetalLB for LoadBalancer testing
4. `ct install` for integration tests

## Conventions

- **Commit messages**: Follow conventional commits format (`fix(scope):`, `feat(scope):`, `chore:`)
- **Chart versioning**: Bump `version` in Chart.yaml when modifying a chart
- **Values schema**: The `minecraft` chart validates values against `values.schema.json` (JSON Schema draft-07). Update the schema when adding/changing values structure.
- **Single replica**: Minecraft servers are not horizontally scalable; `replicaCount` should remain 1
