# Upstream review

Source: [grunt-karma@4.0.2, f9619531457237082176641a9103749e3faf462a](https://github.com/karma-runner/grunt-karma/commit/f9619531457237082176641a9103749e3faf462a). Existing published runtime files match the integrity-checked upstream npm tarball byte-for-byte. Generated adapter files, where applicable, are built from original sources. License and authorship notices remain unchanged.

## Issue triage (2026-09-29)

- [#311: Prototype pollution report](https://github.com/karma-runner/grunt-karma/issues/311): Keep the upstream4.0.2 source identity verified against the npm tarball; resolve the existing lodash^4.17.10 range to the patched release. Exercise all original single/config/merge/flatten task cases in real Chromium.

No upstream contact was made and no blanket issue-resolution claim is implied. Node24 is used for development only; published engine declarations remain unchanged.

## Verification

`npm ci --ignore-scripts`, `npm run build --if-present`, `npm test`, `npm run test:package`, `npm audit --audit-level=low`. Exact CI tarballs require successful CI and CodeQL before provenance-enabled publication.
