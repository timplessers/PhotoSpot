# PhotoSpot — Domain Glossary

PhotoSpot is a single-page browser tool for pinning photos onto an existing PDF, so
that a reader in Adobe Reader can click a pin to reveal the photo and click again to
hide it.

This file defines the project's vocabulary. It is a glossary, not a spec: no
implementation details, no decisions, no TODOs.

## Spot

A single placed photo: one **Image**, at one position, on one page of the **Base
PDF**. A Spot is the atomic unit of the whole tool — created by dropping an Image
onto a page, moved by dragging, destroyed by dragging it off the page.

A Spot carries a **Spot number**, unique across the document, used to refer to it in
conversation and in print.

In the editor a Spot appears as a blue photo icon. In the **Export** it becomes three
things at once: that same icon painted on the page, a **Layer** holding the photo, and
a clickable region that toggles the Layer.

Two Spots may share one Image. An Image is never consumed by being placed.

## Base PDF

The PDF the user starts from. PhotoSpot never alters its existing content — no text is
removed, replaced or covered. Spots are added on top of it; everything already on the
page survives into the Export untouched.

(This is the difference from the earlier `foto_toggle_tool.html`, which searched the
page for filename-like text and deleted those glyphs. That behaviour is not part of
PhotoSpot.)

## Image

A photo the user has added to the tool, listed in the **Image list**. An Image is
identified to the user by its filename and thumbnail. It exists independently of
whether it has been placed: adding an Image does not create a Spot.

## Image list

The right-hand panel: every Image the user has added, in natural filename order. It is
the source of drags that create Spots, and the destination of drags that destroy them.

## Overlay

What a reader sees after clicking a Spot's icon in the exported PDF: a white card
showing the photo, with a close button, centred on the Spot that opened it and pushed
inwards where that would run off the page. At most one Overlay is open per page —
revealing one Spot's photo hides any other on that page.

## Layer

An Optional Content Group in the exported PDF — the PDF-native mechanism that lets
content be shown and hidden. Each Spot owns exactly one Layer, containing that Spot's
Overlay. A Layer starts hidden.

## Export

The act of producing a new PDF from the Base PDF plus every Spot. The Base PDF on disk
is never modified; the Export is a separate downloaded file.

## Session

Everything the user currently has loaded: one Base PDF, the Image list, and the Spots
placed so far. A Session is not a saved document — it lives only in the open page.
