<!-- markdownlint-disable -->

# Hardening Report: easimon--maximize-build-space/v8

> This file was generated automatically by the hardening agent.

**Policy SHA:** `374911c4be584df24e6da57af2d990570ef0f859`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **easimon--maximize-build-space/v8** was hardened automatically. 30 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Sub-rule (a): the composite step 'Maximize build disk space' puts ${{ inputs.* }} expressions straight into its bash run: script. Examples: `BUILD_MOUNT_PATH="${{ inputs.build-mount-path }}"`, `echo "  Root reserve:      ${{ inputs.root-reserve-mb }} MiB"`, `if [[ ${{ inputs.remove-dotnet }} == 'true' ]]; then` (the same unquoted form is used for remove-android, remove-haskell, remove-codeql, remove-docker-images and overprovision-lvm), `ROOT_RESERVE_KB=$(expr ${{ inputs.root-reserve-mb }} \* 1024)`, `TMP_RESERVE_KB=$(expr ${{ inputs.temp-reserve-mb }} \* 1024)`, `sudo touch "${{ inputs.pv-loop-path }}"`, `sudo losetup --find --show "${{ inputs.tmp-pv-loop-path }}"`, `sudo lvcreate -L "${{ inputs.swap-size-mb }}M"` and `sudo chown -R "${{ inputs.build-mount-path-ownership }}"`. Whoever calls the action controls these values, and many of the commands run under sudo, so a crafted value could run arbitrary commands. Fix: pass every input through env: and use it as a double-quoted shell variable, e.g. "$INPUT_ROOT_RESERVE_MB".

Locations:

- `action.yml:82`

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

### prior-fix (severity: high)

Carried forward from this version's previous harden, which fixed it; fix it again unless the code no longer has the problem. The previous harden changed action.yml without recording a finding for it, and this analysis reported nothing there. Re-apply its security changes unless the code no longer needs them. The previous patch:
```diff
diff --git a/action.yml b/action.yml
index e3d9ba1..1d6ef25 100644
--- a/action.yml
+++ b/action.yml
@@ -61,6 +61,23 @@ inputs:
 runs:
   using: "composite"
   steps:
     - name: Disk space report before modification
       shell: bash
       run: |
@@ -73,114 +90,126 @@ runs:
         echo "Available storage:"
         df -h
         echo
-
     - name: Maximize build disk space
       shell: bash
+      env:
+        INPUT_BUILD_MOUNT_PATH: ${{ inputs.build-mount-path }}
+        INPUT_ROOT_RESERVE_MB: ${{ inputs.root-reserve-mb }}
+        INPUT_TEMP_RESERVE_MB: ${{ inputs.temp-reserve-mb }}
+        INPUT_SWAP_SIZE_MB: ${{ inputs.swap-size-mb }}
+        INPUT_OVERPROVISION_LVM: ${{ inputs.overprovision-lvm }}
+        INPUT_PV_LOOP_PATH: ${{ inputs.pv-loop-path }}
+        INPUT_TMP_PV_LOOP_PATH: ${{ inputs.tmp-pv-loop-path }}
+        INPUT_REMOVE_DOTNET: ${{ inputs.remove-dotnet }}
+        INPUT_REMOVE_ANDROID: ${{ inputs.remove-android }}
+        INPUT_REMOVE_HASKELL: ${{ inputs.remove-haskell }}
+        INPUT_REMOVE_CODEQL: ${{ inputs.remove-codeql }}
+        INPUT_REMOVE_DOCKER_IMAGES: ${{ inputs.remove-docker-images }}
+        INPUT_BUILD_MOUNT_PATH_OWNERSHIP: ${{ inputs.build-mount-path-ownership }}
       run: |
-          set -euo pipefail
+        set -euo pipefail
 
-          BUILD_MOUNT_PATH="${{ inputs.build-mount-path }}"
-          if [[ -z "${BUILD_MOUNT_PATH}" ]]; then
-            BUILD_MOUNT_PATH="${GITHUB_WORKSPACE}"
-          fi
+        BUILD_MOUNT_PATH="${INPUT_BUILD_MOUNT_PATH}"
+        if [[ -z "${BUILD_MOUNT_PATH}" ]]; then
+          BUILD_MOUNT_PATH="${GITHUB_WORKSPACE}"
+        fi
 
-          echo "Arguments:"
-          echo
-          echo "  Root reserve:      ${{ inputs.root-reserve-mb }} MiB"
-          echo "  Temp reserve:      ${{ inputs.temp-reserve-mb }} MiB"
-          echo "  Swap space:        ${{ inputs.swap-size-mb }} MiB"
-          echo "  Overprovision LVM: ${{ inputs.overprovision-lvm }}"
-          echo "  Mount path:        ${BUILD_MOUNT_PATH}"
-          echo "  Root PV loop path: ${{ inputs.pv-loop-path }}"
-          echo "  Temp PV loop path: ${{ inputs.tmp-pv-loop-path }}"
-          echo -n "  Removing:     "
-          if [[ ${{ inputs.remove-dotnet }} == 'true' ]]; then
-            echo -n "dotnet "
-          fi
-          if [[ ${{ inputs.remove-android }} == 'true' ]]; then
-            echo -n "android "
-          fi
-          if [[ ${{ inputs.remove-haskell }} == 'true' ]]; then
-            echo -n "haskell "
-          fi
-          if [[ ${{ inputs.remove-codeql }} == 'true' ]]; then
-            echo -n "codeql "
-          fi
-          if [[ ${{ inputs.remove-docker-images }} == 'true' ]]; then
-            echo -n "docker "
-          fi
-          echo
-
-          echo "Removing unwanted software... "
-          if [[ ${{ inputs.remove-dotnet }} == 'true' ]]; then
-            sudo rm -rf /usr/share/dotnet
-          fi
-          if [[ ${{ inputs.remove-android }} == 'true' ]]; then
-            sudo rm -rf /usr/local/lib/android
-          fi
-          if [[ ${{ inputs.remove-haskell }} == 'true' ]]; then
-            sudo rm -rf /opt/ghc
-          fi
-          if [[ ${{ inputs.remove-codeql }} == 'true' ]]; then
-            sudo rm -rf /opt/hostedtoolcache/CodeQL
-          fi
-          if [[ ${{ inputs.remove-docker-images }} == 'true' ]]; then
-            sudo docker image prune --all --force
-          fi
-          echo "... done"
+        echo "Arguments:"
+        echo
+        echo "  Root reserve:      ${INPUT_ROOT_RESERVE_MB} MiB"
+        echo "  Temp reserve:      ${INPUT_TEMP_RESERVE_MB} MiB"
+        echo "  Swap space:        ${INPUT_SWAP_SIZE_MB} MiB"
+        echo "  Overprovision LVM: ${INPUT_OVERPROVISION_LVM}"
+        echo "  Mount path:        ${BUILD_MOUNT_PATH}"
+        echo "  Root PV loop path: ${INPUT_PV_LOOP_PATH}"
+        echo "  Temp PV loop path: ${INPUT_TMP_PV_LOOP_PATH}"
+        echo -n "  Removing:     "
+        if [[ "${INPUT_REMOVE_DOTNET}" == 'true' ]]; then
+          echo -n "dotne
... (truncated)
```

Locations:

- `action.yml`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, static-inline-injection, prior-fix

**Notes:**

The 'Maximize build disk space' step in action.yml now passes all 13 inputs through env: as INPUT_* variables, and the bash script uses them as double-quoted variables instead of inline ${{ }} expressions. This includes the sudo commands (touch, fallocate, losetup, lvcreate, chown), the expr size calculations and the boolean checks. This re-applies the previous harden's patch. The script's logic is otherwise unchanged. Nothing was run or tested after the edit.

