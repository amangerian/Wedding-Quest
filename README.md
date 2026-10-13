# Alex & Katherine: A Love Quest

A small metroidvania for the wedding. Play it in any browser, phone or laptop.
There are three phases of our life, each one a connected map:

1. **College Park.** McKeldin Mall, Testudo, McKeldin Library and the Campus Drive
   underpass. Katherine joins at the top of the library.
2. **Bethesda.** The Metro escalator, Bethesda Row, our apartment (BA is waiting at home)
   and the Purple Line construction site (Mikey is at the MSPCA).
3. **The Birding Trail.** A forest, a marsh boardwalk and a dark hollow, ending at an
   overlook with the wedding arch. There are 12 birds to spot.

One button swaps between everyone you've found:

| Hero | Power |
|---|---|
| Alex | **Stethoscope Swing**: grab glowing rings and swing up to high places |
| Katherine | **Flip the System**: rewrites the code and flips gravity and the screen |
| BA | **Knock It Off**: swats things off ledges to make steps or hold down switches |
| Mikey | **Butt Bump**: dashes or slams through cracked rock |

The cats are small, so they fit through pet doors and tiny tunnels. Later abilities
open up places you passed earlier: the lake trail at College Park needs Mikey and BA,
and the binoculars there unlock the birding trail.

**Two character styles.** *Characters: Pixel* (the default, retro pixel art) or *Characters:
Cartoon* (smooth chibi art drawn at full screen resolution). Switch on the title screen or in
the pause menu; each device remembers its choice. On the birding trail and in the ending,
everyone changes into wedding clothes: a tux for Alex, a gown and veil for Katherine, a bow tie
for BA and a flower collar for Mikey.

## Controls

- **Keyboard:** arrows / WASD to move, Space / Z / ↑ to jump, X / Shift for the power,
  C / Q / Tab to swap, M for the map, Esc to pause.
- **Phone:** on-screen stick plus Jump, Power and Swap buttons. Sideways is best.
- **Game controller:** works too (A = jump, X/B = power, Y/bumpers = swap).

Progress saves automatically in the browser. A full run takes about 15–25 minutes.

## Leaderboard and guestbook

The title screen has a **Leaderboard** (most memories and birds found, then fastest time) and a
**Guestbook** where anyone can leave a note. Finishing the game offers to add you to the
leaderboard. Both are stored by a small Cloudflare Worker. Its code and step-by-step dashboard
setup are in [`cloudflare/`](cloudflare/SETUP.md). Until `CONFIG.apiBase` is filled in, both
features stay hidden and the game works offline exactly as before.

Moderate notes and runs at `<worker address>/admin`.

## Publishing (GitHub Pages)

1. github.com → **New repository** → name it `wedding-quest`, **Public**, Create.
2. **Add file → Upload files** → drop in `index.html` (and this README) → **Commit changes**.
3. **Settings → Pages** → Source: *Deploy from a branch*, branch `main`, folder `/ (root)` → Save.
4. Live in 1–2 minutes at **https://amangerian.github.io/wedding-quest/**

**To update:** open `index.html` in the repo → pencil icon → select all, paste the new
file → **Commit changes**. Then hard-refresh (Cmd+Shift+R). The "Last updated" date
on the title screen tells you which build you're looking at.

## Easy things to edit (all inside `index.html`)

- **`CONFIG`** near the top of the first `<script>`: the title, subtitle, phase names,
  the ending line, and **`weddingDate`**. Fill that in (e.g. `'June 6, 2027'`) and it
  shows on the ending screen. **`apiBase`** is the Worker address that turns on the
  leaderboard and guestbook.
- **Sign text:** the `signs: { ... }` blocks inside `ZONES`, one per zone.
- **Bird facts:** the `BIRDS` list.
- **Level layouts:** the `ZONES` maps. Each character is one 16-pixel tile, and the key
  is in the comment just above `const ZONES`.
- **Character art:** `HUMANS` (Alex, Katherine, plus the `alexW` / `katherineW` wedding
  versions) and `CATS` (BA, Mikey) for the pixel style. `TOON` holds the cartoon-style colours,
  including Katherine's bronde hair (`hair`, `hairHi`, `hairD`).
