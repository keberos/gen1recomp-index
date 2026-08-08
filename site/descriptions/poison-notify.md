Field poison tells you a tick landed by darkening the **whole screen** for
two 4-frame pulses, every fourth step, for as long as anything in your party
is poisoned. This puts that notice in a corner badge instead.

**Why it matters more than it used to.** On a Game Boy the flash was one BG
palette register write — the screen was 160x144 and the effect was over in a
fifth of a second. Over a 3D renderer it is a full-screen veil that strobes
the entire diorama dark while you walk, and it reads as the view stuttering
whether or not anything is actually stuttering.

**PSN ALERT.** `CHIP` is a purple `PSN` badge in the screen's top-left
corner, held for about 0.8 seconds — it pulses on the same 4-frame beat the
hardware flash used, then holds steady so it stays readable. `EDGE` pulses
the screen border instead, about a twelfth of the vanilla fill. `VANILLA`
keeps the engine's flash untouched. `OFF` draws nothing.

**It docks to the screen, not to the Game Boy canvas.** The 160x144 canvas is
letterboxed into the window, so on a 16:9 display its corner is a good way
into the picture and its border is a rectangle floating in the middle. The
badge is laid out in window space instead, against the cutout-safe rect, so
it reaches the real screen edge whatever the aspect ratio — the same layer
the on-screen touch pad draws in.

**PSN SOUND.** The poison step sound effect, on its own ON/OFF row. Off
leaves the badge as the only notice.

Both rows sit on the OPTIONS menu and on this mod's page in the mod manager,
and write the same stored value, so they cannot disagree.

**PSN LOW.** Under `CHIP`, a poisoned Pokemon at 4 HP or less — four more
ticks, sixteen more steps — turns the badge red and it reads `PSN LOW`. Field
poison can black you out while you are looking at the road, and the vanilla
flash looks identical at 40 HP and at 1.

**On frame time.** The vanilla flash is a single alpha rectangle drawn into
the 160x144 UI canvas, the same canvas a dialogue box uses, and the engine's
UI blit runs every frame whether that canvas is empty or not. So the flash is
very unlikely to be *costing* anything — it is what makes a hitch visible,
because the whole screen moves at the moment it lands. Setting both rows to
`OFF` makes a poison tick invisible and silent, which is how to tell the two
apart.

**What it touches.** No render pipeline, no world pass, no palette state. It
zeroes a counter the engine set and draws over the finished composite through
the `render.hud` hook — so it sits on top of a voxel or diorama renderer
rather than fighting it.

No ROM data or game assets are included.

Marked experimental: confirmed working in-game, but the badge's size and hold
time are likely to move before 1.0.
