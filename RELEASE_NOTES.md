# virt-api v1.9.1 — ReadyStack release `v1.9.1-CE-debian12-r3`

Generated 2026-11-25 from this release's build records and strategy. Statements that come from a single record name it in brackets; the others come from this release's strategy and build log.

## Release

- **Image:** `readystack/virtapi:v1.9.1-CE-debian12-r3` (linux/amd64). Index digest `sha256:af76df068b712edf9f4b42b434345b204211349c3449ec751108df29cf4bd234` [`docs/provenance/LOCKED_DIGEST.txt`].
- **Image manifest digest:** `sha256:d99410ac4e7f6c199998267c088b6756c99dbe8f6a9811a002f2ded83ae6acaa` [`TARGET_DIGEST.txt`].
- **Upstream:** virt-api v1.9.1 built from source at `v1.9.1` of https://github.com/kubevirt/kubevirt — upstream notes: https://github.com/kubevirt/kubevirt/releases/tag/v1.9.1 [`docs/provenance/BUILD_RECIPE.json`].
- **Base image:** `gcr.io/distroless/base-debian12@sha256:ca3f629c350fd1cb653caee7c5aed8967be4e43d9577fbb1cb4ed66c260e224e`; runtime user `nonroot-user`.
- **Build:** `source-rebuild-go`, compiled offline with `--network=none`.
- **Supersedes:** ReadyStack release `v1.9.1-CE-debian12-r2`.

## What changed in this release

- Upstream version unchanged (v1.9.1); ReadyStack rebuild.
- KubeVirt v1.9.1's virt-api is unchanged from the release this supersedes (v1.9.1-CE-debian12-r2); this release rebuilds it. Changes: github.com/insomniacslk/dhcp moves from v0.0.0-20240829085014-a3a4c1f04475 to v0.0.0-20260719225207-c76316d4aa82 in virt-api (GHSA-jp3c-6v3g-mpxv, high: a DHCP reply whose IPv4 header claims fewer than eight payload bytes made dhcpv4/nclient4 panic), in patch 0006, made with KubeVirt's own dependency-update path; no other module moves, and KubeVirt v1.10.0 still ships the earlier version. The image is dated when this release was cut (2026-11-25), no longer by the upstream commit. The image's version label now names this release. Settings, ports and data are those of v1.9.1-CE-debian12-r2: replace it with this image as before.

## Security status at release (measured 2026-11-25)

- **Docker Scout:** 0 fixable critical/high vulnerabilities; runs as `1001` (non-root); SBOM + provenance attestations present (SPDX SBOM + SLSA v1) [`docs/provenance/SCOUT_VERDICT.json`].
- **OSV cross-check:** no fixable critical/high vulnerability beyond Docker Scout's findings.
- **Signature:** cosign signature verified by ReadyStack's release gate before publishing; check it yourself with `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/virtapi:v1.9.1-CE-debian12-r3` (signatures are recorded in the public Sigstore transparency log).
- **ReadyStack release check at release:** passed (ReadyStack's own test, not a Docker Scout grade). Vulnerabilities are disclosed every day and the image never changes, so it is re-checked daily, beside Docker Scout's own dated grade, at https://readystack.dev/queue.

## Reproducibility

Rebuilds offline from this archive to the identical image digest `sha256:d99410ac4e7f6c199998267c088b6756c99dbe8f6a9811a002f2ded83ae6acaa`: run `./BUILD_OFFLINE.sh`, then `./VERIFY_OFFLINE.sh` (add `--online` to confirm the Docker Hub tag holds the same digest). Before publishing, ReadyStack rebuilt the kit with `./BUILD_OFFLINE.sh` and compared the result with the published digest [`docs/provenance/REPRO_VERIFICATION.json`], then ran `./BUILD_OFFLINE.sh` and `./VERIFY_OFFLINE.sh` from this archive (without `--online`).

## Validation

- 7 of 7 runbook checks passed (7 authored) on the stack's 3-node integration cluster, recorded 2026-10-29T02:34:55Z [`docs/validation/test-results.json`, from the run's record `docs/stack/RUNBOOK_EVIDENCE.json`]. They are the checks of the stack's operator runbook that name this component; no container of this image was started on its own for them. The record does not show this release's image (`sha256:d99410ac4e7f6c199998267c088b6756c99dbe8f6a9811a002f2ded83ae6acaa`) in that run: it lists the component's images as they were then, an earlier build or a tag, so the checks describe the component, not this digest.
- Failed cases are listed in `docs/validation/FAILED_TESTS.md`.

## Known issues

- **low** (ReadyStack package): VERIFY.md: The measured attestations are SLSA provenance v1 and SPDX only; the Verification Summary Attestation is not recorded on the digest and promotion is deferred, so the third verify-attestation command… [`RSD-virtapi-6078adac36`]
- Open review finding about these release notes (they are rendered from the defects ledger, and the next review checks them again): Names the runtime user by account name only; the numeric user is 1001, which is what a Kubernetes runAsUser/runAsNonRoot check sees. [`RSD-virtapi-60f52477a3`]

## Defects fixed

- 1 problem found before release and fixed before it shipped (1 by review); each is listed in `docs/defects/defects.json`.

## Verify this archive

```
sha256sum -c CHECKSUMS.sha256
./BUILD_OFFLINE.sh && ./VERIFY_OFFLINE.sh --online
cosign verify --key https://readystack.dev/keys/cosign.pub readystack/virtapi:v1.9.1-CE-debian12-r3
```

ReadyStack records every signature in the public Sigstore transparency log (Rekor), so the command needs no extra flags.

