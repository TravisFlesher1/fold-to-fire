# Fold to Fire

**Blind-fire artillery, decided by a single fold.** A print-and-play pen-and-paper
game — and a board generator that makes an unlimited number of unique, printable
boards right in your browser.

▶ **Play / generate boards:** <https://travisflesher.com/fold-to-fire>
📖 **The story behind it:** <https://travisflesher.com/hobbies/fold-to-fire>

The whole thing is a single self-contained `index.html` — no build step, no
dependencies, no server. The web font and the PDF library are embedded, so you
can open the file straight off disk, fork it, and change anything you like.

---

## What it does

- **Generates a board** — a Letter-size sheet with a tilted fold line through the
  center (guaranteeing two equal-area halves), the reachable play area, and the
  grey ✕ "no-play" zones that a fold at that angle can't reach.
- **Deterministic seeds** — the same seed always makes the same board, so a shared
  link reproduces an exact board for both players.
- **Pick an exact angle** — or set the fold angle yourself instead of leaving it to
  the seed.
- **Print** the board, or **download a PDF** that includes the board plus a full
  rules page.

## Using the generator

| Control | What it does |
| --- | --- |
| **Seed** + **Generate** | Type any text and generate the board for that seed. |
| **Random** | Make a fresh random seed. |
| **Angle** + **Set** | Pin an exact fold angle (1°–89°) instead of using the seed's. |
| **Print board** | Open the browser print dialog (board only). |
| **Download PDF** | Save a 2-page PDF: the board + the rules. |

**Shareable links** — the board lives in the URL, so you can send someone the exact board:

- Seed: `…/fold-to-fire#your-seed`
- Fixed angle: `…/fold-to-fire#a=42.5`

## How to play

**You need:** a printed board (or a blank sheet), two different pen colors, and two players.

### Setup

**On a printed board** — the fold line and no-play zones are already drawn. Then:

1. Each player picks a different pen or pencil color (gel pens transfer best).
2. Both players draw the **same** set of 2–10+ shapes in varied sizes — identical
   shapes and sizes on each half; only the position and rotation differ. Keep every
   shape fully inside the play area, and don't let shapes touch or overlap. Be fair!
3. Play Rock Paper Scissors — the winner fires first.

**On blank paper** — build the playfield first:

1. Draw one straight line all the way across the page, through the exact center.
   This is the **fold axis**, not a target; centering it keeps both halves equal.
2. If the line is tilted, fold along it and shade any area that hangs past the other
   half. Those are the **no-play zones** — out of play for both players.
3. Then pick two colors, draw the matching shapes, and Rock Paper Scissors as above.

### Gameplay (one shot per turn, alternating)

1. Mark **one dot** anywhere on your own half — even on top of your own shapes. Small
   enough to stay challenging, big enough to transfer ink. Never in a no-play zone.
2. Fold the page along the line, find your dot from the back, press flat, and draw
   over it so the mark transfers onto your opponent's half.
3. Unfold and check. If any part of the mark shows inside one of your opponent's
   shapes, that shape is **hit**. Otherwise, it's a miss.
4. Alternate turns until one player's shapes are all hit — the **last player with
   shapes standing wins!**

### Rules

- Keep the page flat on the table during the drawing phase.
- No measuring tools of any kind — and no using your pen to gauge distance.
- No folding until your dot is fully committed to the page.
- Dots may never be placed in a no-play zone.
- The fold line is only the fold axis — shapes are the only targets.
- Contested shot? A neutral third party calls it; if none, your opponent calls it — be fair.
- Studying the dots already on the page to judge your aim is fair game.

> The whole page is open — both players see every shape on both halves. The
> challenge is eyeballing where your dot will land once the page is folded, with no
> measuring allowed. As dots pile up they become aiming references that help both
> players equally, which makes going first a slight disadvantage.

## Run / edit it locally

It's one file. Either:

- **Just open it** — double-click `index.html` (or drag it into a browser). Everything
  works from `file://`, including the PDF download.
- **Or serve it** (nice for editing, gives clean share URLs):
  ```sh
  python3 -m http.server 8000
  # then open http://localhost:8000
  ```

To change the game, edit `index.html` directly — the geometry, the seed→angle
mapping, the on-screen SVG, the PDF output, and the rules text all live in the
`<script>` at the bottom of the file.

## Deploy it yourself

Host `index.html` on any static host and it just works:

- **Your own site** — drop it in a folder named `fold-to-fire` so it serves at
  `yoursite.com/fold-to-fire`.
- **GitHub Pages** — enable Pages for this repo (Settings → Pages → deploy from
  `main`) and it'll be live at `https://<user>.github.io/fold-to-fire`.
- **Netlify / Vercel / Cloudflare Pages** — drag-and-drop or connect the repo.

## How the board works (the math)

A fold line through the board's center always splits the sheet into two equal-area
halves at any angle. Folding maps a dot to its **reflection** across that line, so a
target is only reachable where that reflection lands back on the sheet. The no-play
zone is therefore everything in `board \ reflect(board)` — the corners the fold can't
carry a mark into. That's what the grey ✕ grid marks.

## License

[MIT](LICENSE) — free to use, copy, modify, and share. Made with love by Travis Flesher.
