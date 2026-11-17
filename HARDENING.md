<!-- markdownlint-disable -->

# Hardening Report: sigstore--gh-action-sigstore-python/v3.3.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `374911c4be584df24e6da57af2d990570ef0f859`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **sigstore--gh-action-sigstore-python/v3.3.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### prior-fix (severity: high)

Carried forward from this version's previous harden, which fixed it; fix it again unless the code no longer has the problem. The previous harden changed action.yml without recording a finding for it, and this analysis reported nothing there. Re-apply its security changes unless the code no longer needs them. The previous patch:
```diff
diff --git a/action.yml b/action.yml
index b1b33f3..038dc77 100644
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
     - uses: actions/upload-artifact@bbbca2ddaa5d8feaa63e36b76fdaad77386f024f # v7.0.0
       if: inputs.upload-signing-artifacts == 'true'
       with:
         name: "signing-artifacts-${{ github.job }}"
         path: "${{ env.GHA_SIGSTORE_PYTHON_INTERNAL_SIGNING_ARTIFACTS }}"
-
     - uses: softprops/action-gh-release@153bb8e04406b158c6c84fc1615b65b24149a1fe # v2.6.1
       if: inputs.release-signing-artifacts == 'true' && github.event_name == 'release' && github.event.action == 'published'
       with:
         files: "${{ env.GHA_SIGSTORE_PYTHON_INTERNAL_SIGNING_ARTIFACTS }}"

```

Locations:

- `action.yml`

## Iteration Notes

### Iteration 1

**Notes:**

I made no changes because action.yml already has every security property the previous fix was carried forward for. The only changes visible in the previous patch are deleted blank lines, which have no security effect. Its first hunk header says 16 lines were added, but those lines are missing from the patch, so I couldn't re-apply them. What I checked: (1) both third-party actions are pinned to full commit SHAs that match their tags: actions/upload-artifact@bbbca2dd… is v7.0.0 and softprops/action-gh-release@153bb8e0… is v2.6.1; (2) no `run:` step puts a `${{ }}` expression straight into the shell script; every input comes in through `env:` and is used as a quoted variable; (3) setup/setup.bash writes only the path it builds itself to GITHUB_OUTPUT, with no workflow-controlled value.

