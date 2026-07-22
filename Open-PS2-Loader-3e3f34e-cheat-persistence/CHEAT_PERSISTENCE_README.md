# OPL Cheat Persistence and Paging

A source patch for **Open PS2 Loader v1.2.0-Beta-2245**, based on commit:

```text
3e3f34e9f94b058f7fd5b13727cb86e94fd3b35d
```

## Features

- Saves enabled PS2RD cheats in each game's normal OPL CFG file.
- Stores selections by normalized cheat name rather than list position.
- Survives cheat reordering, additions, removals, and regenerated databases.
- Required master/enable codes default on and cannot be toggled.
- Optional cheats default off on first use.
- Left and Right page through ten cheats at a time.
- Square saves selections without launching.
- Start saves selections and launches.
- Cancel is intentionally disabled because the stock selector is entered after launch preparation.
- PSBBN auto-launch restores saved selections silently and continues launching without opening the interactive selector.

## Saved CFG format

```ini
$CheatSel000=Infinite Health
$CheatSel001=Widescreen
$CheatSel002=Invert Camera Y
```

Names are compared case-insensitively. Leading, trailing, and repeated whitespace are normalized.

## Controls

| Button | Action |
|---|---|
| Up / Down | Move one entry |
| Left / Right | Previous / next page of ten |
| Cross or Circle | Toggle the selected optional cheat, according to OPL's configured Select button |
| Square | Save without launching |
| Start | Save and launch |

## PSBBN behavior

When OPL is launched directly, the selector is interactive.

When a title is launched through PSBBN's OPL auto-launch path, OPL restores the saved selections by name and launches silently. This preserves the PSBBN handoff.

The included full source tree also applies the PSBBN internal exFAT defaults:

```text
HDD/APA start mode: Off
BDM start mode: Auto
BDM HDD: On
```

For a generic OPL fork, apply `patches/0001-cheat-persistence-and-paging.patch` only. Apply `patches/0002-psbbn-ata-bdm-defaults.patch` when targeting PSBBN's internal exFAT layout.

## Build

Install the current PS2DEV toolchain and export:

```bash
export PS2DEV=/path/to/ps2dev
export PS2SDK="$PS2DEV/ps2sdk"
export GSKIT="$PS2DEV/gsKit"
export PATH="$PS2DEV/bin:$PS2DEV/ps2sdk/bin:$PS2DEV/ee/bin:$PS2DEV/iop/bin:$PATH"
```

Then build from the source directory:

```bash
make clean
make
```

The package includes the language and auxiliary source dependencies used for the verified compile, so its Makefile does not fetch them during the build.

## Verification status

The refactored source was compiler-verified through the final linked `opl.elf` stage with the official PS2DEV Ubuntu toolchain. The behavior represented by this source was hardware-tested in the preceding non-refactored build on:

- direct OPL launch
- PSBBN game launch
- internal ATA/BDM exFAT game storage
- saved cheat restoration by name
- ten-entry paging
- Square save-only

## Upstream contribution scope

A future upstream pull request should contain only the generic improvements:

- persistent cheat selections
- save by normalized cheat name
- locked required/master codes
- optional cheats default off
- automatic restoration

PSBBN-specific startup behavior, ATA/BDM defaults, and launcher-specific logic should remain project-specific. The generic work should be rebased onto current upstream OPL before submission.

## License

Open PS2 Loader retains its upstream license. This repository provides the complete corresponding modified source and retains the upstream `LICENSE` in the source tree.
