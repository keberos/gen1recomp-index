Ember, Thundershock, Water Gun, Vine Whip — every battle move animation in
the game renders as two-tone white-and-black. This gives each one a palette
drawn from its move's elemental type.

**Why they are colourless.** Nearly every animation tile is stamped with the
`f0` OBJ palette slot, and that slot maps to shades 0 and 3 — the lightest
and darkest anchors of the palette underneath. Hue lives in shades 1 and 2,
which `f0` never selects. So the colour is discarded before any palette is
consulted, which is why no COLORS palette mod can reach these: there is
nothing left for it to colour. On real hardware these animations run under
`wAnimPalette $f0` and genuinely are monochrome, so this is a deliberate
departure from the original rather than a bug fix.

**How the colours are chosen.** Not by hand-indexing 165 moves. Animations
are keyed by move name, and each move already declares an elemental type, so
fifteen type ramps cover the entire move list — with a short exception list
for the few that read wrong in their own type's colours. Explosion and
Self-Destruct borrow Fire; Hyper Beam gets its own violet.

Each ramp is three stops — highlight, body, edge — mapped onto the sprite's
three colours. Normal moves stay near-white on purpose, so a Tackle still
reads as the plain impact it is.

**What it leaves alone.** Sprites that already resolve the full colour range,
and animations that are not moves — the ball toss, the send-out poof, the
status chains. Those keep the engine's own handling, so this composes with
Pokeball Colorfix in either load order.

**Tinkering.** Both tables sit at the top of `main.lua` as plain 0–255 RGB.
Ramps must fall in brightness across the row, light to dark, or the effect
renders inside out.

No ROM data or game assets are included.

Marked experimental: the mechanism is verified against the engine source, but
the colour choices have had limited play-testing.
