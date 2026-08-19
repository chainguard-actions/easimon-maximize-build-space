<!-- markdownlint-disable -->

# Hardening Report: easimon--maximize-build-space/v9

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **easimon--maximize-build-space/v9** was hardened automatically. 32 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Maximize build disk space' step in action.yml directly interpolates ${{ inputs.* }} expressions inside run: shell commands (sub-rule a). Before the shell executes, the Actions runner substitutes these expressions verbatim into the script text, allowing a calling workflow to supply values containing shell metacharacters (`;`, `|`, `$(...)`, etc.) that the shell will then interpret. Affected inputs include: `${{ inputs.build-mount-path }}` (assigned to BUILD_MOUNT_PATH), `${{ inputs.remove-dotnet }}` / `${{ inputs.remove-android }}` / `${{ inputs.remove-haskell }}` / `${{ inputs.remove-codeql }}` / `${{ inputs.remove-docker-images }}` (used in `if [[ ${{ ... }} == 'true' ]]` conditions), `${{ inputs.root-reserve-mb }}` / `${{ inputs.temp-reserve-mb }}` (used in `expr` arithmetic), `${{ inputs.pv-loop-path }}` / `${{ inputs.tmp-pv-loop-path }}` (used in `sudo touch` and `sudo fallocate`), `${{ inputs.swap-size-mb }}` (used in `sudo lvcreate`), and `${{ inputs.build-mount-path-ownership }}` (used in `sudo chown`). All of these must be moved to env: variables and then referenced as double-quoted shell variables (e.g., `"$INPUT_VAR"`).

Locations:

- `action.yml:57`

### script-injection (severity: high)

The workflow file .github/workflows/test.yaml directly interpolates ${{ ... }} expressions inside run: shell commands (sub-rule a). Specifically: (1) 'Determine free space before' step uses `${{ github.workspace }}` directly inside a shell command string; (2) 'Determine free space after' step uses `${{ github.workspace }}` directly; (3) 'Calculate freed space and elapsed time' step uses `${{ matrix.os }}`, `${{ matrix.remove-android }}`, `${{ matrix.remove-dotnet }}`, `${{ matrix.remove-haskell }}`, `${{ matrix.remove-codeql }}`, `${{ matrix.remove-docker-images }}` directly in shell variable assignments and a heredoc; (4) 'Overwrite old report' step uses `${{ env.REPORT_DIR }}` and `${{ env.REPORT_FILE }}` directly in a shell command. These must be moved to env: variables and referenced as double-quoted shell variables.

Locations:

- `.github/workflows/test.yaml:57`
- `.github/workflows/test.yaml:75`
- `.github/workflows/test.yaml:83`
- `.github/workflows/test.yaml:130`
- `.github/workflows/test.yaml:155`

### unpinned-uses (severity: high)

The workflow file .github/workflows/test.yaml references external actions using mutable tag-based refs instead of immutable 40-character SHA digests. Unpinned references are vulnerable to supply-chain attacks if the tag is moved or the upstream repository is compromised. Failing references: `actions/checkout@v4` (appears 3 times), `actions/upload-artifact@v3` (appears 2 times), `actions/download-artifact@v3` (appears 1 time). Each must be pinned to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/test.yaml:22`
- `.github/workflows/test.yaml:62`
- `.github/workflows/test.yaml:110`
- `.github/workflows/test.yaml:118`
- `.github/workflows/test.yaml:130`
- `.github/workflows/test.yaml:143`

### missing-permissions (severity: medium)

The workflow file .github/workflows/test.yaml has no top-level `permissions:` key and none of its three jobs (test-docker-tmp, determine-free-space, collect-reports) define a `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (e.g., write access to contents). A `permissions:` block with minimal required scopes should be added at the top level or per job.

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

- `action.yml:119`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-android }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:122`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-haskell }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:125`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-codeql }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:128`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-docker-images }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:131`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.root-reserve-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:147`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:151`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:151`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:152`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.temp-reserve-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:157`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tmp-pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:161`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tmp-pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:161`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tmp-pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:162`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.swap-size-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:170`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.overprovision-lvm }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:177`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.build-mount-path-ownership }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:183`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, static-inline-injection, unpinned-uses, missing-permissions

**Notes:**

Fixed all findings:

1. action.yml script-injection: Moved all 13 ${{ inputs.* }} expressions from the run: shell block to an env: block. Shell script now uses double-quoted env vars like "${INPUT_BUILD_MOUNT_PATH}", "${INPUT_ROOT_RESERVE_MB}", etc.

2. test.yaml script-injection: Moved ${{ github.workspace }} to env: GH_WORKSPACE in two steps; moved ${{ matrix.* }} expressions to env: block in 'Calculate freed space and elapsed time' step; replaced ${{ env.REPORT_DIR }}/${{ env.REPORT_FILE }} in 'Overwrite old report' with shell variable references.

3. test.yaml unpinned-uses: Pinned actions/checkout@v4 to SHA 11d5960a326750d5838078e36cf38b85af677262, actions/upload-artifact@v3 to SHA ff15f0306b3f739f7b6fd43fb5d26cd321bd4de5, actions/download-artifact@v3 to SHA 9bc31d5ccc31df68ecc42ccf4149144866c47d8a.

4. test.yaml missing-permissions: Added top-level permissions: contents: write, with per-job overrides (contents: read for test-docker-tmp and determine-free-space; contents: write for collect-reports which needs to push to the test-report branch).

