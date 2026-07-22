# OPL Cheat Selection Persistence

A focused Open PS2 Loader modification that adds persistent per-game PS2RD cheat selections.

## Features

- Saves optional cheat selections in the normal per-game OPL CFG.
- Stores selections by normalized cheat name rather than list position.
- Keeps `Mastercode` / `Master Code` enabled and locked.
- Defaults optional cheats to OFF when no saved selection exists.
- Restores selections during PSBBN auto-launch without opening the selector.
- Leaves OPL's automatic enable-all cheat mode unchanged.

Example CFG entries:

```ini
$CheatSel000=Infinite Health
$CheatSel001=Widescreen
```

## Verified build

The hardware-tested persistence build was produced as:

```text
OPNPS2LD_PSBBN_Beta2245_CheatPersistence_ATA_BDM.ELF
```

SHA-256:

```text
fe01caa341d106dc704f4cca83e8ad528440e266aa54d20f336cda143b6fc4b2
```

The binary itself is not stored in this initial source commit. Build artifacts can be attached separately as a GitHub Release.

## Patch target

The included patch was originally prepared against OPL 1.2.0 Beta-2210 commit:

```text
6b300b098c9b48c1b2d541b52b644a12ba99e0af
```

Because OPL continues to evolve, the patch should be rebased and reviewed against current upstream before submission.

## Upstream contribution scope

The upstream-facing change should remain generic:

- persistent selections by cheat name;
- safe optional-cheat defaults;
- locked master code;
- silent restoration during auto-launch.

PSBBN-specific storage-device defaults should remain outside the generic upstream pull request.

## License

This work is intended for use with Open PS2 Loader and is distributed under the same GPL-compatible terms as the upstream project. See `LICENSE`.
