Every Poké Ball in the game renders grey. This colours all of them.

**The ball you throw.** It gets a fixed palette per ball type — red Poké,
blue Great, gold Ultra, purple Master, green Safari — with the Master and
Ultra flicker kept intact. Before this, the ball had no palette of its own:
the engine resolved it against the palette zone under that part of the
screen, so mid-arc it wore the colours of the Pokémon you were throwing it
at. A ball thrown at a Tentacool came out blue.

**The party ball rows**, yours and the opposing trainer's, and in link
battles too. Each of the four states keeps its own reading: red for healthy,
amber for statused, dimmed grey for fainted, and the empty socket left as
the engine draws it. Those rows exist to tell you the state of a team at a
glance, so they are coloured to say that rather than to be uniformly pretty.

**The Pokémon Center healing machine**, whose balls light up one per party
member.

**Why they were grey.** Not an oversight — the ball's OAM palette slot maps
to shades 0 and 3, the near-white and near-black anchors of whatever palette
is underneath, so hue is discarded before any palette is consulted. That is
faithful to the hardware, where the toss genuinely is white-and-black, and
it is why no COLORS palette mod can reach these.

**A fix that carries further than balls.** Under the WIDE battle layout the
engine never colourises the battle animation layer at all — it hands the
draw no colour function, so raw Game Boy greys go straight to screen for
every animation sprite, not just balls. This mod turns that on, so wide-layout
players get the whole layer back.

**On taste and tinkering.** Every colour is a plain 0–255 RGB table at the
top of `main.lua`. Change the red, retune a state, or point a ball type
somewhere else without touching any logic.

**Playing with the VoxelMod battle-art fork?** That fork bakes the party HUD
through a shader that flips near-black pixels to white over a dark backdrop,
so its own text stays legible. It has no idea this mod exists, and was
flipping the ball row's outline the same way — read as grey and white. 1.0.1
detects the fork and swaps in a palette that clears its threshold with real
margin instead.

No ROM data or game assets are included. The party-row and healing-machine
art is recoloured at runtime from your own imported cache.

Verified in game: the thrown Poké Ball, the party rows, the healing machine.
Not yet tested: the statused and fainted icons, the non-Poké ball colours,
and the Master/Ultra flicker. The VoxelMod fix is verified by math against
the fork's real shader source, not yet confirmed in play.
