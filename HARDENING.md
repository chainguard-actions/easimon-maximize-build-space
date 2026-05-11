# Hardening Report: easimon--maximize-build-space/v6

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **easimon--maximize-build-space/v6** was hardened automatically. 24 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Maximize build disk space' step in action.yml directly interpolates `inputs.*` expressions inside `run:` shell commands without first assigning them to environment variables. An attacker who controls these inputs can inject arbitrary shell commands. Affected inputs include: `inputs.build-mount-path`, `inputs.root-reserve-mb`, `inputs.temp-reserve-mb`, `inputs.swap-size-mb`, `inputs.overprovision-lvm`, `inputs.pv-loop-path`, `inputs.tmp-pv-loop-path`, `inputs.remove-dotnet`, `inputs.remove-android`, `inputs.remove-haskell`. Examples of dangerous patterns: `BUILD_MOUNT_PATH="${{ inputs.build-mount-path }}"`, `if [[ ${{ inputs.remove-dotnet }} == 'true' ]]`, `expr ${{ inputs.root-reserve-mb }} \* 1024`, `sudo touch "${{ inputs.pv-loop-path }}"`. All inputs should be assigned to env vars (e.g., `env: BUILD_MOUNT_PATH: ${{ inputs.build-mount-path }}`) and referenced as `$BUILD_MOUNT_PATH` in the shell script.

Locations:

- `action.yml:52`
- `action.yml:57`
- `action.yml:58`
- `action.yml:59`
- `action.yml:60`
- `action.yml:62`
- `action.yml:63`
- `action.yml:65`
- `action.yml:68`
- `action.yml:71`
- `action.yml:75`
- `action.yml:78`
- `action.yml:81`
- `action.yml:93`
- `action.yml:99`
- `action.yml:101`
- `action.yml:106`
- `action.yml:111`
- `action.yml:116`
- `action.yml:118`
- `action.yml:123`
- `action.yml:128`
- `action.yml:133`

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

**Fixes applied:** script-injection, static-inline-injection

**Notes:**

Fixed all script injection findings in action.yml by adding an env: block to the 'Maximize build disk space' step with 10 environment variables (INPUT_BUILD_MOUNT_PATH, INPUT_ROOT_RESERVE_MB, INPUT_TEMP_RESERVE_MB, INPUT_SWAP_SIZE_MB, INPUT_OVERPROVISION_LVM, INPUT_PV_LOOP_PATH, INPUT_TMP_PV_LOOP_PATH, INPUT_REMOVE_DOTNET, INPUT_REMOVE_ANDROID, INPUT_REMOVE_HASKELL) that map all ${{ inputs.* }} expressions. All references in the run: shell script were updated to use the corresponding ${INPUT_*} environment variables instead of direct ${{ }} interpolation, preventing shell injection attacks.

