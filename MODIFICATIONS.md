# Fork modifications — lawnchair-icon-badge-uncapped

This repository is a fork of [LawnchairLauncher/Lawnchair](https://github.com/LawnchairLauncher/Lawnchair)
(branch `15-dev`, base commit `505dbc4`), licensed under Apache License 2.0.
All Lawnchair and Android Open Source Project copyright notices and license terms are
retained unmodified. Per Section 4(b) of the Apache License 2.0, this file states the
changes made by this fork.

## Changes (branch `badge-uncapped`)

Full reviewable diff:
[lawnchair `15-dev`...`badge-uncapped`](https://github.com/LawnchairLauncher/lawnchair/compare/15-dev...brendangreenley:lawnchair-icon-badge-uncapped:badge-uncapped)
·
[submodule `6a11ef7`...`badge-uncapped`](https://github.com/LawnchairLauncher/platform_frameworks_libs_systemui/compare/6a11ef7...brendangreenley:platform_frameworks_libs_systemui-badge-uncapped:badge-uncapped)

1. **Notification counter cap raised from 999 to 20000**
   - `src/com/android/launcher3/dot/DotInfo.java` — `MAX_COUNT` raised to `20000`
     (upstream value: `999`). Controls the maximum count a notification dot represents.

2. **Dot renders the full number and morphs into a pill**
   - `platform_frameworks_libs_systemui/iconloaderlib/src/com/android/launcher3/icons/DotRenderer.java`
     (in the `platform_frameworks_libs_systemui` submodule; see below):
     - `MAX_COUNT` raised from `99` to `20000` so the paint layer no longer clamps
       counts to two digits.
     - When the counter text is wider than the round dot, the dot is drawn as a
       horizontal stadium-shaped pill (including its shadow layer) sized to fit the
       digits at full counter text size, instead of overflowing or clipping.
       Padding per side: `0.75 x dot radius`.

3. **Third-party shortcut corner badge never drawn**
   - `src/com/android/launcher3/icons/IconCache.java` — `getShortcutIcon()` no longer
     attaches the source-app badge (`withBadgeInfo(getShortcutInfoBadge(si))`) to
     shortcut icons.
   - `src/com/android/launcher3/Utilities.java` — the workspace shortcut icon rebuild
     path no longer fetches/attaches the shortcut badge either.

## Submodule

The `DotRenderer.java` change lives in the `platform_frameworks_libs_systemui`
submodule (upstream:
[LawnchairLauncher/platform_frameworks_libs_systemui](https://github.com/LawnchairLauncher/platform_frameworks_libs_systemui),
also Apache License 2.0). This fork's `.gitmodules` points the submodule at
[brendangreenley/platform_frameworks_libs_systemui-badge-uncapped](https://github.com/brendangreenley/platform_frameworks_libs_systemui-badge-uncapped),
branch `badge-uncapped`, whose only change relative to upstream commit `6a11ef7` is
the `DotRenderer.java` change described above.

## Prebuilt artifact

A debug-signed APK built from this branch is attached to the GitHub release tagged
`badge-uncapped`. It is signed with the standard Android debug key and is provided for
sideloading/testing only.
