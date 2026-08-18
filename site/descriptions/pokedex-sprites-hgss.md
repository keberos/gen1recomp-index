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

Untested in-game as of this release. Worth checking: the dex list scroll, a few full
entries at different sprite sizes (a tall one like Alakazam, a wide one like Arcanine), and
that battle/summary art is still vanilla.
