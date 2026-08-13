Four one-button shortcuts instead of menu digging. All four actions are
verified in-game, including Safari Zone's separate BALL branch and FLY
under a mod that broadens field-move eligibility.

| Action | Default | Vanilla path it replaces |
|---|---|---|
| TOWN MAP | **Y** (+ M on keyboard) | START → ITEM → scroll → A |
| BICYCLE | **L3** (stick click) | START → ITEM → scroll → A |
| FLY | **R3** (stick click) | START → POKéMON → pick a mon → FLY |
| Throw preferred ball | **X**, battle only | ITEM → scroll → A, every single throw |

Every one of the four is independently remappable in the mod's options,
including to shoulders and triggers.

**Includes TOWN MAP, and stands alone.** A sibling mod,
[Quick Map](https://github.com/keberos/quickmap), does the TOWN MAP button
on its own — this mod does the same action too, so it doesn't need Quick
Map installed. Running both together works (different option keys,
different wrap-guard names) but is redundant; this mod's own START MENU
ROW defaults off for that reason.

**Why this needs a mod at all.** The rebinding screen under OPTION →
CONTROLS rebinds the eight Game Boy buttons and nothing else — every
physical source in the engine, keyboard and controller alike, is mapped
onto up/down/left/right/A/B/START/SELECT. There is no "get on the bike" or
"throw a ball" action anywhere to bind a button to. So this mod makes
four.

**One button, two meanings.** The ball button only ever does anything
mid-battle; MAP/BIKE/FLY only ever do anything while free-roaming. Those
can't both be true at once, so the same physical button safely carries a
battle action and an overworld action together.

**The ball button.** Throws whichever ball PREFERRED BALL is set to —
never MASTER BALL by default, so an accidental press can't burn the
one-of-a-kind. Goes through the same engine method the bag's own throw
uses, so a trainer blocking the ball and a ghost battle's guaranteed dodge
come for free. Safari Zone gets its own path and ignores PREFERRED BALL
entirely, since Safari never uses a regular ball.

No ROM data or game assets are included. Every action calls the engine's
own methods — the same bicycle toggle, the same FLY warp, the same ball
throw the bag itself uses.

**Two real bugs, found and fixed by in-game testing before promotion.**

The BALL button's first release threw a ball that never visibly
appeared — a press beeped but did nothing, and opening the bag afterward
played the throw back late, looped. `BattleState:throwBall` only *queues*
its sequence; it never sets `self.phase`, and the engine only drains that
queue while `phase == "messages"`. The vanilla bag flow never hits this,
because choosing ITEM already makes that switch before the bag ever
reaches `throwBall`. This hotkey was skipping straight to `throwBall` from
`phase == "menu"`, so the sequence silently stalled. Fixed by setting the
same two fields `openItems`/`openParty` already set before any other
queued sequence.

FLY always refused with `No POKéMON knows FLY.` for a player running a
separate mod that widens field-move eligibility to any Pokémon that can
*learn* a move, not only one with it in an active slot. The cause: this
mod's FLY check hand-rolled the vanilla badge+moveset test directly
instead of calling `OverworldState:partyKnows(moveId)` — the engine's own
extension point for exactly this question, which runs that same check
*through* a `fieldmove.eligibility` hook other mods can widen. A
hand-rolled duplicate can never see a hook another mod wraps. Fixed by
calling `partyKnows` instead of reimplementing it.
