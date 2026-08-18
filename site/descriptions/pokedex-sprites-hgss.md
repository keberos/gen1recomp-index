The Pokédex draws every species with its original Game Boy sprite. This swaps that art
for HeartGold/SoulSilver-style sprites, for all 151 species.

**Only the Pokédex.** The list-view preview and the full entry page both change; battle,
the party summary screen, evolution, Hall of Fame, trade, the title screen, and Professor
Oak's lab all keep their original art untouched.

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

**0.2.0 is a diagnostic build.** 0.1.0 changed nothing in game, and static analysis found
no fault — the hook exists in the current engine release, the wiring matches the bundled
example mods, and the species ids are correct for Gen 1. So this build makes the game
report which branch actually runs rather than guessing a second time.

Open the Pokédex, back out, then press START and read the three `SPR` rows: how many
`pokemon.sprite` calls were seen, how many arrived with kind `dex`, and the last dex
species id with HIT or MISS against the art table. No rows at all means the mod is not
loading. The sprite swap itself is unchanged and still in; the rows come out once the
cause is known.
