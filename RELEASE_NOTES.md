# virt-api v1.9.1 — ReadyStack release `v1.9.1-CE-debian12-r2`

Generated 2026-11-08 from this release's build records and strategy. Statements that come from a single record name it in brackets; the others come from this release's strategy and build log.

## Release

- **Image:** `readystack/virtapi:v1.9.1-CE-debian12-r2` (linux/amd64). Index digest `sha256:65177dc67dc11ed39de81fa63968e08cc768b7525fcde52aa0c8dc959f670a31` [`docs/provenance/LOCKED_DIGEST.txt`].
- **Image manifest digest:** `sha256:38ee20d8459ac3344e048c09fb4295a29ad9615f08037dfb8a2e651cee253ae2` [`TARGET_DIGEST.txt`].
- **Upstream:** virt-api v1.9.1 built from source at `v1.9.1` of https://github.com/kubevirt/kubevirt — upstream notes: https://github.com/kubevirt/kubevirt/releases/tag/v1.9.1 [`docs/provenance/BUILD_RECIPE.json`].
- **Base image:** `gcr.io/distroless/base-debian12@sha256:ca3f629c350fd1cb653caee7c5aed8967be4e43d9577fbb1cb4ed66c260e224e`; runtime user `nonroot-user`.
- **Build:** `source-rebuild-go`, compiled offline with `--network=none`.
- **Supersedes:** ReadyStack release `v1.9.1-CE-debian12-r1`.

## What changed in this release

- Upstream version unchanged (v1.9.1); ReadyStack rebuild.
- KubeVirt v1.9.1's virt-api is unchanged from the release this supersedes (v1.9.1-CE-debian12-r1); this release rebuilds it. Changes: golang.org/x/net moves from v0.60.0 to v0.62.0 in every binary it links (GO-2026-6860, GO-2026-6866: CVE-2026-78661, high), with the versions it requires: golang.org/x/crypto v0.58.0, golang.org/x/sys v0.49.0, golang.org/x/text v0.43.0, golang.org/x/term v0.47.0 and golang.org/x/tools v0.51.0 (patch 0006, made with KubeVirt's own dependency-update path; google.golang.org/grpc stays at v1.83.2). The image's version label now names this release. Settings, ports and data are those of v1.9.1-CE-debian12-r1: replace it with this image as before.

## Security status at release (measured 2026-11-08)

- **Docker Scout:** 0 fixable critical/high vulnerabilities; runs as `1001` (non-root); SBOM + provenance attestations present (SPDX SBOM + SLSA v1) [`docs/provenance/SCOUT_VERDICT.json`].
- **OSV cross-check:** no fixable critical/high vulnerability beyond Docker Scout's findings.
- **Signature:** cosign signature verified by ReadyStack's release gate before publishing; check it yourself with `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/virtapi:v1.9.1-CE-debian12-r2` (signatures are recorded in the public Sigstore transparency log).
- **ReadyStack release check at release:** passed (ReadyStack's own test, not a Docker Scout grade). Vulnerabilities are disclosed every day and the image never changes, so it is re-checked daily, beside Docker Scout's own dated grade, at https://readystack.dev/queue.

## Reproducibility

Rebuilds offline from this archive to the identical image digest `sha256:38ee20d8459ac3344e048c09fb4295a29ad9615f08037dfb8a2e651cee253ae2`: run `./BUILD_OFFLINE.sh`, then `./VERIFY_OFFLINE.sh` (add `--online` to confirm the Docker Hub tag holds the same digest). Before publishing, ReadyStack rebuilt the kit with `./BUILD_OFFLINE.sh` and compared the result with the published digest [`docs/provenance/REPRO_VERIFICATION.json`], then ran `./BUILD_OFFLINE.sh` and `./VERIFY_OFFLINE.sh` from this archive (without `--online`).

## Validation

- 7 of 7 runbook checks passed (7 authored) on the stack's 3-node integration cluster, recorded 2026-10-29T02:34:55Z [`docs/validation/test-results.json`, from the run's record `docs/stack/RUNBOOK_EVIDENCE.json`]. They are the checks of the stack's operator runbook that name this component; no container of this image was started on its own for them. The record does not show this release's image (`sha256:38ee20d8459ac3344e048c09fb4295a29ad9615f08037dfb8a2e651cee253ae2`) in that run: it lists the component's images as they were then, an earlier build or a tag, so the checks describe the component, not this digest.
- Failed cases are listed in `docs/validation/FAILED_TESTS.md`.

## Known issues

- **low** (ReadyStack package): Docker Hub README: Says the build kit is free for any registered account (also line 15, 'free with an account'), but the bundle MANIFEST prices this release's kit at 1000 cents and marks it not a free release. [`RSD-virtapi-93ee77d3a1`]
- **low** (ReadyStack package): VERIFY.md: The release's measured attestations list only SLSA provenance v1 and SPDX; no record shows the Verification Summary Attestation, and the promotion record says promotion is deferred, so the third… [`RSD-virtapi-a7f7baa471`]
- Open review finding about these release notes (they are rendered from the defects ledger, and the next review checks them again): Names the runtime user by account name only; every other record (SECURITY_REPORT line 7, VERIFY line 33, IMAGE_CONFIG User) gives the numeric user 1001, which is what a Kubernetes… [`RSD-virtapi-60f52477a3`]

## Verify this archive

```
sha256sum -c CHECKSUMS.sha256
./BUILD_OFFLINE.sh && ./VERIFY_OFFLINE.sh --online
cosign verify --key https://readystack.dev/keys/cosign.pub readystack/virtapi:v1.9.1-CE-debian12-r2
```

ReadyStack records every signature in the public Sigstore transparency log (Rekor), so the command needs no extra flags.

