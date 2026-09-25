<!-- markdownlint-disable -->

# Hardening Report: sigstore--gh-action-sigstore-python/v3.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **sigstore--gh-action-sigstore-python/v3.0.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Two `uses:` references in action.yml are pinned to mutable version tags instead of immutable 40-character commit SHAs. This exposes the action to supply-chain attacks if the upstream tag is moved or the repository is compromised:
- `actions/upload-artifact@v4` (line 105) — `v4` is a mutable tag
- `softprops/action-gh-release@v2` (line 111) — `v2` is a mutable tag

These should be replaced with full SHA pins, e.g.:
  `uses: actions/upload-artifact@<40-char-sha> # v4`
  `uses: softprops/action-gh-release@<40-char-sha> # v2`

Locations:

- `action.yml:105`
- `action.yml:111`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned two mutable tag references in hardened/action/action.yml to immutable commit SHAs:
- `actions/upload-artifact@v4` → `actions/upload-artifact@ea165f8d65b6e75b540449e92b4886f43607fa02 # v4` (line 105)
- `softprops/action-gh-release@v2` → `softprops/action-gh-release@3bb12739c298aeb8a4eeaf626c5b8d85266b0e65 # v2` (line 111)

SHAs were resolved using lookup_action_sha against the upstream repositories.

