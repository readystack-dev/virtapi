# virt-api: ReadyStack build kit

The offline build kit for the Docker image `readystack/virtapi:v1.9.1-CE-debian12-r2`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [v1.9.1-CE-debian12-r2](https://github.com/readystack-dev/virtapi/releases/tag/v1.9.1-CE-debian12-r2)
- Image: [`docker.io/readystack/virtapi:v1.9.1-CE-debian12-r2`](https://hub.docker.com/r/readystack/virtapi/tags), manifest digest `sha256:38ee20d8459ac3344e048c09fb4295a29ad9615f08037dfb8a2e651cee253ae2`
- Product page: https://readystack.dev/products/virtapi
- Source and build recipe: https://readystack.dev/products/virtapi/recipe
- Build trail: https://readystack.dev/products/virtapi/trail/v1.9.1-CE-debian12-r2
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=virtapi

## The image

the API server KubeVirt registers with Kubernetes for its subresources (console, VNC, port-forward, migration) and the validating and mutating webhooks for KubeVirt's custom resources.

## Who uses virt-api and why

Kubernetes cluster administrators who run virtual machines in their clusters with KubeVirt.

virt-api is KubeVirt's API server and the entry point for virtualisation requests. It fills in defaults for virtual machine definitions and validates them.

A typical use: When a user creates or changes a virtual machine in a cluster running KubeVirt, the request passes through virt-api, which applies default settings and rejects invalid definitions before they are stored as Kubernetes resources.

From the upstream project's own description: https://github.com/kubevirt/kubevirt/blob/main/docs/components.md, https://github.com/kubevirt/kubevirt.

## This release

- Docker Scout policy grade at release: **A** (94%), graded 2026-11-08 with `docker scout policy` (CLI 1.26.0, docker-default configuration).
  - Docker Scout counts 3 packages with copyleft licences (GPL, LGPL), all of them operating-system packages (it counts only packages whose licence it can read; the SBOM lists every component).
- Signed with ReadyStack's release key (fingerprint `04daa92344a52dbc`): https://readystack.dev/keys/cosign.pub.
- Runs as a non-root user (`1001`).
- Attestations on the image: an SPDX SBOM and SLSA provenance v1.
- Rebuilt from this kit with network egress blocked on 2026-11-08; the rebuilt image digest is the published one.
- Base: Debian 12.

The current grade, measured again every day, is on https://readystack.dev/products/virtapi.

virt-api is distributed under its upstream licence (Apache-2.0); the kit contains upstream's source under that licence, and each vendored component under its own.

## Download

From the [v1.9.1-CE-debian12-r2 release](https://github.com/readystack-dev/virtapi/releases/tag/v1.9.1-CE-debian12-r2): `ReadyStack-virtapi-v1.9.1-CE-debian12-r2.tar.gz` (1.1 GB), SHA-256 `1698e5a8f45d3f6159123cae78e287d36fbb0d0cf0d4a933dd7d0d2afba33159`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-virtapi-v1.9.1-CE-debian12-r2.rebuild.json.sigstore ReadyStack-virtapi-v1.9.1-CE-debian12-r2.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-virtapi-v1.9.1-CE-debian12-r2.tar.gz
cd v1.9.1-CE-debian12-r2
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-virtapi-v1.9.1-CE-debian12-r2.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/virtapi/recipe. The complete kit is the release download. Each release is a tag here.

— ReadyStack · https://readystack.dev
