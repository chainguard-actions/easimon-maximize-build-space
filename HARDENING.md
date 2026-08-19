<!-- markdownlint-disable -->

# Hardening Report: easimon--maximize-build-space/v10

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **easimon--maximize-build-space/v10** was hardened automatically. 29 finding(s) were identified and resolved across 2 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Maximize build disk space' run: block directly interpolates ${{ inputs.* }} expressions inside shell commands (rule a). GitHub Actions substitutes these values into the shell script string before the shell parses it, allowing an attacker who controls the calling workflow's inputs to inject arbitrary shell metacharacters and commands. Affected lines include:
- Line 82: BUILD_MOUNT_PATH="${{ inputs.build-mount-path }}"
- Line 89: echo "  Root reserve:      ${{ inputs.root-reserve-mb }} MiB"
- Line 90: echo "  Temp reserve:      ${{ inputs.temp-reserve-mb }} MiB"
- Line 91: echo "  Swap space:        ${{ inputs.swap-size-mb }} MiB"
- Line 92: echo "  Overprovision LVM: ${{ inputs.overprovision-lvm }}"
- Line 94: echo "  Root PV loop path: ${{ inputs.pv-loop-path }}"
- Line 95: echo "  Temp PV loop path: ${{ inputs.tmp-pv-loop-path }}"
- Lines 97,100,103,106,109: if [[ ${{ inputs.remove-* }} == 'true' ]]; then
- Lines 122,125,128,131,134: if [[ ${{ inputs.remove-* }} == 'true' ]]; then (second set)
- Line 150: ROOT_RESERVE_KB=$(expr ${{ inputs.root-reserve-mb }} \* 1024)
- Lines 154,155: sudo touch/losetup with "${{ inputs.pv-loop-path }}"
- Line 160: TMP_RESERVE_KB=$(expr ${{ inputs.temp-reserve-mb }} \* 1024)
- Lines 164,165: sudo touch/losetup with "${{ inputs.tmp-pv-loop-path }}"
- Line 173: sudo lvcreate -L "${{ inputs.swap-size-mb }}M"
- Line 180: if [[ ${{ inputs.overprovision-lvm }} == 'true' ]]
- Line 186: sudo chown -R "${{ inputs.build-mount-path-ownership }}"
Fix: move all inputs into env: variables and reference them as quoted shell variables (e.g., "$INPUT_VAR") in the run: block.

Locations:

- `action.yml:82`
- `action.yml:89`
- `action.yml:90`
- `action.yml:91`
- `action.yml:92`
- `action.yml:94`
- `action.yml:95`
- `action.yml:97`
- `action.yml:100`
- `action.yml:103`
- `action.yml:106`
- `action.yml:109`
- `action.yml:122`
- `action.yml:125`
- `action.yml:128`
- `action.yml:131`
- `action.yml:134`
- `action.yml:150`
- `action.yml:154`
- `action.yml:155`
- `action.yml:160`
- `action.yml:164`
- `action.yml:165`
- `action.yml:173`
- `action.yml:180`
- `action.yml:186`

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

- `action.yml:122`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-android }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:125`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-haskell }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:128`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-codeql }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:131`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.remove-docker-images }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:134`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.root-reserve-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:150`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:154`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:154`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:155`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.temp-reserve-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:160`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tmp-pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:164`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tmp-pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:164`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tmp-pv-loop-path }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:165`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.swap-size-mb }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:173`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.overprovision-lvm }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:180`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.build-mount-path-ownership }}" appears directly in run: block of step "Maximize build disk space"; move to env: map

Locations:

- `action.yml:186`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, static-inline-injection

**Notes:**

Moved all 13 ${{ inputs.* }} expressions out of the run: block in the 'Maximize build disk space' step and into a new env: block. Added env vars: INPUT_BUILD_MOUNT_PATH, INPUT_BUILD_MOUNT_PATH_OWNERSHIP, INPUT_ROOT_RESERVE_MB, INPUT_TEMP_RESERVE_MB, INPUT_SWAP_SIZE_MB, INPUT_OVERPROVISION_LVM, INPUT_PV_LOOP_PATH, INPUT_TMP_PV_LOOP_PATH, INPUT_REMOVE_DOTNET, INPUT_REMOVE_ANDROID, INPUT_REMOVE_HASKELL, INPUT_REMOVE_CODEQL, INPUT_REMOVE_DOCKER_IMAGES. All references in the shell script now use quoted ${VAR} syntax, preventing shell injection from attacker-controlled input values.

### Iteration 2

**Fixes applied:** unpinned-uses, missing-permissions, script-injection, github-env-injection

**Notes:**

Rewrote .github/workflows/test.yaml with all four security fixes:

1. unpinned-uses: Pinned all 7 action references to full SHA hashes: actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262, actions/upload-artifact@v3 → @ff15f0306b3f739f7b6fd43fb5d26cd321bd4de5, actions/download-artifact@v3 → @9bc31d5ccc31df68ecc42ccf4149144866c47d8a.

2. missing-permissions: Added top-level `permissions: contents: write` and per-job permissions blocks (contents: read for jobs that don't push, contents: write for collect-reports which does git push).

3. script-injection: Moved all ${{ }} expressions out of run: shell strings into env: blocks. Matrix values (os, remove-android, etc.) moved to MATRIX_* env vars; step outputs moved to WORKSPACE_PARENT; env context values moved to REPORT_DIR_ENV/REPORT_FILE_ENV. github.workspace replaced with built-in ${GITHUB_WORKSPACE} env var.

4. github-env-injection: The two 'Determine free space' steps now sanitize values before writing to GITHUB_ENV using `printf '%s' ... | tr -d '\n\r'`, preventing newline injection attacks.

