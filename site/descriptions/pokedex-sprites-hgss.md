The Pokédex draws every species with its original Game Boy sprite. This swaps that art
for HeartGold/SoulSilver-style sprites, for all 151 species, and gives the caught-species
marker a modern Poké Ball.

**The entry page.** Open the Pokédex, highlight a Pokémon you've caught and choose
**DATA** — that page is where the picture lives. The Pokédex *list* draws no sprite of its
own in Gen 1, so scrolling it never shows different art. Battle, the party summary screen,
evolution, Hall of Fame, trade, the title screen, and Professor Oak's lab all keep their
original art untouched.

**The caught marker.** The list marks every caught species with a small ball, drawn inline
as a flat black disc with no asset behind it. This repaints it as a proper Poké Ball — red
top, white bottom, dark band and outline, white release button. A **CAUGHT BALL** option in
the mod manager switches back to the vanilla marker.

**How it works.** The swap wraps `DexEntryMenu.new` and replaces the sprite on the finished
screen, which works on every engine version. It also answers the public `pokemon.sprite`
hook where that is raised, since that is the only route to Yellow's PRNT printer job.
Requires the `engine_internals` permission.

**Why the first release did nothing.** 0.1.0 went only through `pokemon.sprite`. A
diagnostic build proved the hook was never raised even once, while this mod's *other* hook
fired normally — so the bus worked and `Sprites.path` simply wasn't being reached.
`DexEntryMenu` only began resolving its picture through `Sprites.path` between engine
releases **v0.1.20 and v0.1.30**, and `Sprites.lua` at v0.1.0 raises no hook at all. On an
older engine a hook-only mod is silently inert, with nothing broken anywhere to find.

**Why the art is masked rather than boxed.** Full-colour art has to sit out the SGB shade
pass, which keys on the red channel and would otherwise return a baked red as white.
`markTrueColor` is the escape hatch, but it re-blits the whole rect it is handed — including
transparent pixels — which repaints the page background raw white as a grey slab, and a tall
sprite drawn at y = 0 reached above the mon-pic zone and broke the page's brown border. So
sprites are capped at vanilla's own 56px front-pic limit, and each one carries a span mask
so only opaque pixels are ever marked. The ball marker gets a disc mask for the same reason.

**Useful Dex: either/or for the sprites.** Nothing breaks if both are installed and no hard
conflict is declared, but Useful Dex registers its own dex screens, and a registry record
beats the builtin. The modern caught-ball marker still works — its list is built on the
engine's `PokedexMenu` and still renders through `ListMenu`. The entry-page sprite swap does
not: its `setSpecies()` re-resolves the picture through `Sprites.path` with `kind = "battle"`
(deliberately, so skin mods apply) and overwrites the swapped art, and it draws with its own
screen rather than the engine's, so the true-colour mask never runs either. Run one or the
other for the sprites.

**Art.** HeartGold/SoulSilver sprite rips from Bulbagarden Archives, trimmed to their opaque
bounds — personal, non-commercial use. An unofficial fan-art swap, not affiliated with or
endorsed by Nintendo, Creatures Inc., GAME FREAK inc., or The Pokémon Company.

Verified in game.
