The Pokédex draws every species with its original Game Boy sprite. This swaps that art
for HeartGold/SoulSilver-style sprites, for all 151 species.

**Only the Pokédex entry page.** Open the Pokédex, highlight a Pokémon you've caught and
choose **DATA** — that page is where the picture lives. The Pokédex *list* draws no sprite
at all in Gen 1, so scrolling it never looks different. Battle, the party summary screen,
evolution, Hall of Fame, trade, the title screen, and Professor Oak's lab all keep their
original art untouched.

**How it works.** `src/pokemon/Sprites.lua` raises a public `pokemon.sprite` hook carrying
`ctx.kind`, so a hook can tell which screen is asking for art — `"battle"`, `"dex"`,
`"summary"`, and so on. This mod answers only when `ctx.kind == "dex"` and falls through
untouched everywhere else.

**No permissions required.** It never reaches into an internal engine module directly —
only the public `mod.hooks` and `mod.assets` APIs every mod already has.

**Art.** Sprites are trimmed to their opaque pixel bounds and scaled down (never up) to
fit within 64×60px, so nothing crowds the stats text on the entry page or gets clipped off
the top. Source: HeartGold/SoulSilver sprite rips from Bulbagarden Archives — personal,
non-commercial use, and this is an unofficial fan-art swap, not affiliated with or endorsed
by Nintendo, Creatures Inc., GAME FREAK inc., or The Pokémon Company.

**Why 0.1.0 did nothing, and what 0.3.0 changed.** The first build went only through the
public `pokemon.sprite` hook. A diagnostic build proved that hook was never raised even
once, while this mod's *other* hook fired normally — so the bus worked and `Sprites.path`
simply wasn't being reached. The engine history explains it: `DexEntryMenu` only began
resolving its picture through `Sprites.path` between releases **v0.1.20 and v0.1.30**, and
`Sprites.lua` at v0.1.0 raises no hook at all. On an older engine a hook-only mod is
silently inert, with nothing broken anywhere to find.

0.3.0 wraps `DexEntryMenu.new` and replaces the sprite on the finished screen instead,
which works on every engine version. The hook is kept too — it's the only route to
Yellow's PRNT printer job. Full-colour art is marked to survive the SGB shade remap rather
than coming back washed out. This version needs the `engine_internals` permission.

Still carries three temporary `SPR` diagnostic rows in the START menu, and is not yet
confirmed rendering in play.
