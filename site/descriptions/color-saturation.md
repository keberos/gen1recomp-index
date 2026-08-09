One dial for how colourful the game is, with the colours themselves left alone.

**The problem it solves.** ADVANCED resolves real per-tile colour and can read
hot. Every palette that tones it down does so by dragging every hue toward one
family — sepia goes warm, ocean goes cool, pocket goes grey. That is a different
*look*, not a quieter version of the same one.

**What it does instead.** Scales each colour's distance from grey and nothing
else. Luminance stays exactly where it was, hue stays exactly where it was, only
chroma moves. So **70** is ADVANCED with the shouting turned down — the same
greens and reds in the same places — and **150** is louder than vanilla.

**Zero is worth a look.** It gives a true greyscale derived from the real
colours, where each one greys to *its own* brightness. A four-rung greyscale
palette can't do that: it quantises everything onto four fixed values.

**Where it hooks.** The four colour-producing functions that between them cover
everything the renderer asks for a colour: the overworld's background palettes,
overworld sprites' OBJ palettes, a Pokémon's own colours, and the named palettes
behind battle backdrops and menus.

**On the bake caches.** ADVANCED doesn't shade at draw time, it bakes tileset
atlases and sprite sheets into several different caches. The dial extends the
one keyed on display mode and flushes the others by hand — only the ones that
can hold a baked colour, deferred until the menus close, so audio is never
touched and dragging the dial costs one rebuild, not one per step. At 100 every
wrapper calls straight through, so the default costs nothing at all.

Set COLORS to ADVANCED for the intended effect. Groovy Palette can stay
installed — it only intervenes when one of its own palettes is selected.

No ROM data or game assets are included.

**Verified in-game** across the overworld, interiors and character sprites.
