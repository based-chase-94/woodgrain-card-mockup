# Folding Card Mockup

Open `index.html` in any browser. No build step, no server needed.

A top-fold card: 4.75 in wide × 3.5 in tall folded, printed on one 4.75 × 7 in sheet
with a single fold across the middle.

## Artwork

| Face | File |
|---|---|
| Front cover (outside) | `images/wg-card-updated_01.jpg` |
| Back (outside) | `images/wg-card-updated_02.jpg` |
| Inside top | *blank white* |
| Inside bottom | *blank white* |

`_01` is the panel that was exported upside down, i.e. the top half of the press
sheet, which on a top-fold card is the front cover. If that pairing is backwards,
swap the two filenames in the `ART` block and flip `FRONT_COVER_IS_PRESS_ORIENTED`.

The two placeholder SVGs are still in `images/` if they're ever useful again.

## Swapping the artwork

Edit the `ART` block at the top of the `<script>` in `index.html`:

```js
const ART = {
  frontCover:   'images/wg-card-updated_01.jpg',
  frontBack:    'images/wg-card-updated_02.jpg',
  insideTop:    '',      // '' = blank white
  insideBottom: '',
};

const FRONT_COVER_IS_PRESS_ORIENTED = true;
```

Drop new files in `images/` and point these at them. Any format the browser reads
works (jpg, png, svg, webp). Setting a value to `''` leaves that face blank white,
which is how the interior is set up now — if the inside ever gets art, just fill
those two in.

`FRONT_COVER_IS_PRESS_ORIENTED` says whether the front cover file is *already*
rotated 180° the way it prints on the sheet. It's `true` now because
`wg-card-updated_01.jpg` came off the imposed sheet that way. Set it to `false` if a
future export reads right side up the way the finished card does. Either way the
mockup shows the cover right side up when the card is folded.

## How the fold works

The card turns about a horizontal crease, so the top half folds *down and forward*
over the bottom half. That is why the front cover prints upside down on the press
sheet — folding it over turns it right side up. The reference print-file diagram
from the printer shows the same thing.

That also means the cover's reverse is flipped top-to-bottom rather than
left-to-right, which is why `#pCover .face.back` uses `rotateX(180deg)` while the
base panel uses the ordinary `rotateY(180deg)`.

Artwork is 4.75 in × 3.5 in per panel. The current files are 1698 × 1243 px, an aspect
ratio a hair wider than 4.75 : 3.5, so the mockup crops a sliver off the sides
(`object-fit: cover`). For print, 1425 × 1050 px is 300 dpi at trim size, plus whatever
bleed the printer wants.

## Controls

- **Slide to open / close** — scrub the fold from flat open to fully closed
- **Closed / Half open / Fully open** — animated presets
- **Flip over** — spin to the other side
- **Labels** — face name overlays
- **Press sheet** — flat imposition view of both sides of the sheet with the fold line
- **Drag** to rotate, **scroll** to zoom. The view auto-fits and re-centres on whatever
  the fold is currently showing, so nothing runs off the edge of the frame.

The slider deliberately sits on its own row rather than at the very top of the page:
Arc keeps a window-drag strip along the top edge of the web view, and a control up
there drags the browser window instead of the handle.

## Search visibility

`robots.txt` disallows all crawlers and the page carries a `noindex, nofollow` meta
tag. Neither makes the site private — anyone with the URL can open it. They only keep
it out of search results.

The mockup is view-only — there's no way for a viewer to alter the artwork from the page.
