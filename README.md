# keberos mod index

A personal [Gen1Recomp](https://github.com/bryanthaboi/gen1recomp) mod index.
Metadata only — the mods live in their own repos, and every install still goes
through the launcher's normal zip import.

## Add it in Gen1Recomp

**Launcher → MODS → Find mods → add a source**, then paste either:

```
keberos/gen1recomp-index
```

```
https://raw.githubusercontent.com/keberos/gen1recomp-index/main/site/data/index.json
```

The engine accepts a bare `owner/repo`, a GitHub repo URL, a Pages root, or the
feed file itself — all four resolve to the same source.

The launcher ships with **no** index sources and never adds one on its own, so
adding this is a deliberate act of trusting what it lists.

## Listed

| Mod | Version | |
| --- | --- | --- |
| [Pokeball Colorfix](https://github.com/keberos/pokeball-colorfix) | 1.0.0 | Colours every Poké Ball the engine leaves grey |
| [Pokemove Colorfix](https://github.com/keberos/pokemove-colorfix) | 1.1.3 | Colours battle move animations by elemental type |
| [Color Saturation](https://github.com/keberos/color-saturation) | 1.0.0 | One SATURATION dial for ADVANCED colours — no tone bias, hue and brightness untouched |
| [Poison Notify](https://github.com/keberos/poison-notify) | 0.2.0 | Corner PSN badge instead of the full-screen poison flash — experimental |
| [Raichu Unlock (Yellow)](https://github.com/keberos/raichu-unlock) | 1.0.0 | Lets the starter PIKACHU evolve into RAICHU with a Thunder Stone, and revert |
| [Quick Map](https://github.com/keberos/quickmap) | 1.1.0 | One-button shortcuts for TOWN MAP, BICYCLE, FLY, and throwing your preferred ball in battle |

## Layout

```
site/
  data/index.json          the feed
  descriptions/*.md        long-form text, one per mod
```

`site/data/index.json` is the path the engine's raw-GitHub fallback looks for,
so the index works **without GitHub Pages enabled**. If you later turn Pages on,
serve it from the `/site` folder on `main` and the primary feed URL
(`https://keberos.github.io/gen1recomp-index/data/index.json`) starts working too.

`description_url` values are absolute on purpose, so descriptions load either way.

## Feed contract

- `schema_version` must be `1`. It is a hard gate: an unknown version is refused
  outright, not parsed hopefully.
- Each entry needs an `id`. Everything else is optional, but a card can only be
  installed when it resolves a URL — either `update_check: "ok"` with a
  `latest.zip.url`, or a fixed `downloadURL`.
- Release asset filenames should be `<id>-<version>.zip`. That is the shape the
  launcher's updater looks for.
- Feeds are cached for 24 hours.

## Adding a mod

1. Publish the mod in its own repo with a release whose asset is
   `<id>-<version>.zip`.
2. Add an entry to `site/data/index.json` and a `site/descriptions/<id>.md`.
3. Add a row to the **Listed** table above, and bump its version there on every
   release. Nothing generates that table — it is the repo's shop window and the
   only part of this index a human reads first, so it is also the part that
   silently goes stale. The feed is what clients actually read; the table is
   what people do.
4. Commit and push. Clients pick it up within a day, or immediately on a fresh
   source add.

Keep `latest.zip.url`, `latest.tag` and `version` in step with the actual
release — nothing here verifies them, and a wrong URL is a 404 at install time.
