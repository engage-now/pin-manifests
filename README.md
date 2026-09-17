# pin-manifests

Public, signed SSL pin manifest for [engage-now-mobile](https://github.com/engage-now/engage-now-mobile), published by that repo's CI.

This repo is intentionally public and unauthenticated — the mobile app fetches `manifest.json` and `manifest.json.sig` from here over plain HTTPS with no token, so a routine backend certificate rotation can be picked up without an app store release. **Trust does not come from this repo's contents being fetched over TLS** — it comes from verifying `manifest.json.sig` against a public key baked into the app. See [`docs/RUNBOOK-SSL-PIN-ROTATION.md`](https://github.com/engage-now/engage-now-mobile/blob/main/docs/RUNBOOK-SSL-PIN-ROTATION.md) in the mobile repo ("Remote pin manifest" section) for the full design.

Nothing in this repo is sensitive: `manifest.json` lists SPKI SHA-256 hashes derived from public server certificates, and `manifest.json.sig` is a digital signature — signatures are meant to be distributed publicly. The one sensitive artifact in this system, the private signing key, is **not** here — it lives only in a GitHub Actions secret on `engage-now-mobile`.

**Do not edit files in this repo by hand.** They're overwritten by the `sign-pin-manifest.yml` workflow in `engage-now-mobile` every time it runs.
