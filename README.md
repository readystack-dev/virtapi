# virt-api: ReadyStack build kit

The offline build kit for the Docker image `readystack/virtapi:v1.9.1-CE-debian12-r2`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [v1.9.1-CE-debian12-r2](https://github.com/readystack-dev/virtapi/releases/tag/v1.9.1-CE-debian12-r2)
- Image: [`docker.io/readystack/virtapi:v1.9.1-CE-debian12-r2`](https://hub.docker.com/r/readystack/virtapi/tags), manifest digest `sha256:38ee20d8459ac3344e048c09fb4295a29ad9615f08037dfb8a2e651cee253ae2`
- Product page: https://readystack.dev/products/virtapi
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=virtapi

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
