# Cyber Ronin Sprite Pack 1.1

15 characters and 2371 hand-checked animation frames from the cyberpunk samurai roguelite
[Cyber Ronin](https://pavelekh.itch.io/cyber-ronin): the Last Ronin, his enemies and bosses.
Painted (not pixel-art) sprites with soft anti-aliased edges, all facing right, all at the same scale:
regular characters are about 126 px tall, bosses about 172 px.

## What's inside

Every character has its own folder:

```
<character>/
  <character>.png    sprite sheet, main colour set
  <character>.json   frame data: rectangles, durations, animation tags, pivot, jump phases, air-attack sequence, hitboxes (Aseprite JSON, array)
  <character>.tres   ready-made SpriteFrames for Godot 4
  frames/<anim>/     every frame as a separate PNG
  raw/               the same sheet in the original, slightly brighter colours
  half/              the same sheet at 50% size, downscaled with high quality
```

`raw` is the colour straight from the source; the main set is toned down a little (×0.85) so that all
characters sit together in a dark scene. Pick whichever suits your game.

## Sheet layout

* All frames of one character share one cell size, so the sheet is a plain grid: **8 columns**, and
  **every animation starts on a new row** (long animations wrap onto the next rows).
* Order of animations and exact rectangles are in the JSON (`meta.frameTags`, `frames`).
* **Pivot** = the point between the feet on the ground line. It is the same for every frame of a
  character, so animations never slide when you switch between them. In the JSON: `meta.pivot` (pixels
  from the top-left of a cell), `meta.pivotNormalized` (0..1 from the top-left: Godot, Aseprite) and
  `meta.pivotUnity` (0..1 from the bottom-left: Unity). For `half/` divide pixel values by 2.
* No frame touches the cell edge; there is a little empty margin around every character.

| folder | character | cell (px) | pivot x, y (px) | animations (frames) |
|---|---|---|---|---|
| `last-ronin/` | Last Ronin | 194×174 | 100, 154 | idle 13, walk 21, run 21, run_old 21, attack 14, attack2 16, attack3 16, block 29, crouch 10, crouch_idle 16, crouch_up 10, jump 14, jump_to_attack 6, jump_attack 25, dash 20, dash2 19, hurt 16, death 18, knockdown 10, getup 18 |
| `admin-oni/` | Admin Oni | 218×224 | 98, 204 | idle 16, walk 26, run 26, attack 16, block 16, jump 16, hurt 17, death 14 |
| `armorer/` | Armorer | 218×218 | 104, 202 | idle 16, walk 19, run 18, attack 14, throw 16, block 16, jump 16, hurt 16, death 12 |
| `beta-warden/` | Beta Warden | 336×272 | 148, 260 | idle 16, walk 25, run 22, attack 16, block 16, jump 16, hurt 16, death 14 |
| `drone/` | Drone | 168×134 | 80, 102 | fly 16, hurt 16, death 14 |
| `fencer/` | Fencer | 236×174 | 80, 158 | idle 16, walk 45, run 24, attack 29, block 33, jump 16, hurt 29, death 14 |
| `maglev-warden/` | Maglev Warden | 296×286 | 100, 270 | idle 16, walk 24, run 17, attack 16, block 16, jump 16, hurt 16, death 14 |
| `pendulum/` | Pendulum | 182×170 | 92, 154 | idle 16, walk 24, run 20, attack 16, block 16, jump 16, hurt 16, death 14 |
| `shield/` | Shield | 160×150 | 82, 140 | idle 16, walk 31, walk2 27, run 16, attack 16, block 16, jump 16, hurt 17, death 14 |
| `shogun-fists/` | Shogun (fists) | 334×288 | 128, 276 | idle 16, walk 27, run 26, attack 16, block 16, jump 16, hurt 16, death 14, death2 14 |
| `shogun-sword/` | Shogun (sword) | 312×296 | 112, 264 | idle 16, walk 34, run 19, attack 16, block 16, jump 16, hurt 17, death 14, death2 14 |
| `the-double/` | The Double | 332×316 | 112, 302 | idle 16, walk 26, run 27, attack 28, attack2 16, block 16, jump 16, hurt 16, death 14 |
| `thrower/` | Thrower | 180×158 | 102, 144 | idle 16, walk 30, run 13, throw 16, block 16, jump 16, hurt 16, death 14 |
| `tracer/` | Tracer | 164×152 | 84, 138 | idle 16, walk 21, run 14, attack 14, block 16, jump 16, hurt 17, death 14 |
| `twin/` | Twin | 150×154 | 68, 142 | idle 16, walk 23, run 15, attack 16, block 16, jump 16, hurt 16, death 18, death2 14 |

## Timing

Frame rates below are what the animations were made for; each frame's duration is also in the JSON.

| animation | what it is | fps | per frame | loops |
|---|---|---|---|---|
| `idle` | standing loop | 8 | 125 ms | yes |
| `fly` | hover loop | 11.1 | 90 ms | yes |
| `walk` | walk loop | 11.1 | 90 ms | yes |
| `walk2` | alt. walk loop | 11.1 | 90 ms | yes |
| `run` | run loop | 15.9 | 63 ms | yes |
| `run_old` | **deprecated** — the previous run loop (long wide blade), kept for older projects; use `run` | 15.9 | 63 ms | yes |
| `attack` | attack | 16.7 | 60 ms | no |
| `attack2` | second attack | 16.7 | 60 ms | no |
| `attack3` | stepping attack | 16.7 | 60 ms | no |
| `throw` | throw | 12.5 | 80 ms | no |
| `block` | block | 14.3 | 70 ms | no |
| `crouch` | stand → crouch | 14.3 | 70 ms | no |
| `crouch_idle` | crouching loop | 8 | 125 ms | yes |
| `crouch_up` | crouch → stand | 14.3 | 70 ms | no |
| `jump` | jump in place | 12.5 | 80 ms | no |
| `jump_to_attack` | mid-air bridge: from the top of `jump` (frame 4) into `jump_attack` — continue `jump_attack` from frame 9 | 14.3 | 70 ms | no |
| `jump_attack` | jump with a downward cut, lands in the stance | 16.7 | 60 ms | no |
| `dash` | dash forward and stop | 16.7 | 60 ms | no |
| `dash2` | alt. dash | 16.7 | 60 ms | no |
| `hurt` | hit reaction | 11.1 | 90 ms | no |
| `death` | death | 10 | 100 ms | no |
| `death2` | alt. death | 10 | 100 ms | no |
| `knockdown` | knocked down onto the back (getup starts from its last pose) | 12.5 | 80 ms | no |
| `getup` | get up from the ground | 12.5 | 80 ms | no |

The Drone has no idle: it uses `fly` as its standing loop. Its pivot is on the ground line under it, like everyone else's.

## Jump phases and hit frames

* **Jump phases.** Every `jump` is also split into four tags over the same frames: `jump_start` (crouch before
  take-off), `jump_rise`, `jump_fall` and `jump_land`. For a platformer, play `jump_start` on the button,
  hold `jump_rise` / `jump_fall` while in the air (the jumps in the pack are short hops) and `jump_land` on touch-down.
  In Godot they are separate animations in the `.tres`.
* **Air attack (Last Ronin).** `jump_attack` is a full leap from the ground and has the same four phase tags
  (`jump_attack_start`, `_rise`, `_fall`, `_land`; the slam is its active frames, on landing). When the player presses
  attack *during* a `jump`, play the sequence `air_attack` instead: the bridge `jump_to_attack` (from the top of the
  jump into the raised blade), then `jump_attack` from its frame 9 to the end. In the JSON it is `meta.sequences` →
  `air_attack` (sheet frame indices in play order, `enterFrom`: start it from `jump_rise` or the first `jump_fall`
  frame; the bridge starts in the pose of `jump` frame 4, the top). In Godot it is one more animation, `air_attack`,
  in the `.tres`; `get_meta("active_frames")["air_attack"]` and `get_meta("hitboxes")["air_attack"]` give the slam's hit
  frames inside it.
* **Active frames.** Each attack/throw tag has `activeFrames` (`from`, `to`, sheet frame indices): the frames where
  the blade, fist or splash is out in front. Deal damage on those.
* **Hitboxes.** `meta.slices` has one slice per attack, `hitbox_<anim>`, with a key for every active frame
  (`bounds` in cell pixels, like Aseprite). Boxes cover what sticks out in front of the standing pose, facing right;
  mirror them around the pivot for a left-facing character. They are a sensible starting point, not frame-perfect
  collision: tune them to your game's feel.
* In Godot, `.tres` metadata has the same data: `sprite_frames.get_meta("active_frames")` → `{"attack": Vector2i(first, last)}`
  (frame numbers inside the animation) and `get_meta("hitboxes")` → `{"attack": [Rect2, …]}`, one rectangle per active
  frame, relative to the pivot (the node origin when Offset is set as below).

## Godot 4

1. Copy a character folder into your project.
2. Add an `AnimatedSprite2D`, set **Sprite Frames** to `<character>.tres`. All animations come with their fps and loop flags.
3. To put the node's origin between the feet, set **Offset** to the value in the comment at the top of the `.tres` file (also: cell centre minus pivot).
4. Import settings: keep **Filter = Linear** (the project default). Do not use Nearest: these are not pixel-art sprites.

## Unity

1. Import `<character>.png`, set **Sprite Mode = Multiple**, **Filter Mode = Bilinear**, **Compression = None**, **Max Size = 8192**.
2. Sprite Editor → Slice → **Grid By Cell Size** with the cell from the table above, Pivot = **Custom** with `meta.pivotUnity` from the JSON.
3. Frame order and fps per animation are in the JSON (`frameTags`) and in the timing table.

## Other engines and tools

The JSON follows Aseprite's "array" export, which most sprite tools and engine importers read
(Phaser, PixiJS, Defold, GameMaker and LibGDX plug-ins, etc.). Or just use the PNGs in `frames/`.

**Filtering.** Use linear / bilinear filtering. Nearest-neighbour filtering is made for pixel art; on these sprites
it gives jagged edges and shimmering when scaled. If you show the characters much smaller than 50%, enable mipmaps
or start from the `half/` sheets.

## Changes

### 1.1

* Last Ronin: 9 new animations — `crouch`, `crouch_idle`, `crouch_up`, `jump_attack`, `jump_to_attack` (a mid-air bridge from the top of `jump` into `jump_attack`), `dash`, `dash2`, `knockdown` and `getup` (it starts from the last pose of `knockdown`)
* Last Ronin: a new matte `idle` and a new `jump`; every other animation is colour-matched to the new idle
* Last Ronin: a new run (thin katana in the rear hand); the previous one stays as `run_old`, marked deprecated
* Last Ronin: no dark outline around the glowing katana on light backgrounds
* Gameplay data for every character: jump phase tags (`jump_start`, `_rise`, `_fall`, `_land`; the same for `jump_attack`), active hit frames and hitboxes for every attack — in the JSON (`activeFrames`, `meta.slices`) and in the Godot `.tres` metadata
* Last Ronin: the `air_attack` sequence for an attack pressed mid-jump (`meta.sequences` in the JSON, an animation in the `.tres`)

## License

You may use these sprites in any project, free or commercial, and modify them however you like.
You may not resell or re-share the sprites themselves. Full text: `LICENSE.txt`.
Credit is not required but appreciated: "Sprites: Cyber Ronin Sprite Pack by PavelEKh".

## How they were made

Characters were designed and animated with generative AI tools, then cut out, aligned, colour-matched, looped and
cleaned up frame by frame by hand.
