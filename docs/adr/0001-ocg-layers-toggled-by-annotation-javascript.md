# 1. Photo visibility via Optional Content Groups toggled by annotation JavaScript

Date: 2026-09-11

## Status

Accepted

## Context

PhotoSpot must produce a PDF in which a reader clicks a small icon on the page and the
corresponding photo appears; clicking again — or clicking the card's close button —
hides it. The photo has to live inside the single exported PDF file, because these
documents are mailed around and printed, not served from anywhere.

PDF offers several mechanisms that could carry a hidden-then-revealed photo:

- **Optional Content Groups (OCGs, "Layers").** Page content marked with `/OC` whose
  visibility is controlled by the document's `/OCProperties`. A Link annotation with a
  `/JavaScript` action can flip an OCG's state at runtime via `this.getOCGs()`.
- **Popup / Text annotations with an image appearance.** Native to PDF, no JavaScript.
- **File attachment annotations.** The photo travels as an attached file that the
  reader opens in an external viewer.
- **Separate pages.** Each photo on its own page, reached by an internal link.
- **Form fields (button widgets) with image icons**, shown and hidden by setting
  field visibility from JavaScript.

The reader population is on Adobe Reader / Acrobat.

## Decision

Each Spot gets its own OCG. The photo, its card, and its close button are painted into
the page's content stream inside a `/OC /Name BDC … EMC` block bound to that OCG, which
starts hidden. Two Link annotations carry a `/JavaScript` action that toggles the OCG's
state: one over the Spot's icon, one over the close button.

Opening a Spot closes the other Spots on the same page: each Spot's script switches its
own layer on and its page siblings off.

## Consequences

The exported PDF is self-contained, and revealing a photo is a single click with no
dialog, no external application and no page navigation. Page content is untouched —
Spots are added on top of whatever the Base PDF already contains.

The cost is that **the mechanism only works in Adobe Reader and Acrobat.** Chrome's
built-in viewer, Firefox's pdf.js and macOS Preview all render the document correctly
but ignore annotation JavaScript, so clicking an icon does nothing and the photos stay
invisible. This is accepted deliberately: it is the only option of the five that
delivers in-place show/hide, and the readership uses Adobe.

Because OCGs are listed in Acrobat's Layers panel, a reader always has a manual
fallback if a click fails: the layers are grouped under one parent entry so the panel
stays legible.

Reversing this decision means rebuilding the export path end to end — the layer
creation, the content-stream marking, the annotations and their scripts are all
specific to this mechanism. Only the editor half of the tool would survive.
