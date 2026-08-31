# Folding Card Mockup

Open `index.html` in any browser. No build step, no server needed.

A top-fold card: 4.75 in wide × 3.5 in tall folded, printed on one 4.75 × 7 in sheet
with a single fold across the middle.

## Artwork

| Face | File |
|---|---|
| Front cover (outside) | `images/wg-card-front.jpg` |
| Back (outside) | `images/wg-card-updated_01.jpg` |
| Inside top | *blank white* |
| Inside bottom | *blank white* |

The two placeholder SVGs and the superseded `wg-folding-card_*` / `wg-card-updated_02`
exports are still in `images/`, unreferenced.

`wg-card-front.jpg` was supplied as a CMYK/GRACoL JPEG. It is converted to sRGB here
because browsers render CMYK JPEGs inconsistently (Firefox in particular) and every
other export in this folder is already sRGB. Use the original CMYK file for print —
this copy is for the web mockup only.

## Swapping the artwork

Edit the `ART` block at the top of the `<script>` in `index.html`:

```js
const ART = {
  frontCover:   'images/wg-card-front.jpg',
  frontBack:    'images/wg-card-updated_01.jpg',
  insideTop:    '',      // '' = blank white
  insideBottom: '',
};

const ROTATED_180 = {
  frontCover: false,
  frontBack:  true,
};
```

Drop new files in `images/` and point these at them. Any format the browser reads
works (jpg, png, svg, webp). Setting a value to `''` leaves that face blank white,
which is how the interior is set up now — if the inside ever gets art, just fill
those two in.

`ROTATED_180` marks a face whose *file* sits 180° off from the way the finished card
reads — usually because it was exported straight off the imposed press sheet, where
the front cover prints upside down. The mockup spins those back so the folded card
always reads right way up, and spins them the other way round for the press sheet
view, so both views stay correct whichever orientation a file arrives in.

The two current files disagree, which is why this is a flag per face rather than one
switch: `wg-card-front.jpg` reads right side up, while `wg-card-updated_01.jpg` was
exported for the top half of an earlier imposition and is upside down.

**Worth knowing for print:** that means neither file is currently in the orientation
its panel needs on the sheet — the cover has to be rotated 180° and the back has to be
rotated 180° before imposition. The press sheet view shows the target layout.

## How the fold works

The card turns about a horizontal crease, so the top half folds *down and forward*
over the bottom half. That is why the front cover prints upside down on the press
sheet — folding it over turns it right side up. The reference print-file diagram
from the printer shows the same thing.

That also means the cover's reverse is flipped top-to-bottom rather than
left-to-right, which is why `#pCover .face.back` uses `rotateX(180deg)` while the
base panel uses the ordinary `rotateY(180deg)`.

Artwork is 4.75 in × 3.5 in per panel. The current files are ~1698 × 1242 px, an aspect
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
