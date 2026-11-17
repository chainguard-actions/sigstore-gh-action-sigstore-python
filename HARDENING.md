<!-- markdownlint-disable -->

# Hardening Report: sigstore--gh-action-sigstore-python/v3.4.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `374911c4be584df24e6da57af2d990570ef0f859`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **sigstore--gh-action-sigstore-python/v3.4.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### prior-fix (severity: high)

Carried forward from this version's previous harden, which fixed it; fix it again unless the code no longer has the problem. The previous harden changed action.yml without recording a finding for it, and this analysis reported nothing there. Re-apply its security changes unless the code no longer needs them. The previous patch:
```diff
diff --git a/action.yml b/action.yml
index baa9edf..9a29153 100644
--- a/action.yml
+++ b/action.yml
@@ -74,10 +74,26 @@ inputs:
     description: "run with debug logs (default false)"
     required: false
     default: "false"
-
 runs:
   using: "composite"
   steps:
     - name: Set up sigstore-python
       id: setup
       run: |
@@ -86,7 +102,6 @@ runs:
       env:
         GHA_SIGSTORE_PYTHON_INTERNAL_BE_CAREFUL_DEBUG: "${{ inputs.internal-be-careful-debug }}"
       shell: bash
-
     - name: Run sigstore-python
       id: sigstore-python
       run: |
@@ -109,14 +124,12 @@ runs:
         GHA_SIGSTORE_PYTHON_INTERNAL_BE_CAREFUL_DEBUG: "${{ inputs.internal-be-careful-debug }}"
         GHA_SIGSTORE_PYTHON_INPUTS: "${{ inputs.inputs }}"
       shell: bash
-
     - uses: actions/upload-artifact@043fb46d1a93c77aae656e7c1c64a875d1fc6a0a # v7.0.1
       if: inputs.upload-signing-artifacts == 'true'
       with:
         name: "signing-artifacts-${{ github.job }}"
         path: "${{ env.GHA_SIGSTORE_PYTHON_INTERNAL_SIGNING_ARTIFACTS }}"
-
     - uses: softprops/action-gh-release@b4309332981a82ec1c5618f44dd2e27cc8bfbfda # v3.0.0
       if: inputs.release-signing-artifacts == 'true' && github.event_name == 'release' && github.event.action == 'published'
       with:
         files: "${{ env.GHA_SIGSTORE_PYTHON_INTERNAL_SIGNING_ARTIFACTS }}"

```

Locations:

- `action.yml`

## Iteration Notes

### Iteration 1

**Fixes applied:** prior-fix

**Notes:**

I made no file changes because action.yml already has the security fixes. actions/upload-artifact and softprops/action-gh-release are pinned to full commit SHAs, and every input reaches the run: scripts through env: variables, so no expression is placed inline in shell code. The earlier patch only shows deleted blank lines, which make no difference to security. Its hunk header says 16 lines were added, but those lines are missing from the diff, so I couldn't see or re-apply them.

