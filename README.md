# FlatLink Mod Submissions

Community mod submissions for [FlatLink](https://github.com/TylerBits/Flatlink) — the PCVR Mod Hub desktop app.

## What is this?

This repository accepts pull requests from the community to add new PCVR mods to the FlatLink discovery catalogue. Approved submissions appear in the app automatically.

## How to submit a mod

### Requirements

- The mod must be a VR mod for a non-VR PC game
- The mod must be publicly available (GitHub, Nexus Mods, Thunderstore, itch.io, etc.)
- The installer must be non-destructive (no permanent game file modification without backup/restore)

### Steps

1. **Fork** this repository
2. **Copy** `_template/game.json` into a new file at `Core/<YourModId>/game.json`
3. **Fill in** all required fields (see field reference below)
4. **Open a pull request** with title: `Add: <Game Name> VR Mod`

A maintainer will review your submission and merge it if it meets the guidelines.

---

## Field Reference

| Field | Required | Description |
|---|---|---|
| `id` | Yes | Unique camelCase identifier, e.g. `LethalCompanyVR` |
| `name` | Yes | The base game's full display name |
| `modName` | Yes | The VR mod's name and version |
| `modAuthor` | Yes | The mod creator's name |
| `modVersion` | Yes | Semver string, e.g. `1.2.3` |
| `steamAppId` | Yes (if on Steam) | The game's Steam App ID as a number |
| `steamFolder` | Yes | Folder name inside `steamapps/common/` |
| `platform` | Yes | `steam`, `epic`, `gog`, `gamepass`, or `other` |
| `genres` | Yes | Array of genre strings |
| `tags` | Yes | Array of tags, e.g. `["6DOF", "Motion Controls"]` |
| `quality` | Yes | `excellent`, `good`, or `playable` |
| `description` | Yes | One-line description shown in the app |
| `infoUrl` | Yes | Link to the mod's page or GitHub repo |
| `modFile` | Yes | Relative path to the mod's main file (used to detect if installed) |
| `installSteps` | Yes | Typed array of install steps (see below) |

### Install Step Types

```jsonc
// Detect the game folder
{ "type": "detect", "steamFolder": "Game Folder Name", "fallbackPaths": [] }

// Download a file
{ "type": "download", "url": "https://...", "filename": "mod.zip", "label": "Mod v1.2" }

// Extract downloaded zip into game folder
{ "type": "extract" }

// Copy a specific file from the extracted zip
{ "type": "copyFile", "src": "mod/file.dll", "dest": "game/file.dll" }

// Verify key files exist after install
{ "type": "verify", "paths": ["BepInEx/plugins/MyMod.dll"] }

// Create a desktop shortcut
{ "type": "shortcut", "name": "My Game VR", "target": "MyGame.exe" }

// Show the user a message (optional: wait for dismiss)
{ "type": "message", "text": "Installation complete!", "requireDismiss": false }
```

---

## License

Submitted mod metadata is released under [CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/). Mod files and installers remain under their respective original licenses.

Copyright (c) Tyler Dickerson
