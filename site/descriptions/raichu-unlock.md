Lets your starter PIKACHU evolve into RAICHU with a THUNDER STONE, and turn it
back with a second one.

**Why Yellow needs this at all.** `item_effects.asm` runs
`IsThisPartyMonStarterPikachu` before `TryEvolvingMon` and refuses the stone on
the Pikachu Oak gave you — an OT-identity check, not a species check, so it
isn't really "Pikachu can't evolve," it's "*this* Pikachu can't." That would be
moot except Yellow has no other Pikachu to point the stone at: grepping the
disassembly's wild encounter tables for `PIKACHU` or `RAICHU` turns up nothing
at all. One Pikachu on the cartridge, and it's the one that says no. The
evolution data itself is untouched in the ROM — `evos_moves.asm` still lists
the Thunder Stone row — so nothing here is invented, only the refusal lifted.

**The revert.** A second stone on the resulting Raichu turns it back. Vanilla
stones already do nothing to a Raichu (`RaichuEvosMoves` has no evolution
rows), so this claims an otherwise-dead case rather than overriding anything,
and it looks up which item triggers it from Pikachu's own evolution data
rather than hardcoding Thunder Stone by name. Both directions run through the
engine's real evolution screen and stat recalculation unmodified — HP is
preserved as a *deficit*, not a raw value, so reverting can't heal or clip
you, and the Pokédex entry for the species you're leaving is never cleared.
The walking Pikachu follower and Pikachu's Beach key purely on `mon.species`,
so they come back on their own the moment you revert.

One accepted wart: the evolution screen's on-screen text is hardcoded for one
direction only, so a revert reads a little backwards ("RAICHU evolved into
PIKACHU!"). Reusing the real screen instead of writing a parallel one was
judged worth that, since everything else about it — the flash animation, the
cry, the non-cancelable stone behavior, the post-transform level-up move
check — is genuine engine machinery either way.

Two independent options: ALLOW EVOLUTION and ALLOW REVERT, both read live with
no restart.

No ROM data or game assets are included.

**Untested.** The mechanism is verified against the engine source — the
OT-identity gate, the data-driven stone lookup, the symmetry of
`Evolution.apply` — but no in-game run has happened yet. Published early so it
can be installed on a device for testing.
