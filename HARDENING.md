<!-- markdownlint-disable -->

# Hardening Report: easimon--maximize-build-space/v7

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **easimon--maximize-build-space/v7** was hardened automatically. 31 finding(s) were identified and resolved across 2 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The composite action's 'Maximize build disk space' run: block directly interpolates multiple ${{ inputs.* }} expressions inside shell commands (sub-rule a). Before the shell executes, GitHub Actions substitutes these values verbatim into the script string, allowing an attacker-controlled input to inject arbitrary shell commands. Affected interpolations include: ${{ inputs.build-mount-path }}, ${{ inputs.root-reserve-mb }}, ${{ inputs.temp-reserve-mb }}, ${{ inputs.swap-size-mb }}, ${{ inputs.overprovision-lvm }}, ${{ inputs.pv-loop-path }}, ${{ inputs.tmp-pv-loop-path }}, ${{ inputs.remove-dotnet }}, ${{ inputs.remove-android }}, ${{ inputs.remove-haskell }}, ${{ inputs.remove-codeql }}, ${{ inputs.remove-docker-images }}. All of these should be moved to env: variables and then referenced as double-quoted shell variables (e.g., "$INPUT_VAR").

Locations:

- `action.yml:57`

### github-env-injection (severity: high)

In the workflow's 'Determine free space before' step, the value of ${{ github.workspace }} is embedded directly in a command substitution that writes to $GITHUB_ENV without sanitization (no `printf '%s' ... | tr -d '\n\r'` step). A newline in the workspace path could allow injection of arbitrary environment variables. Similarly, the 'Determine free space after' step has the same pattern. Offending lines: `echo "FREE_GIG_BEFORE=$(df --output=avail --sync -BG "${{ github.workspace }}" | tail -1 | sed 's/[^0-9]*//g')" >> $GITHUB_ENV`

Locations:

- `.github/workflows/test.yaml:44`
- `.github/workflows/test.yaml:55`

### unpinned-uses (severity: high)

All uses: references in the workflow use mutable version tags (@v2) instead of full 40-character commit SHAs. This means the action code can change without notice, enabling supply-chain attacks. Unpinned references: actions/checkout@v2 (lines ~47, ~107, ~116), actions/upload-artifact@v2 (line ~89), actions/download-artifact@v2 (line ~101).

Locations:

- `.github/workflows/test.yaml:47`
- `.github/workflows/test.yaml:89`
- `.github/workflows/test.yaml:101`
- `.github/workflows/test.yaml:107`
- `.github/workflows/test.yaml:116`

### missing-permissions (severity: medium)

The workflow file .github/workflows/test.yaml has no top-level `permissions:` key, and neither the 'test-action' job nor the 'collect-reports' job defines a `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (write access to contents, pull-requests, etc.).

Locations:

- `.github/workflows/test.yaml:1`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.build-mount-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:78`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.root-reserve-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:85`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.temp-reserve-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:86`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.swap-size-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:87`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.overprovision-lvm }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:88`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:90`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tmp-pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:91`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-dotnet }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:93`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-android }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:96`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-haskell }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:99`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-codeql }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:102`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-docker-images }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:105`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-dotnet }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:111`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-android }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:114`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-haskell }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:117`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-codeql }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:120`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-docker-images }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:123`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.root-reserve-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:139`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:143`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:143`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:144`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.temp-reserve-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:149`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tmp-pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:153`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tmp-pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:153`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tmp-pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:154`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.swap-size-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:162`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.overprovision-lvm }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:169`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, static-inline-injection, github-env-injection, unpinned-uses, missing-permissions

**Notes:**

Fixed all findings in action.yml and .github/workflows/test.yaml:

1. action.yml - script-injection/static-inline-injection: Moved all 12 ${{ inputs.* }} expressions from the 'Maximize build disk space' run: block into an env: block (INPUT_BUILD_MOUNT_PATH, INPUT_ROOT_RESERVE_MB, INPUT_TEMP_RESERVE_MB, INPUT_SWAP_SIZE_MB, INPUT_OVERPROVISION_LVM, INPUT_PV_LOOP_PATH, INPUT_TMP_PV_LOOP_PATH, INPUT_REMOVE_DOTNET, INPUT_REMOVE_ANDROID, INPUT_REMOVE_HASKELL, INPUT_REMOVE_CODEQL, INPUT_REMOVE_DOCKER_IMAGES). All shell references now use double-quoted ${VAR} forms.

2. test.yaml - github-env-injection: Moved ${{ github.workspace }} to env var GITHUB_WORKSPACE_PATH and sanitized with `printf '%s' "$GITHUB_WORKSPACE_PATH" | tr -d '\n\r'` before use in both 'Determine free space before' and 'Determine free space after' steps.

3. test.yaml - unpinned-uses: Pinned all 5 uses: references to full commit SHAs: actions/checkout@v2→0717577d..., actions/upload-artifact@v2→82c141cc..., actions/download-artifact@v2→cbed621e...

4. test.yaml - missing-permissions: Added top-level `permissions: {}` plus job-level permissions (contents: read for test-action, contents: write for collect-reports which pushes to test-report branch).

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed two script-injection findings in .github/workflows/test.yaml:

1. 'Calculate freed space' step: Moved all six matrix context expressions (${{ matrix.os }}, ${{ matrix.remove-android }}, ${{ matrix.remove-dotnet }}, ${{ matrix.remove-haskell }}, ${{ matrix.remove-codeql }}, ${{ matrix.remove-docker-images }}) into a step-level `env:` block as MATRIX_OS, MATRIX_REMOVE_ANDROID, MATRIX_REMOVE_DOTNET, MATRIX_REMOVE_HASKELL, MATRIX_REMOVE_CODEQL, MATRIX_REMOVE_DOCKER_IMAGES. All shell references updated to use these env vars.

2. 'Overwrite old report' step: Replaced `${{ env.REPORT_DIR }}/${{ env.REPORT_FILE }}` with `"${REPORT_DIR}/${REPORT_FILE}"` — these variables are already available as environment variables from the workflow/job-level env blocks, so no additional env: block was needed. The ${{ }} template expressions are no longer embedded in the run: shell string.

