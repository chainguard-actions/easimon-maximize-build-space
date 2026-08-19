<!-- markdownlint-disable -->

# Hardening Report: easimon--maximize-build-space/v8

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **easimon--maximize-build-space/v8** was hardened automatically. 32 finding(s) were identified and resolved across 2 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Sub-rule (a): The 'Maximize build disk space' run: block in action.yml directly interpolates ${{ inputs.* }} expressions inside shell commands. Examples include: `BUILD_MOUNT_PATH="${{ inputs.build-mount-path }}"`, `ROOT_RESERVE_KB=$(expr ${{ inputs.root-reserve-mb }} \* 1024)`, `sudo touch "${{ inputs.pv-loop-path }}"`, `sudo lvcreate -L "${{ inputs.swap-size-mb }}M"`, `sudo chown -R "${{ inputs.build-mount-path-ownership }}"`, and many more. All 28 occurrences of ${{ inputs.* }} are interpolated directly into shell before the shell ever sees them, enabling command injection via crafted input values.

Locations:

- `action.yml:72`

### script-injection (severity: high)

Sub-rule (a): The workflow test.yaml directly interpolates ${{ github.workspace }}, ${{ matrix.* }}, and ${{ env.* }} expressions inside run: shell commands. Offending lines include: `echo "FREE_GIG_BEFORE=$(df ... "${{ github.workspace }}" ...)" >> $GITHUB_ENV`, `REPORT_FILENAME_BASE="${REPORT_DIR}/${{ matrix.os }}_${{ matrix.remove-android }}_..."`, `REMOVE_ANDROID="${{ matrix.remove-android }}"`, `"os": "${{ matrix.os }}"` inside a heredoc, and `cat ${{ env.REPORT_DIR }}/${{ env.REPORT_FILE }} >> README.md`. Any ${{ ... }} expression interpolated directly in a run: block is a script-injection risk.

Locations:

- `.github/workflows/test.yaml:49`
- `.github/workflows/test.yaml:67`
- `.github/workflows/test.yaml:71`
- `.github/workflows/test.yaml:83`
- `.github/workflows/test.yaml:91`
- `.github/workflows/test.yaml:135`

### unpinned-uses (severity: high)

The workflow .github/workflows/test.yaml references external actions using mutable version tags instead of full 40-character SHA digests, making the workflow vulnerable to supply-chain attacks if those tags are moved. Unpinned references: `actions/checkout@v3` (×2), `actions/upload-artifact@v3` (×2), `actions/download-artifact@v3` (×1).

Locations:

- `.github/workflows/test.yaml:53`
- `.github/workflows/test.yaml:107`
- `.github/workflows/test.yaml:117`
- `.github/workflows/test.yaml:128`
- `.github/workflows/test.yaml:131`

### missing-permissions (severity: medium)

The workflow .github/workflows/test.yaml has no top-level `permissions:` key, and neither of its jobs (`test-action`, `collect-reports`) defines a job-level `permissions:` block. This means the workflow runs with the default token permissions (which can include write access to repository contents), violating the principle of least privilege.

Locations:

- `.github/workflows/test.yaml:1`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.build-mount-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:82`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.root-reserve-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:89`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.temp-reserve-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:90`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.swap-size-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:91`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.overprovision-lvm }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:92`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:94`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tmp-pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:95`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-dotnet }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:97`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-android }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:100`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-haskell }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:103`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-codeql }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:106`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-docker-images }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:109`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-dotnet }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:115`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-android }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:118`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-haskell }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:121`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-codeql }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:124`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-docker-images }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:127`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.root-reserve-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:143`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:147`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:147`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:148`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.temp-reserve-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:153`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tmp-pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:157`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tmp-pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:157`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tmp-pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:158`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.swap-size-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:166`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.overprovision-lvm }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:173`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.build-mount-path-ownership }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:182`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, static-inline-injection, unpinned-uses, missing-permissions

**Notes:**

Fixed all findings:
1. action.yml: Moved all 13 ${{ inputs.* }} expressions from the run: block into an env: block on the 'Maximize build disk space' step. Shell script now uses environment variables (INPUT_BUILD_MOUNT_PATH, INPUT_ROOT_RESERVE_MB, etc.).
2. test.yaml: Moved ${{ github.workspace }} and ${{ matrix.* }} expressions from run: blocks into env: blocks on their respective steps.
3. test.yaml: Pinned all 5 action references to full SHA digests: actions/checkout@a37ce9120846195fa4ece8f58b268e6043cb2f26 (v3), actions/upload-artifact@ff15f0306b3f739f7b6fd43fb5d26cd321bd4de5 (v3), actions/download-artifact@9bc31d5ccc31df68ecc42ccf4149144866c47d8a (v3).
4. test.yaml: Added top-level permissions: contents: write, with job-level overrides (test-action: contents: read, collect-reports: contents: write).

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed four unquoted shell variable expansions in expr commands in action.yml. The variables $ROOT_FREE_KB, $ROOT_RESERVE_KB, $ROOT_LVM_SIZE_KB, $TMP_FREE_KB, $TMP_RESERVE_KB, and $TMP_LVM_SIZE_KB (derived from user-controlled inputs root-reserve-mb and temp-reserve-mb) are now double-quoted in their expr invocations, preventing word-splitting and shell metacharacter injection.

