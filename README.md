# Prometheus

A Windows desktop mod manager for Valve's **Deadlock**.

## Download

Get **[Prometheus.ModManager.exe](https://github.com/0xSnww/Prometheus/releases/latest/download/Prometheus.ModManager.exe)** from the [latest release](https://github.com/0xSnww/Prometheus/releases/latest) and run it. There is nothing to install: it's a single exe for 64-bit Windows 10 and 11, and it updates itself.

Keep the file name `Prometheus.ModManager.exe`: Discord recognizes `prometheus.exe` as **Omega Strikers**.

## Features

- **Find and install mods**: Browse skins, sounds and more from GameBanana, or drag in your own mod files.
- **Customize Deadlock**: Switch hero skins, change your HUD and music, pick ability sounds and design a crosshair.
- **Manage your collection**: Turn mods on or off, change their priority or remove several at once.
- **Save and share setups**: Save your favorite mod combinations, switch between them and share GameBanana mod lists with a code.
- **Keep mods updated**: Update mods together, keep a version you like or restore an earlier one.
- **Sort out conflicts**: See which mods overlap, choose which takes priority and get help tracking down problems.
- **Try mods and undo changes**: Test mods temporarily and restore your setup from automatic backups.
- **Launch and play**: Start Deadlock from the app, or temporarily turn off your Prometheus mods for a session.

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
