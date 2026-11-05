<!-- markdownlint-disable -->

# Hardening Report: easimon--maximize-build-space/v10

> This file was generated automatically by the hardening agent.

**Policy SHA:** `374911c4be584df24e6da57af2d990570ef0f859`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **easimon--maximize-build-space/v10** was hardened automatically. 30 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Sub-rule (a): the 'Maximize build disk space' composite step puts GitHub expressions directly into its run: script, so they are substituted before bash parses the script. Examples: `BUILD_MOUNT_PATH="${{ inputs.build-mount-path }}"`, `if [[ ${{ inputs.remove-dotnet }} == 'true' ]]; then` (the same unquoted pattern is used for remove-android, remove-haskell, remove-codeql, remove-docker-images and overprovision-lvm), `ROOT_RESERVE_KB=$(expr ${{ inputs.root-reserve-mb }} \* 1024)`, `TMP_RESERVE_KB=$(expr ${{ inputs.temp-reserve-mb }} \* 1024)`, `sudo touch "${{ inputs.pv-loop-path }}"`, `sudo touch "${{ inputs.tmp-pv-loop-path }}"`, `sudo lvcreate -L "${{ inputs.swap-size-mb }}M"` and `sudo chown -R "${{ inputs.build-mount-path-ownership }}"`. A crafted input value can run arbitrary commands, with sudo available. Fix: pass each input through the step's env: block and use it in the script as a double-quoted variable, e.g. "$INPUT_REMOVE_DOTNET".

Locations:

- `action.yml:80`

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

### prior-fix (severity: high)

Carried forward from this version's previous harden, which fixed it; fix it again unless the code no longer has the problem. The previous harden changed action.yml without recording a finding for it, and this analysis reported nothing there. Re-apply its security changes unless the code no longer needs them. The previous patch:
```diff
diff --git a/action.yml b/action.yml
index 04f3923..431b914 100644
--- a/action.yml
+++ b/action.yml
@@ -61,6 +61,23 @@ inputs:
 runs:
   using: "composite"
   steps:
     - name: Disk space report before modification
       shell: bash
       run: |
@@ -73,124 +90,136 @@ runs:
         echo "Available storage:"
         sudo df -h
         echo
-
     - name: Maximize build disk space
       shell: bash
+      env:
+        INPUT_BUILD_MOUNT_PATH: ${{ inputs.build-mount-path }}
+        INPUT_BUILD_MOUNT_PATH_OWNERSHIP: ${{ inputs.build-mount-path-ownership }}
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
       run: |
-          set -euo pipefail
-
-          BUILD_MOUNT_PATH="${{ inputs.build-mount-path }}"
-          if [[ -z "${BUILD_MOUNT_PATH}" ]]; then
-            BUILD_MOUNT_PATH="${GITHUB_WORKSPACE}"
-          fi
-
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
-          # store owner of $GITHUB_WORKSPACE in case the action deletes it
-          WORKSPACE_OWNER="$(stat -c '%U:%G' "${GITHUB_WORKSPACE}")"
-
-          # ensure mount path exists before the action
-          sudo mkdir -p "${BUILD_MOUNT_PATH}"
-          sudo find "${BUILD_MOUNT_PATH}" -maxdepth 0 ! -empty -exec echo 'WARNING: directory [{}] is not empty, data loss might occur. Content:' \; -exec ls -al "{}" \;
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
+        set -euo pipefail
 
-          VG_NAME=buildvg
+        BUILD_MOUNT_PATH="${INPUT_BUILD_MOUNT_PATH}"
+        if [[ -z "${BUILD_MOUNT_PATH}" ]]; then
+          BUILD_MOUNT_PATH="${GITHUB_WORKSPACE}"
+        fi
 
-          # github runners have an active swap file in /mnt/swapfile
-          # we want to reuse the temp disk, so first unmount swap an
... (truncated)
```

Locations:

- `action.yml`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, static-inline-injection, prior-fix

**Notes:**

In action.yml, the 13 inputs that the 'Maximize build disk space' step used now come in through the step's env: block as INPUT_* variables. The script refers to each one as a double-quoted shell variable: the [[ ]] true/false checks, the expr arithmetic, the paths passed to touch/fallocate/losetup, the lvcreate size and the chown ownership. This applies the same change as the previous harden (prior-fix). The script logic is otherwise unchanged. Nothing was run or tested after the edit.

