# PhotoSpot — place photos on a PDF as clickable Layers

Status: ready-for-agent
Date: 2026-09-11 (revised 2026-09-12)
Related: [ADR-0001](../adr/0001-ocg-layers-toggled-by-annotation-javascript.md), [CONTEXT.md](../../CONTEXT.md)

## Problem Statement

I produce reports, checklists and site plans as PDFs, and I have a folder of photos
that belong to specific places in those documents. Today the photos travel as a
separate folder or as a long appendix, and the reader has to work out for themselves
which photo belongs to which paragraph, room or detail on the plan.

The previous tool solved half of this, but only if I first edited the source document
so that every photo's exact filename appeared as text at the right spot. That means
the document has to be prepared for the tool before the tool can help, and a typo in a
filename silently produces nothing. I want to work the other way round: take the PDF as
it is, and point at the places myself.

I also do not want the photos to be visible all the time. A report with thirty photos
pasted into it is unreadable and unprintable. The reader should see a clean document,
and open a photo only when they want it.

## Solution

A single HTML file I open in my browser. Nothing to install, nothing uploaded anywhere.

The left three quarters of the window is the PDF: I drop a document there (or click to
pick one) and it fills the pane, scrolling continuously through every page. The right
quarter is the **Image list**: I drop photos or a whole folder there, or pick them with
two buttons, and they appear as a sorted list with thumbnails.

I drag a photo out of the list and drop it on the page, exactly where it belongs. A
small blue photo icon — a **Spot** — appears at that point. I can drag it somewhere
else, drop the same photo in a second place, or drag a Spot back onto the Image list to
delete it. Every Spot carries a number so I can talk about "photo 7".

When I press **PDF exporteren** I get a new PDF in my downloads folder. The original is
untouched. In Adobe Reader the document looks exactly like the original plus a scatter
of small blue icons; clicking one opens the photo, big and centred on the page, with a
close button. Clicking the icon again, or the close button, puts it away. Only one
photo is open per page at a time, so the document never turns into a pile of cards.

## User Stories

### Loading a document

1. As a report author, I want to drop a PDF onto the left pane, so that I can start
   placing photos without going through a file dialog.
2. As a report author, I want to click the same pane to open a file picker, so that I
   can work without dragging when the file is buried in a folder tree.
3. As a report author, I want the document to fill the width of the pane by default, so
   that I can see where things are without adjusting anything first.
4. As a report author, I want to scroll continuously through every page, so that a
   forty-page inspection report is one gesture rather than forty.
5. As a report author, I want to zoom in and out, and back to fit-width or fit-page, so
   that I can place a Spot precisely on a small detail of a site plan.
6. As a report author, I want to type a page number and jump there, so that I do not
   have to scroll through a long document to reach page 31.
7. As a report author, I want pages to keep their position on screen when I zoom, so
   that I do not lose my place.
8. As a report author, I want to be warned when a page of my PDF is rotated, so that I
   know to check that page in the export rather than discovering it later.
9. As a report author, I want to be told clearly when a PDF cannot be opened, so that I
   do not sit waiting for something that will never load.
10. As a report author, I want to load a different PDF without reloading the page, so
    that I can move on to the next document in a batch.
11. As a report author, I want to be asked to confirm before a new PDF wipes the Spots I
    have already placed, so that a mis-drop does not destroy an afternoon of work.

### Building the Image list

12. As a report author, I want to drop a folder of photos onto the right panel, so that
    I can bring in a whole shoot in one gesture.
13. As a report author, I want folders inside that folder to be included too, so that a
    shoot organised by room still arrives complete.
14. As a report author, I want a button to pick individual photos, so that I can add a
    few files from different places.
15. As a report author, I want a button to pick a whole directory, so that I can add a
    folder without dragging it.
16. As a report author, I want non-image files to be ignored silently, so that dropping
    a folder containing a spreadsheet does not produce an error.
17. As a report author, I want my photos listed in natural filename order, so that
    IMG_2 comes before IMG_10 as a human would expect.
18. As a report author, I want a thumbnail on every row, so that I can pick the right
    photo without opening them one by one.
19. As a report author, I want photos taken in portrait to appear upright, so that I am
    not choosing between sideways thumbnails.
20. As a report author, I want to be told when I add a photo that is already in the
    list, so that I do not end up with the same image twice.
21. As a report author, I want HEIC photos from my phone to work, so that I do not have
    to convert a folder before I can start.
22. As a report author, I want to see that a HEIC photo is still being converted, so
    that I know why I cannot drag it yet.
22b. As a report author, I want the other photos to stay usable while a HEIC converts,
    so that one slow format does not hold up the rest.
23. As a report author, I want the interface to stay responsive while HEIC photos are
    converting, so that I can carry on placing the photos that are ready.
24. As a report author, I want to remove a photo from the list, so that I can tidy up
    photos I am not going to use.
25. As a report author, I want to be warned when the photo I am removing is already
    placed, so that I do not delete Spots by accident.

### Placing Spots

26. As a report author, I want to drag a photo from the list onto the page, so that I
    can mark exactly where it belongs.
27. As a report author, I want the icon to land where my cursor was, so that placing it
    on a small detail is accurate.
28. As a report author, I want to see the photo's thumbnail following my cursor while I
    drag, so that I know which photo I am about to place.
28b. As a report author, I want the blue icon under my cursor while I drag, with the
    photo beside it, so that I can see exactly where the Spot will land as well as which
    photo it carries — when placing a new one and when moving one already placed.
28c. As a report author, I want a Spot dropped inside a table row to sit centred between
    that row's lines, so that a page full of Spots looks deliberate rather than
    hand-placed.
28d. As a report author, I want to see the line it is going to snap to before I let go,
    so that I am not guessing.
28e. As a report author, I want to switch snapping off, so that I can put a Spot exactly
    where I want it on a page where the guessing goes wrong.
29. As a report author, I want the document to scroll while I drag towards the top or
    bottom edge, so that I can place a photo on a page that was not on screen when I
    started.
30. As a report author, I want to drag a placed Spot to a new position, so that I can
    correct a placement without deleting and redoing it.
31. As a report author, I want to drag a Spot to a different page, so that I can fix a
    placement I made on the wrong page.
32. As a report author, I want to drag a Spot onto the Image list to delete it, so that
    removing a mistake is one gesture.
33. As a report author, I want a drag that ends outside the window to leave the Spot
    where it was, so that a slip of the hand costs nothing.
34. As a report author, I want to place the same photo in several places, so that one
    detail photo can be referenced from more than one point on a plan.
35. As a report author, I want to see how many times each photo has been placed, so
    that I can check I have not forgotten one.
36. As a report author, I want every Spot numbered, so that I can refer to "photo 12"
    in the report text.
37. As a report author, I want the numbers to stay contiguous after I delete a Spot, so
    that the exported document has no unexplained gaps.
38. As a report author, I want to be warned when two Spots sit almost on top of each
    other, so that I do not ship a document where one of them cannot be clicked.
39. As a report author, I want the Spots to stay in place when I zoom or scroll, so
    that the editor always shows me the truth about where they are.
40. As a report author, I want to be warned before closing the tab with Spots placed,
    so that I do not lose them to a stray keystroke.

### Exporting

41. As a report author, I want a single Export button, so that finishing is obvious.
42. As a report author, I want the button disabled until there is something to export,
    so that I cannot produce a pointless copy of my own document.
43. As a report author, I want to choose the photo quality, so that I can trade file
    size against detail depending on who the document is going to.
44. As a report author, I want a sensible default quality, so that I do not have to
    think about it for the common case.
45. As a report author, I want photos downscaled by default, so that a document with
    thirty phone photos does not become a file nobody can email.
46. As a report author, I want a progress indication during export, so that I know a
    long export has not hung.
47. As a report author, I want one clear summary when the export finishes, so that I
    know what it contained without reading a log.
48. As a report author, I want one broken photo to be skipped and reported rather than
    aborting the export, so that a single corrupt file does not cost me the whole run.
49. As a report author, I want the exported file named after the original, so that I can
    tell the two apart in my downloads folder.
50. As a report author, I want the original PDF left untouched on disk, so that I can
    export again after a correction.
51. As a report author, I want a photo used by several Spots stored once, so that
    reusing a photo does not multiply the file size.

### Reading the exported document

52. As a report reader, I want the document to look normal, so that I can read it
    without visual clutter.
53. As a report reader, I want to click a blue icon to see the photo it refers to, so
    that I do not have to search an appendix.
54. As a report reader, I want the photo shown large and centred on the icon I clicked,
    so that it appears where I am already looking and I can see the detail it was taken
    for.
55. As a report reader, I want a close button on the photo, so that I can put it away
    and carry on reading.
56. As a report reader, I want clicking the icon again to close the photo, so that the
    obvious gesture works.
57. As a report reader, I want opening a photo to close the one already open on that
    page, so that the page never fills up with overlapping cards.
58. As a report reader, I want every photo hidden when I open the document, so that I
    start from a clean page.
59. As a report reader, I want the photos listed under one entry in the Layers panel, so
    that I can still reach a photo manually if a click does not work.
60. As a report author, I want to know that this only works in Adobe Reader and
    Acrobat, so that I can tell recipients what to open it with.
61. As a report reader, I want an opened photo to fit the window I am reading in, so
    that I can see all of it without zooming out.
61b. As a report reader, I want the document to stay exactly where it is when I open a
    photo, so that nothing jumps under my hands.
61c. As a report author, I want to see who made the tool, under what licence, and on
    what it is built, so that I can pass it on with confidence.
62. As a report author, I want to see which version of the tool I am using, so that I
    can say which one produced a given document.
63. As a report author, I want the licence to be visible in the tool itself, so that
    anyone I pass it to knows what they may do with it.

## Implementation Decisions

### Shape of the thing

- **One HTML file, opened directly from disk.** No build step, no server, no install.
  Libraries load from cdnjs: pdf.js 3.11.174 for rendering and pdf-lib 1.17.1 for
  writing. Both are pinned, and both are classic scripts — pdf.js 4 and later are
  ESM-only and cannot be loaded this way. Internet access is required at load.
- **Chrome and Edge are the target.** Nothing may break outright in Safari or Firefox
  except directory picking, which is Chromium-only.
- **Dutch interface, English code and comments.**

### Session state

- A **Session** is one **Base PDF**, an **Image list**, and the **Spots** placed so far.
  It lives in memory only; there is no persistence and no save file.
- A **Spot** holds a page index and a position in PDF user space (points, origin at the
  bottom-left of the page) — never screen pixels. Zoom and scroll are then presentation
  concerns, and **Export** needs no coordinate conversion at all.
- **Spot** numbering is global across the document, assigned in placement order, and
  renumbered to stay contiguous whenever one is deleted.
- An **Image** is independent of whether it has been placed: placing does not consume
  it, and one Image may back any number of Spots.
- Destructive transitions are confirmed, never silent: loading a new Base PDF over
  existing Spots, and removing an Image that has Spots (which deletes those Spots with
  it, since an orphaned Spot would fail at export).
- There is no undo. Deletion therefore requires aiming at the Image list; a drag
  released anywhere else — including outside the window — returns the Spot to where it
  was.

### Viewer

- Continuous vertical scroll of all pages; fit-to-width is the default, with explicit
  zoom in/out, fit-width, fit-page, and ctrl+scroll.
- Pages render lazily as they approach the viewport and re-render on zoom change;
  canvases far outside the viewport are released so a long document at high zoom does
  not accumulate every page it has ever shown.
- Page rendering uses the device pixel ratio, capped, so text stays sharp on a retina
  display without quadrupling memory.
- Page rotation and a non-zero CropBox origin are **not** compensated for. Rotation is
  detected on load and reported in a banner, because the failure is otherwise silent and
  visibly wrong. Encrypted PDFs are not handled beyond reporting that the file would not
  open.

### Spots in the editor

- The icon is 8 PDF points square; on screen it scales with zoom but never renders
  smaller than a usable click target.
- The drop point is the icon's **centre**.
- Spots closer than 20 points to each other on the same page are flagged, in the editor
  and on export, because in the exported PDF only one of two overlapping hotspots is
  reachable. Overlap is allowed — it is sometimes deliberate — but never silent.
- Both gestures (list → page, and moving or deleting a Spot) are one pointer-driven
  mechanism, which is what allows edge autoscroll and a drag ghost. The delete target is
  the whole Image-list panel, which turns red while a Spot is being dragged.
- The drag ghost is the blue icon centred on the pointer — where the Spot will land —
  with the photo's thumbnail beside it on the same line. Both parts are positioned around
  the pointer rather than laid out in a row: in a row the height is the photo's, and the
  icon drifts half a thumbnail below the cursor. The same ghost serves placing a new Spot
  and moving an existing one: the question being answered is the same.

### Snapping between rules

- A Spot dropped between two horizontal rules is centred between them. Only the vertical
  position is snapped; horizontal placement is left alone.
- The rules are found by reading the **rendered page**, not the PDF's drawing operators:
  a row of canvas pixels more than half full of ink is a rule. This reads the page the
  way the user sees it — a table drawn with vector strokes and a scanned form both come
  out as dark rows, and only the first of those has operators to inspect. The page canvas
  is already on screen during a drag, so it costs one read, cached per page and zoom.
- A run of inked rows thicker than ~1% of the page height is a filled band (a shaded
  header, a photo), not a rule, and is discarded. Pairs closer than 9 pt or further apart
  than 170 pt do not snap either: the first is a hairline pair, the second a page border
  rather than a row.
- While a snap is live a dashed guide is drawn at the target line, so the user sees where
  the Spot will land before letting go. Snapping is on by default and can be switched off
  from the toolbar.

### File drops

- Drops are accepted at the window in the capture phase, not on each zone, and the drag
  is accepted unconditionally. A drag must be accepted during `dragover` or the browser
  navigates to the dropped file and replaces the editor; deciding that from
  `dataTransfer.types` means trusting every browser to describe a file drag identically.
  Window-level capture also means a drop that lands slightly off — on the toolbar, in
  the gutter beside a page, on the warning banner — still does what it obviously meant.
- The pane under the cursor decides what a drop means, but the routing is forgiving: a
  PDF loads wherever it lands, and photos dropped on the document still reach the Image
  list, with a message saying so. A drop that yields nothing usable says that too,
  rather than failing silently.
- `dataTransfer.files` is used directly for plain file drops; the FileSystemEntry tree
  is walked only when a directory is actually among the dropped items. Entries are taken
  out of the DataTransfer synchronously, since it is emptied as soon as the handler
  yields.
- Spots move on pointer events, never HTML5 drag-and-drop, so the two mechanisms cannot
  be confused with one another.

### Image pipeline

- EXIF orientation is applied on decode — for thumbnails and for export — or a large
  share of phone photos arrive on their side.
- HEIC has no native decoder in Chrome. `heic2any` (libheif compiled to wasm, ~1.3 MB)
  is fetched only when a HEIC file is actually added, and runs in a Web Worker: a 12 MP
  decode takes seconds and would otherwise freeze the editor. A HEIC Image is not
  draggable until its conversion finishes; a failed conversion leaves a dead row that
  says why.
- **The worker cannot fetch that library itself.** A worker built from a blob URL has an
  opaque origin and `importScripts()` across origins is refused from there. The page may
  fetch it, so the source is fetched on the main thread and built into the worker.
- Two shims travel with it, because the library expects a browser: it touches `window`
  while loading and creates a `video` element to sniff codec support, and it converts its
  decoded pixels to a blob through a canvas — none of which a worker has. `window` maps
  to the worker's own global, and `document.createElement` returns an `OffscreenCanvas`
  carrying a `toBlob()` of its own for canvases, and an inert object for anything else.
- If the worker cannot be built at all, the decode falls back to the main thread with a
  warning that the page will stutter. A stuttering conversion beats none.
- Three quality modes: Original, High (max 1600 px, q0.85, the default), and Compact
  (max 900 px, q0.70). Re-encoded output is always JPEG, which flattens transparency —
  irrelevant for photographs, deliberate for anything else.
- Original embeds untouched bytes only where nothing needs baking in: a PNG, or a JPEG
  whose EXIF orientation flag is already upright. Anything else — a rotated JPEG, a
  HEIC, a WebP — is re-encoded at full resolution, because pdf-lib embeds only JPEG and
  PNG and ignores orientation entirely.
- Each Image is embedded into the output document once, however many Spots use it.

### Export

Governed by [ADR-0001](../adr/0001-ocg-layers-toggled-by-annotation-javascript.md).

- Each **Spot** owns one **Layer** (an Optional Content Group), created hidden: listed
  in `/OCProperties`, added to the default configuration's `/OFF` array, with
  `/BaseState` left as `ON`.
- A document that already carries layers is normalized rather than overwritten — any
  subset of `/OCProperties`, `/D`, `/ON`, `/OFF` may be missing, and pre-existing layers
  keep their place in the panel.
- Our Layers are grouped under one labelled entry ("Foto's") in `/D /Order`, so the
  Layers panel stays readable and still offers a manual fallback.
- Layer names are reduced to escape-free ASCII — diacritics folded, everything outside
  `[A-Za-z0-9 ._-]` replaced — and the same reduction is applied to the literal inside
  the toggle script, so the two can never drift apart. This is not cosmetic: an action
  script is written into the PDF as a literal string, and a reader must ignore any
  backslash escape it does not recognise, so a `\uXXXX` escape arrives at the JS engine
  with its backslash gone and the layer never matches its own name. An escaped quote
  breaks the script outright, and an unbalanced parenthesis corrupts the object. The
  cost is that accents are lost from the names shown in Acrobat's Layers panel.
- Two Link annotations per Spot. The icon hotspot (the icon rect plus 2 points) carries
  **no** `/OC`, so it stays clickable underneath an open card and can close it. The
  close button carries `/OC` tied to its own Layer, so it is inert while that photo is
  hidden.
- The icon's toggle script flips its own Layer and switches off every other Layer on the
  same page — one photo per page at a time. The close button's script only switches its
  own Layer off.
- Page content is written in two passes: every Spot's icon first, then every Spot's
  overlay. Interleaved, a later Spot's icon would paint over an earlier Spot's open
  photo.
- **Clicking a Spot shows the photo and moves nothing else.** Centring the card in the
  reader's window was tried twice — first as two statements inside the toggle script,
  which cost the whole feature (below), then safely as a `/GoTo` chained after it — and
  even working, it reads as the document jumping under your hands. Neither annotation
  carries a chained action: the click is the script and nothing more.
- **Nothing but the toggle goes in the toggle script.** Everything in one script shares
  one fate: the view move was first written as two extra statements inside it, and
  whatever Acrobat objected to there took the toggle down with it — clicking a Spot did
  nothing at all, in a document whose structure was provably correct. Anything a viewer
  might refuse belongs in a separate action that can fail on its own; the view move has
  since been dropped altogether. One test locks the script to the toggle and nothing
  else, another asserts that neither annotation carries a chained action.
- The **Overlay** card is **centred on the Spot that opened it**, not on the page, and
  slides inwards where that would run it off the paper. The reader has just clicked that
  point, so it is by definition what they are looking at — which is what puts the photo on
  screen, with no view to move and nothing jumping under their hands. A page-centred card
  cannot manage that: a PDF has no idea where the reader has scrolled to.
- It is sized against the part of the page a reader can see rather than against the
  paper: at most 55% of page width, and at most 70% of the band a fit-to-width window
  shows (taken as 0.62 × page width, capped at the page height). Sized against the page
  alone, a card fits the paper but overflows the screen, which is what makes a photo feel
  oversized. A photo's pixel dimensions have no bearing on this — the drawn size is set in
  points, so a 48 MP original occupies exactly the same paper as a 2 MP one. There is no
  cascade: with one photo open per page, there is nothing to cascade around.
- Nothing is drawn as text, so no font is embedded. Spot numbers are an editor aid and
  survive into the export only as part of the Layer name.
- Layers carry no `/Usage` print entry: Acrobat prints them as displayed. An open photo
  therefore prints.
- Output is `<original>-fotos.pdf`, downloaded as a blob. Per-Spot failures are skipped
  and counted; the export only aborts if nothing at all succeeded. Feedback is a
  progress bar during the run and a single summary message at the end — how many photos,
  into which file, how large, and how many were skipped. Per-Spot detail goes to the
  browser console, not to the interface.

### Identity and licensing

- The application is **Photo Spot**, version **1.0.0**. The icon, name and version sit at
  the top-left of the window, left of the loaded document's name, where they are always
  visible. Credit is split by contribution: Tim Plessers (concept), Grill With Docs
  (specificatie), Claude Code (implementatie).
- Apache License 2.0, copyright Steel Prisms. The repository carries `LICENSE` and
  `NOTICE` and the HTML file carries the standard licence header; in the interface the
  copyright is not repeated — below the export button sits an **About** link alone.
- About opens a centred modal dialog: icon, name and version; the three credits, one per
  line; a link to the Apache licence; the third-party libraries with their own licences
  (pdf.js — Apache 2.0, pdf-lib — MIT, heic2any — MIT); and "Made with ❤️ in Belgium". It
  closes on the close button, on Escape, and on a click outside it.

## Testing Decisions

**What makes a good test here.** Assert on what the user does and what the exported
document contains — never on the name or shape of an internal function. A test drives
the page the way a person does (pointer events on real elements, OS-level file drags)
and then inspects the artefact the way Adobe will (the PDF object graph). Nothing in the
production code exists to make testing easier: the tests reach everything through the
page's own UI, and the export is captured by intercepting the anchor click and fetching
the blob URL rather than through an export-to-memory hook.

**One seam.** Headless Chrome with remote debugging, loading the real `photospot.html`
from disk, driven over the DevTools protocol. The page is its own test fixture: pdf-lib
is already loaded there, so the exported bytes are re-parsed in the same page and the PDF
structural assertions live at the same seam as the interaction ones.

The alternative — extracting the export code into a node-testable module — was rejected:
it would split the single file that is the point of the tool.

**Coverage, by harness.** Five suites, 115 checks:

- **Editor and export, end to end (51).** Load; fit-width scale; natural sort;
  non-image files skipped; thumbnails; drop coordinates mapping to the expected PDF
  points; placed-count per row; one Image reused by several Spots; moves within and
  across pages; drag-to-list deletion with renumbering; a release outside the window
  leaving the Spot untouched; export button enablement. Then, on the real exported
  bytes: one Layer per Spot, all in `/OFF` with `/BaseState ON`; layer names containing
  no character that needs escaping; the script literal byte-identical to the layer name
  it must match; **the toggle script matching a pattern that is the toggle and nothing
  else**; no chained action on either annotation, so a click never scrolls
  the document, with the card's own geometry checked across page and photo
  orientations: inside the visible band unaided, centred on the Spot wherever there is
  room, and pushed fully back onto the paper for a Spot in a corner. Plus the chrome: brand top-left of the PDF name, the
  colophon reduced to an About link, and the About dialog's contents and alignment.
- **Snapping (15).** Against a generated PDF with rules at known positions: every rule
  located to within about a point; a drop off-centre in a row landing on the row's
  midpoint, and the same for a move; the guide appearing during the drag and gone after
  it; the ghost carrying both icon and photo with the icon centred on the pointer to
  within a pixel; snapping off leaving the drop exactly where it was put; a point not
  bracketed by two rules left alone.
- **HEIC (11).** Against a real HEIC file, through the app's own path: accepted into the
  list, shown as converting and not draggable while it is, the JPEG beside it usable
  meanwhile, converted, thumbnailed, placeable as a Spot, and present in the exported
  PDF as an image.
- **File drops (7).** A PDF landing on the viewer, on the toolbar just outside it, and
  on the photo panel; a photo landing on the panel and on the document; and the drag
  being accepted so the browser does not navigate away. Driven as real OS-level drags
  through the DevTools protocol, never as synthesised `DataTransfer` objects — a
  synthetic one returns null from `webkitGetAsEntry` and so silently exercises a
  different path than a user does.
- **Export structure, in node (31).** A mirror: it lifts the OCG helpers out of the HTML
  by slicing the file and drives them against a synthetic two-page document, checking
  `/OCProperties`, the grouped `/Order` entry, annotation rects, icons painted before
  overlays, original page content preserved, and card geometry across page and photo
  orientations. Because it re-implements the export loop rather than running it, it can
  drift from the real one — it already did once, which is why the script assertions were
  moved up to the browser seam. Treat it as a fast structural check, not as the seam.

**Where they live.** All five are in the session scratchpad, not in the repository. The
outstanding work is to commit them as a test suite with the fixtures they need (a ruled
PDF, a small JPEG, a real HEIC) and a single command to run them.

**What cannot be tested here.** Whether Adobe Reader actually executes the annotation
JavaScript. No automated check reaches that; it needs a person opening the export in
Acrobat. This is not a gap to be closed by more tests: it is the reason the toggle script
is held to a known-good shape by a pattern, and the reason anything a viewer might refuse
lives in a chained action rather than inside that script.

## Out of Scope

- **Editing the Base PDF's existing content.** No text is searched, removed, replaced or
  covered. The previous tool's placeholder-matching and content-stream rewriting is not
  part of PhotoSpot.
- **Round-trip editing.** An exported PDF cannot be re-opened to adjust its Spots.
- **Saving a Session.** No project file, no autosave, no resume after a refresh. This was
  considered and deliberately deferred.
- **Undo.**
- **Correcting page rotation or a CropBox offset.** Detected and warned about only.
- **Encrypted or password-protected PDFs.**
- **Non-Adobe viewers.** The photos will not open in Chrome's viewer, Firefox or
  Preview, and no fallback is attempted.
- **Captions, labels or any drawn text**, including drawing the Spot number into the
  page.
- **Offline use.** The libraries come from a CDN and are not inlined.
- **Touch and mobile layouts.**
- **Virtualised scrolling of the Image list.** Sessions are expected to run to roughly
  20-50 photos, and no more than a couple of hundred.

## Further Notes

An implementation already exists in `photospot.html` and passes all 115 checks described
above. This spec is the record of what was decided and why, not a description of unbuilt
work; treat any divergence between the two as a bug in whichever is easier to defend.

Two decisions are worth revisiting if experience argues against them:

- **Printing.** Layers print as displayed, so a reader who prints with a photo open gets
  that photo on the paper. Making photos never print is a `/Usage` dictionary and an
  `/AS` entry per Layer if this turns out to bite.
- **Session persistence.** Deferred, not rejected. Autosaving Spot coordinates and
  filenames to `localStorage` would make a refresh survivable; a sidecar JSON file would
  additionally let a layout be handed to a colleague.
- **The window estimate.** One number — a reader's window is assumed to be about 0.62 ×
  the page width — decides how large the Overlay card is, and so whether it lands fully on
  screen without the reader scrolling. It is a guess about how people read, not a
  measurement, and it is the first thing to adjust if photos come out too large or small.
