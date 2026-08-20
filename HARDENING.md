<!-- markdownlint-disable -->

# Hardening Report: easimon--maximize-build-space/v6

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **easimon--maximize-build-space/v6** was hardened automatically. 28 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Sub-rule (a): Multiple ${{ inputs.* }} expressions are interpolated directly inside run: shell commands in the 'Maximize build disk space' step. This allows any caller of the composite action to inject arbitrary shell commands. Offending lines include: `BUILD_MOUNT_PATH="${{ inputs.build-mount-path }}"`, `if [[ ${{ inputs.remove-dotnet }} == 'true' ]]`, `ROOT_RESERVE_KB=$(expr ${{ inputs.root-reserve-mb }} \* 1024)`, `sudo touch "${{ inputs.pv-loop-path }}"`, `sudo lvcreate -L "${{ inputs.swap-size-mb }}M"`, `if [[ ${{ inputs.overprovision-lvm }} == 'true' ]]`, and many more. All inputs should be mapped to env: variables and those env vars should be double-quoted in the shell script.

Locations:

- `action.yml:77`
- `action.yml:84`
- `action.yml:85`
- `action.yml:86`
- `action.yml:87`
- `action.yml:89`
- `action.yml:90`
- `action.yml:92`
- `action.yml:95`
- `action.yml:98`
- `action.yml:103`
- `action.yml:107`
- `action.yml:111`
- `action.yml:120`
- `action.yml:124`
- `action.yml:125`
- `action.yml:129`
- `action.yml:133`
- `action.yml:134`
- `action.yml:139`
- `action.yml:145`

### script-injection (severity: high)

Sub-rule (a): Multiple ${{ ... }} expressions are interpolated directly inside run: shell commands in .github/workflows/test.yaml. Offending lines include: `echo "FREE_GIG_BEFORE=$(df ... "${{ github.workspace }}" ...)" >> $GITHUB_ENV` (line 34), `echo "FREE_GIG_AFTER=$(df ... "${{ github.workspace }}" ...)" >> $GITHUB_ENV` (line 44), `REPORT_FILENAME_BASE="${REPORT_DIR}/${{ matrix.os }}_${{ matrix.remove-android }}_${{ matrix.remove-dotnet }}_${{ matrix.remove-haskell }}"` (line 47), `REMOVE_ANDROID="${{ matrix.remove-android }}"` (line 55), `"os": "${{ matrix.os }}"` (line 62), and `cat ${{ env.REPORT_DIR }}/${{ env.REPORT_FILE }} >> README.md` (line 94). All ${{ }} expressions must be moved to env: blocks and the env vars double-quoted in the shell.

Locations:

- `.github/workflows/test.yaml:34`
- `.github/workflows/test.yaml:44`
- `.github/workflows/test.yaml:47`
- `.github/workflows/test.yaml:55`
- `.github/workflows/test.yaml:56`
- `.github/workflows/test.yaml:57`
- `.github/workflows/test.yaml:62`
- `.github/workflows/test.yaml:94`

### github-env-injection (severity: high)

The workflow writes a value derived from ${{ github.workspace }} directly to $GITHUB_ENV without sanitization (no `printf '%s' ... | tr -d '\n\r'` step). This occurs in two steps: 'Determine free space before' (line 34) and 'Determine free space after' (line 44). A malicious value in github.workspace could inject additional environment variable assignments via newline characters.

Locations:

- `.github/workflows/test.yaml:34`
- `.github/workflows/test.yaml:44`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and neither job (test-action, collect-reports) defines a job-level `permissions:` block. Without explicit permissions, the workflow inherits the default repository permissions, which may be overly broad (e.g., write access to contents). A minimal permissions block should be added.

Locations:

- `.github/workflows/test.yaml:1`

### unpinned-uses (severity: high)

Multiple `uses:` references in the workflow are pinned to mutable version tags rather than immutable full-length SHA digests, making the workflow vulnerable to supply-chain attacks if the tag is moved. Failing references: `actions/checkout@v2` (lines 36 and 90), `actions/upload-artifact@v2` (line 67), `actions/download-artifact@v2` (line 79). Each should be replaced with the full 40-character commit SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/test.yaml:36`
- `.github/workflows/test.yaml:67`
- `.github/workflows/test.yaml:79`
- `.github/workflows/test.yaml:90`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.build-mount-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:70`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.root-reserve-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:77`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.temp-reserve-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:78`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.swap-size-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:79`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.overprovision-lvm }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:80`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:82`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tmp-pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:83`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-dotnet }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:85`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-android }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:88`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-haskell }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:91`

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

shell injection: expression "${{ inputs.root-reserve-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:119`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:123`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:123`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:124`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.temp-reserve-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:129`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tmp-pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:133`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tmp-pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:133`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tmp-pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:134`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.swap-size-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:142`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.overprovision-lvm }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:149`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, github-env-injection, missing-permissions, unpinned-uses, static-inline-injection

**Notes:**

Fixed all findings in action.yml and .github/workflows/test.yaml:

1. action.yml - script-injection/static-inline-injection: Added an `env:` block to the 'Maximize build disk space' step mapping all 10 inputs (build-mount-path, root-reserve-mb, temp-reserve-mb, swap-size-mb, overprovision-lvm, pv-loop-path, tmp-pv-loop-path, remove-dotnet, remove-android, remove-haskell) to INPUT_* environment variables. Replaced all ${{ inputs.* }} expressions in the run: block with double-quoted ${INPUT_*} references.

2. test.yaml - missing-permissions: Added `permissions: {}` at the top level of the workflow.

3. test.yaml - unpinned-uses: Pinned all four action references to full SHAs: actions/checkout@v2 → 0717577d45739eb3c851188b29f50ed6c0b2194e, actions/upload-artifact@v2 → 82c141cc518b40d92cc801eee768e7aafc9c2fa2, actions/download-artifact@v2 → cbed621e49e4c01b044d60f6c80ea4ed6328b281.

4. test.yaml - script-injection: Moved ${{ github.workspace }} to WORKSPACE env var in 'Determine free space before/after' steps; moved ${{ matrix.* }} expressions to MATRIX_* env vars in 'Calculate freed space' step; replaced ${{ env.REPORT_DIR }}/${{ env.REPORT_FILE }} with env var references.

5. test.yaml - github-env-injection: Sanitized the workspace path with `printf '%s' "$WORKSPACE" | tr -d '\n\r'` before using it in the df command and writing to GITHUB_ENV.

