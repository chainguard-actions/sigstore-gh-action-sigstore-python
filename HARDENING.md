<!-- markdownlint-disable -->

# Hardening Report: sigstore--gh-action-sigstore-python/v3.5.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `374911c4be584df24e6da57af2d990570ef0f859`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **sigstore--gh-action-sigstore-python/v3.5.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### prior-fix (severity: high)

Carried forward from this version's previous harden, which fixed it; fix it again unless the code no longer has the problem. The previous harden changed action.yml without recording a finding for it, and this analysis reported nothing there. Re-apply its security changes unless the code no longer needs them. The previous patch:
```diff
diff --git a/action.yml b/action.yml
index 2ab78e2..ee96e77 100644
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
     - uses: softprops/action-gh-release@3d0d9888cb7fd7b750713d6e236d1fcb99157228 # v3.0.2
       if: inputs.release-signing-artifacts == 'true' && github.event_name == 'release' && github.event.action == 'published'
       with:
         files: "${{ env.GHA_SIGSTORE_PYTHON_INTERNAL_SIGNING_ARTIFACTS }}"

```

Locations:

- `action.yml`

## Iteration Notes

### Iteration 1

**Notes:**

No changes made. The carried-forward finding does not apply to the current code. The old patch's visible changes are only deleted blank lines, which don't affect security. Its hunk header says 16 lines were added near the end of the inputs: block, but the diff doesn't include them, so there was nothing concrete to re-apply. action.yml already pins both uses: lines to full SHAs with the tag in a comment (upload-artifact v7.0.1, action-gh-release v3.0.2). Every input reaches the run: steps through env: and is read as a quoted shell variable. A search of the action for action_ref, GITHUB_ACTION_REF, curl and wget found nothing.

