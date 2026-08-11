**Experimental.** New, and not yet verified in game.

Three one-button shortcuts instead of menu digging.

| Action | Default | Vanilla path it replaces |
|---|---|---|
| BICYCLE | **L3** (stick click) | START → ITEM → scroll → A |
| FLY | **R3** (stick click) | START → POKéMON → pick a mon → FLY |
| Throw preferred ball | **X**, battle only | ITEM → scroll → A, every single throw |

Every one of the three is independently remappable in the mod's options,
including to shoulders and triggers.

**A sibling to [Quick Map](https://github.com/keberos/quickmap)**, which
does the same for the TOWN MAP button and nothing else. The two don't
overlap — this mod never touches MAP, and doesn't share an option key or a
wrap-guard field with it — so they install together or alone with no
conflict.

**Why this needs a mod at all.** The rebinding screen under OPTION →
CONTROLS rebinds the eight Game Boy buttons and nothing else — every
physical source in the engine, keyboard and controller alike, is mapped
onto up/down/left/right/A/B/START/SELECT. There is no "get on the bike" or
"throw a ball" action anywhere to bind a button to. So this mod makes
three.

**One button, two meanings.** The ball button only ever does anything
mid-battle; BIKE and FLY only ever do anything while free-roaming. Those
can't both be true at once, so the same physical button safely carries a
battle action and an overworld action together — nothing stops you from
putting the ball throw on the same button as the bike or fly.

**Why these buttons.** On a standard controller the d-pad, A, B, START and
SELECT are already Game Boy buttons, and all four shoulders and triggers
cycle game speed. That leaves X, Y, and the two stick clicks as the only
buttons doing nothing at all — hence the defaults (L3 bike, R3 fly, X
ball). The SELECT+X and SELECT+Y display chords still work — a press with
SELECT held goes straight through, untouched.

**The ball button.** Throws whichever ball PREFERRED BALL is set to —
never MASTER BALL by default, so an accidental press can't burn the
one-of-a-kind. Goes through the same engine method the bag's own throw
uses, so a trainer blocking the ball and a ghost battle's guaranteed dodge
come for free. Safari Zone gets its own path and ignores PREFERRED BALL
entirely, since Safari never uses a regular ball — included deliberately
rather than carved out, so the button works everywhere rather than almost
everywhere.

**It stays out of the way.** BIKE and FLY only work while actually walking
around: not in a battle, not in a menu, not during a cutscene or a text
box, not while a trainer is spotting you. BALL only works while a battle's
own menu is showing, never during the old man's scripted catching
tutorial. Anywhere a button's action doesn't apply, the press goes to the
engine untouched — a shoulder bound to BIKE still cycles game speed
whenever the bike genuinely can't apply. Once an action DOES apply though,
the button is claimed even if the specific attempt is refused (surfing, no
cycling here, out of balls) — a refusal is still a response, and a
silently dead button reads as broken.

No ROM data or game assets are included. Every action calls the engine's
own methods — the same bicycle toggle, the same FLY warp, the same ball
throw the bag itself uses.

Untested in game: all three actions, every non-default button choice, and
the raw-pad escape hatch.
