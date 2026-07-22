# Applying the patches

Start from Open PS2 Loader commit:

```text
3e3f34e9f94b058f7fd5b13727cb86e94fd3b35d
```

Apply the generic feature patch:

```bash
git apply patches/0001-cheat-persistence-and-paging.patch
```

For PSBBN internal exFAT/ATA use, also apply:

```bash
git apply patches/0002-psbbn-ata-bdm-defaults.patch
```

The full modified tree in this repository already contains both patches.
