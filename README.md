# Photo Spot

Pin photos onto an existing PDF. The reader clicks a small icon on the page and the
photo appears over it; clicking again hides it.

Photo Spot is one HTML file. There is no server, no build step and no installation:
open `photospot.html` in a browser, drop in a PDF and some photos, and export a new PDF
with the photos embedded as clickable layers. The PDF you started from is never
modified — nothing on its pages is moved, covered or removed.

## Requirements

**The exported PDF must be read in Adobe Reader or Adobe Acrobat.** The show/hide
mechanism uses optional content groups driven by annotation JavaScript, which Chrome's
built-in viewer, Firefox and macOS Preview all ignore — they render the document
correctly, but clicking an icon does nothing and the photos stay hidden. This is a
deliberate trade-off, explained in [ADR-0001](docs/adr/0001-ocg-layers-toggled-by-annotation-javascript.md).

The editor itself runs in any modern browser. It loads pdf.js, pdf-lib and heic2any
from a public CDN, so the first open needs an internet connection.

The interface is in Dutch.

## Use it

1. Open `photospot.html` in a browser.
2. Drop a PDF onto the left-hand page view, or click to pick one.
3. Drop photos onto the right-hand panel, or a whole folder of them. JPEG, PNG and
   HEIC are the expected formats; anything else the browser can decode works too.
4. Drag a photo from the panel onto the page. That places a *spot*: a numbered icon at
   the point where you dropped it. Drag a spot to move it, drag it back to the panel to
   remove it. One photo can be placed as many times as you like.
5. Two settings shape the export. The **icon size** slider, beside the photo count,
   sets how large the spot icons print — its centre is the default size, its ends are
   half and double that, and the icons on the page resize as you drag it.
   **Fotokwaliteit**, at the foot of the panel, decides how far the photos are
   compressed on the way in.
6. Click **PDF exporteren**. The export downloads as a new file; the PDF you loaded is
   never written to.

Nothing you load is uploaded anywhere. Every PDF and photo stays in the browser tab,
and the export is produced locally.

Two conveniences worth knowing: **Uitlijnen** centres a dropped spot between the two
horizontal rules it lands between, which is what you want in a table; and a warning
appears if two spots sit so close that only one of them would be clickable in Reader.

## How the export works

Every spot becomes three things in the exported PDF: the icon painted onto the page, an
optional content group (a *layer*) holding the photo card, and two link annotations —
one over the icon, one over the card's close button — whose JavaScript switches that
layer on and off. Layers start hidden, so the document prints and reads exactly as it
did before anyone clicks. Opening a photo closes any other photo open on that page.

Because the layers are listed in Acrobat's Layers panel, a reader who cannot get a
click to work still has a manual way to reveal a photo.

## Repository

| Path | What it is |
| --- | --- |
| `photospot.html` | The tool. This is the whole program. |
| `foto_toggle_tool.html` | Its predecessor, kept for reference. It searched the page for filename-like text and replaced those glyphs; Photo Spot takes the PDF as it is. |
| `CONTEXT.md` | The project's vocabulary — spot, layer, overlay, base PDF. |
| `docs/specs/` | What was asked for, and why. |
| `docs/adr/` | Decisions that would be expensive to reverse. |

## Licence

Apache License 2.0 — see [LICENSE](LICENSE). Copyright 2026 Steel Prisms.

Photo Spot bundles no third-party code. The libraries it loads at runtime — pdf.js
(Apache 2.0), pdf-lib (MIT) and heic2any (MIT) — are listed in [NOTICE](NOTICE).
