# Mac Dev Cache Cleaner Skill

A Codex/Cursor helper skill to find and clean macOS development caches safely.

## What It Does

- Scans iOS/Android/Web cache locations (Gradle, Android Studio, CocoaPods, Xcode, npm/yarn/pnpm, Homebrew).
- Can scan common home dot-directories (`~/.android`, `~/.cursor`, `~/.codex`, etc.) with risk labels.
- Detects possible orphan app data (app removed but data still exists).
- Uses dry-run first and requires strict confirmation tokens for risky cleanup.

## Install (Codex)

Install from GitHub with skill installer:

```bash
$skill-installer install https://github.com/Ppang0405/mac-cleaner-skills/tree/main
```

Then restart Codex.

## Install (Cursor)

Cursor does not install Codex skills directly. Use this repo as a project tool and run:

```bash
/usr/bin/python3 scripts/dev_cache_manager.py scan --include-home-dotdirs --include-orphans --min-size-mb 256
```

You can also add a Cursor rule/AGENTS.md instruction to call this script for cleanup tasks.

## Quick Start

```bash
# Scan only (safe)
/usr/bin/python3 scripts/dev_cache_manager.py scan --min-size-mb 256

# Broader scan
/usr/bin/python3 scripts/dev_cache_manager.py scan --include-home-dotdirs --include-orphans --min-size-mb 256

# Dry-run cleanup
/usr/bin/python3 scripts/dev_cache_manager.py clean --key gradle-caches --key npm-cache
```

## Safety

- `clean` requires `--apply --yes` for real deletion.
- High-risk/non-safe targets also require:
  - `--confirm-risk DELETE_HIGH_RISK`
- Orphan cleanup requires:
  - `--confirm-orphans DELETE_ORPHAN_APP_DATA`

## About `SKILL.md`

`SKILL.md` is the runtime instruction file used by Codex after skill activation.
`README.md` is for humans (installation + usage guidance).
