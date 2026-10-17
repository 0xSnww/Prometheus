# Prometheus

A Windows desktop mod manager for Valve's **Deadlock**.

## Download

Get **[Prometheus.ModManager.exe](https://github.com/0xSnww/Prometheus/releases/latest/download/Prometheus.ModManager.exe)** from the [latest release](https://github.com/0xSnww/Prometheus/releases/latest) and run it. There is nothing to install: it's a single exe for 64-bit Windows 10 and 11, and it updates itself.

Keep the file name `Prometheus.ModManager.exe`: Discord recognizes `prometheus.exe` as **Omega Strikers**.

## Features

- **Setup**: finds the Deadlock install through your Steam libraries and checks it by looking for `game/citadel/gameinfo.gi`.
  - **gameinfo.gi patch**: adds a single `Game citadel/addons` search path. Prometheus backs up the original file first.
  - Shows the patch status, can patch and restore, and re-applies the patch after a game update reverts it (optional).
- **Browse GameBanana Mods and Sounds**:
  - Separate catalogs, categories, favorites and update identities for mods and sounds. Sound detail pages play author-provided audio previews when available.
  - Paged card grid with search, category filter and sort. Skins can be narrowed down to one hero.
  - Favorites: mark mods with the heart and find them under ★ Favorites.
  - Mods marked obsolete are hidden by default, and you can hide whole categories (right-click a category).
  - Detail view with a gallery, description, the mod's requirements, the author's recent updates (changelog) and all files, including archived ones.
  - Cached thumbnails.
  - NSFW mods are hidden by default; you can turn this off in Settings.
- **Download queue**:
  - Several downloads run at once (Settings → Mod management). Installing still happens one mod at a time.
  - Pause, resume, retry and cancel. An interrupted download keeps its partial file and resumes where it stopped.
- **Install pipeline**:
  - Downloads with progress and cancel, then extracts into a staging folder.
  - Finds the VPKs in the archive, including multi-part `pakNN_dir.vpk` + `pakNN_000.vpk` sets, nested archives and variant folders. When there is more than one variant, you choose which to install.
  - Each mod gets free `pakNN_dir.vpk` slots and is recorded in a manifest.
  - You can import local `.zip/.7z/.rar/.vpk` files with the **Import** button or by dragging them onto the window.
- **Installed mods**:
  - Search names, authors, heroes, tags and personal notes; filter by enabled state, updates, conflicts, local imports or pinned versions. Select visible results for bulk enable, disable, update, removal or merging.
  - **Preferences** in each mod’s menu stores tags, notes, update policy, cosmetic category and remembered conflict rules.
  - Enable or disable mods. Disabled files move to `citadel/prometheus_store`.
  - Uninstall mods.
  - Reorder by dragging or with the up/down buttons. Mods higher in the list get lower pak numbers and win conflicts. Renumbering is two-phase and transactional, with rollback on failure.
  - Pak files that Prometheus did not install are detected and left alone unless you choose **Manage**. Paks installed by Deadlock Mod Manager are recognized from its `.dmm.json`, and **Manage and link** connects them to their GameBanana page.
  - Any local or adopted mod can be linked to its GameBanana page later, so it gets update checks.
  - **Disable all** turns every mod off and remembers which were on, so one click turns them back on.
- **Conflict detection**:
  - Persistent “override these mods” preferences preserve chosen winners when reordering or switching profiles. Cyclic rules are rejected before files change.
  - Prometheus reads each VPK's file list (the directory tree, not the data) and works out which enabled mods change the same files.
  - Each mod shows whether it overrides files in other mods, loses files to them, or has no effect at all because mods above it replace every file it changes.
  - The details view lists the colliding files and offers **Move above it** / **Move below it**. Files that are byte-identical in both mods (same CRC and size) aren't counted as conflicts.
- **Heroes**:
  - Mods are tagged with the heroes they change, worked out from their files, so local imports are tagged too.
  - The Heroes page groups skins by hero. Picking one enables it and turns off that hero's other skins; voice and effect mods are listed separately.
  - Skin mods are grouped and labeled only by the heroes they reskin, so bundled sounds, effects or icons do not add unrelated heroes. Mod details still show every affected hero and file.
  - Enabling a second skin for a hero asks whether to swap or keep both (can be turned off in Settings).
- **Updates**:
  - Pin a version, skip an update, or disable automatic updates for an individual mod. Rolling back pins the restored version.
  - Review the added, removed and changed VPK files before applying an update. Automatic updates pause for new conflicts, unreadable VPKs or a required variant choice.
  - Checks GameBanana for newer files and shows badges.
  - Update one mod or update all.
  - Optional checks on startup and auto-update on an interval.
  - An update keeps the mod's load-order slot and enabled state.
  - The replaced version is kept, so **Roll back** in the mod's … menu restores it (and a rollback can itself be undone). This can be turned off in Settings.
- **Game updates**:
  - Prometheus records Deadlock's Steam build when each mod is installed. After a game update, a banner says how many enabled mods were made before it, with shortcuts to check for mod updates or find the broken mod.
  - Mark a mod tested working or broken on your current Steam build. These are personal notes, not community compatibility claims.
  - **Find broken mods** checks a clean managed-mod baseline, reproduces the problem, narrows down interacting combinations, then verifies isolation and removal. The test history survives app restarts. Launch count depends on the interaction; a combination does not prove one mod is defective. Other mod changes are blocked until diagnosis finishes or is restored.
- **Complete profiles**: save, switch, delete, and export/import as JSON. New local profiles retain exact VPK bytes, including local imports, selected variants, order, enabled state, update preferences, conflict rules and managed commands. Review differences before applying. Legacy profiles remain supported.
  - **Share codes**: copy a profile as a `PROM1-…` code or a `prometheus:profile/…` link. No server is involved; the code holds GameBanana catalog and file ids, selected variants, update preferences, conflict rules and managed commands. Importing shows what's installed, downloads the missing mods and can switch to the profile when done. Local mod files must be supplied separately. Shared profiles restore exact GameBanana file versions while those files remain available; local recovery files stay on your computer.
- **Crosshair designer**: live approximate preview, color and geometry controls, dot/outline options, saved presets and JSON import/export. Applying writes the managed autoexec section and enables it for launches through Prometheus; profiles retain the result.
- **Global cosmetics**: HUD, announcer/SFX, music, soul containers and icon packs in one view, with per-mod category corrections.
- **Recovery**: automatic snapshots before installs, updates, profile switches and removals, plus manual snapshots. Stores all current managed VPK parts and managed commands, verifies checksums before restoring, and deduplicates identical data. The default budget is 5 GB; oldest unprotected points are pruned. The newest point and points retained by profiles or temporary sessions can exceed that budget. Unmanaged paks and the user's own autoexec section stay untouched.
- **Temporary trials**: choose **Try temporarily** during install review, test in game, then keep changes or restore your prior setup in Recovery. The session survives restarting Prometheus.
- **Vanilla session**: **Launch vanilla once** disables managed mods and removes managed commands, then restores them after the game exits. An interrupted session is recovered when Prometheus next runs. Unmanaged addons must be resolved first; unrelated Steam launch options and personal config are not changed.
- **Install impact review**: shows affected heroes, content groups, conflicting mods and priority before installation, plus file differences for updates. Unreadable content and unmanaged addons are identified as unknown impact.
- **VPK merging**: select adjacent enabled mods and use **Merge selected**. Prometheus preserves first-file priority and CRC-verifies streamed payloads; original mods stay disabled for **Unmerge**. Output is a self-contained VPK, limited to 4 GB. Missing source mods must be recovered before unmerging.
- **Per-ability sound selections**: use a mod’s **Choose ability sounds** menu to filter compiled sound resources by folder and filename. Build independently toggleable selections from different packs, optionally disabling each full source pack. Original game paths are retained; this selects existing compiled sounds, rather than synthesizing audio or changing pitch/volume.
- **3D model previews**: use **Preview 3D model** on an installed mod containing compiled models. Orbit and zoom a static model with base-color textures. First use downloads a checksum-verified 50 MB [Source 2 Viewer 20.0 CLI](https://github.com/ValveResourceFormat/ValveResourceFormat/releases/tag/20.0) into app data. The game installation supplies missing dependencies. Texture-only packs, animations, particles and game shader lighting are not rendered by this preview.
- **Console commands**: an editor for `game/citadel/cfg/autoexec.cfg` with a small library of common commands. Prometheus only touches its own marked section of the file. The Launch button can add `+exec autoexec`, which Deadlock needs to run the file.
- **Launch Deadlock** through Steam. Prometheus warns you if you change mods while `deadlock.exe` is running.
- **Self-update** through NetSparkle, from signed GitHub releases (see below).

Game-file operations stay inside `game/citadel/addons`, `game/citadel/prometheus_store` (disabled mods and kept previous versions), `gameinfo.gi` and, when applying commands, crosshairs, profiles or recovery, `game/citadel/cfg/autoexec.cfg`. Prometheus never moves or deletes paks it doesn't own unless you ask it to.

Prometheus has no account and no telemetry. The only network requests go to GameBanana (browsing, downloads, update checks) and to GitHub (Prometheus updates and the optional 3D preview tool download). Author audio previews use GameBanana’s media servers.

App data (settings, manifest backups, profiles, recovery blobs, preview tools, caches and logs) is stored in `%APPDATA%\Prometheus`. To use a different folder, for example a portable or test instance, set `PROMETHEUS_DATA_DIR`.

## 1-click install

In **Settings → 1-click install**, turn on *Open prometheus: links with Prometheus*.

- This registers the `prometheus:` URL scheme for the current user only, under `HKCU\Software\Classes\prometheus`. No admin rights are needed.
- Turning the option off removes the registration. Prometheus never registers the scheme unless you turn the option on.

The link format follows the one GameBanana uses for Deadlock mod managers:

```
prometheus:https://gamebanana.com/mmdl/<fileId>,Mod,<modId>
```

Use `Sound` instead of `Mod` for GameBanana Sounds.

`deadlock-mod-manager:` payloads are also accepted when passed on the command line.

If Prometheus is already running, a link opens in the existing window rather than starting a second instance.

Note: GameBanana only shows 1-click buttons for tools registered with it. `prometheus:` links won't appear on the site unless Prometheus is registered there as a mod manager.

## Updates

Prometheus checks this repository for a new version on startup (turn this off in **Settings → Prometheus updates**). Every release is signed, and Prometheus refuses an update whose signature does not match. **What's new** on the update banner shows the release notes.
