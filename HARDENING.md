# Hardening Report: easimon--maximize-build-space/v7

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **easimon--maximize-build-space/v7** was hardened automatically. 28 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Maximize build disk space' run: step in action.yml directly interpolates ${{ inputs.* }} expressions into the shell script without first assigning them to environment variables. All 13 distinct inputs (build-mount-path, root-reserve-mb, temp-reserve-mb, swap-size-mb, overprovision-lvm, pv-loop-path, tmp-pv-loop-path, remove-dotnet, remove-android, remove-haskell, remove-codeql, remove-docker-images, swap-size-mb) are interpolated directly into shell commands. An attacker who controls these inputs (e.g. via workflow_dispatch or a calling workflow) can inject arbitrary shell commands. Examples include: BUILD_MOUNT_PATH="${{ inputs.build-mount-path }}", if [[ ${{ inputs.remove-dotnet }} == 'true' ]], ROOT_RESERVE_KB=$(expr ${{ inputs.root-reserve-mb }} \* 1024), and sudo touch "${{ inputs.pv-loop-path }}". The fix is to assign each input to an env: variable and reference $ENV_VAR in the run: block instead.

Locations:

- `action.yml:74`
- `action.yml:80`
- `action.yml:81`
- `action.yml:82`
- `action.yml:83`
- `action.yml:85`
- `action.yml:86`
- `action.yml:88`
- `action.yml:91`
- `action.yml:95`
- `action.yml:99`
- `action.yml:103`
- `action.yml:107`

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

**Fixes applied:** script-injection, static-inline-injection

**Notes:**

Fixed all 28 script injection findings in action.yml by adding an env: block to the 'Maximize build disk space' step with 12 environment variables (INPUT_BUILD_MOUNT_PATH, INPUT_ROOT_RESERVE_MB, INPUT_TEMP_RESERVE_MB, INPUT_SWAP_SIZE_MB, INPUT_OVERPROVISION_LVM, INPUT_PV_LOOP_PATH, INPUT_TMP_PV_LOOP_PATH, INPUT_REMOVE_DOTNET, INPUT_REMOVE_ANDROID, INPUT_REMOVE_HASKELL, INPUT_REMOVE_CODEQL, INPUT_REMOVE_DOCKER_IMAGES) mapping each ${{ inputs.* }} expression. All occurrences of ${{ inputs.* }} in the run: block were replaced with the corresponding $INPUT_* environment variable references. The ${{ inputs.* }} expressions now only appear in the safe env: map context.

