---
name: drawing-set
description: Make drawings of a model in Aircad - layouts with plan, elevation, and section views at a scale, dimensions and notes, and a title block - and check them for printing. Use when the user asks for a drawing set, sheets, a layout, shop drawings, construction documents, a plan or section on paper, or to get a model ready to print or send.
---

# Drawing sets in Aircad

A drawing set is one layout per sheet. Each layout holds a title block,
viewports that look into the model at a stated scale, and the dimensions
and notes that explain it. Work in this order.

## 1. Agree on the set

Call `file_brief` and look at the model's extents, its units, the layouts
that already exist, and the blocks (a title block may already be there).
Then settle with the user, in one short question if they haven't said:

- the paper size and orientation (A3 or A1 landscape, 11x17 or 24x36),
- the sheets and what each shows (plans per floor, elevations, sections,
  details),
- the scale of each view, or let you pick standard ones that fit.

Pick scales the trade uses: 1:50, 1:100, 1:200 or 1/4" = 1'-0", 1/8" = 1'-0"
for buildings; 1:1, 1:2, 1:5 for parts. Work out whether each view fits its
viewport at that scale from the extents before you build, and say so when a
view needs a larger sheet or a smaller scale.

## 2. Cuts before views

For plans and sections, place the section entities in the model space
first, and check each cut with `cad.doc.sectionCut` in a `run_query_script`:
a plan cut should pass through the walls of its floor, a section through
the part of the model it is meant to explain. Name sections the way the
sheets will cite them.

## 3. Build the sheets in one script

Write one `run_edit_script` that, for each sheet, adds the layout
(`cad.doc.spaces.addSheet`), places the title block, and adds each viewport
with its view direction and drawing scale, framed on its own part of the
model. Leave room for the view title under each viewport and keep
everything inside the layout's margins. Put the sheet number and title in
the title block's attributes when it has them.

If the file has no title block and the user has none to give you, draw a
simple one on the layout (a border, a title strip with the project, sheet
title, sheet number, scale, and date) and say so; offer to make it a block
so every sheet shares it. The Libraries panel (`cad.editor.show`) may offer
one the user can add.

## 4. Dimensions and notes

Dimension what someone builds from: overall sizes, then the positions of
openings, holes, or grid lines, then the details. Annotation is annotative,
so size text and dimensions for paper and they read the same at every
scale. Add a view title with its scale under each viewport. Don't dimension
the same thing twice across sheets.

## 5. Check it like a print

Open each layout with a short `run_query_script` (`cad.editor.setActiveSpace`
changes only what the user sees, not the file, and doesn't replace your
draft), take a `screenshot`, and look for: views clipped by their viewport,
text overlapping geometry or other text, dimensions inside the model's
lines, empty or crowded sheets, and anything over the margins. Fix it in a
new version of the whole script.

## 6. Report

List the sheets with what each shows and its scale, and anything you
assumed (a paper size, a cut height). When the draft is waiting, say it's
waiting for them to apply in Aircad.

For how layouts, viewports, and print preview work in the editor, call
`docs_search` and link the page.
