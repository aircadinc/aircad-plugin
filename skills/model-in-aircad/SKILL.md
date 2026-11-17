---
name: model-in-aircad
description: Build a 3D model in Aircad from a description, a sketch, a photo, or a reference image. Use when the user asks to model, build, or make something in 3D in Aircad (a part, a product, a piece of furniture, a structure, a building, a plant or site), or to turn a drawing or picture into a model.
---

# Model in Aircad

A good model here is the right size in the file's units, made of a few
named parts that repeat as blocks, and checked from more than one side.
Work in this order.

## 1. Read the file before drawing

Call `file_brief`. Note the model units, the grid and working area, the
layers, the blocks already in the file, and what is selected. Size the model
to the working area when the user gives no dimensions, and reuse a layer or
block that already fits rather than making a new one. If the file is empty
and the user hasn't said what they're making at what size, ask before you
build. Call `script_api_reference` before your first script.

## 2. Plan the parts and say the numbers

Break the object into parts the way someone would build it: a frame, its
legs, its panels; a column grid, its beams, its bracing. For each part,
decide its overall size and how many times it repeats.

From a reference image, read proportions, not pixels. Pick one dimension
you know or can reasonably assume (a door is about 2.1 m tall, a stair riser
about 180 mm, a pallet 1.2 m long) and scale the rest from it. Tell the user
which dimensions you read and which you estimated before or with the draft,
so they can correct them.

## 3. Build in one script, in parts

Write the change as one `run_edit_script`, with a function per part. Build
each repeated part once, make it a block named for what it is, and place
the rest as instances, as the server instructions describe. Put parts on
layers named for what they are when the file has none that fit. Use
`cad.ui.explain` to list the parts and the sizes you used.

Every `run_edit_script` replaces the draft still waiting in the file. So
unless the user has turned on Auto-apply file edits, don't split the model
across several scripts and expect them to add up: either build it all in one
script, or stop after each part and ask the user to apply it before the
next. For a large model, building it part by part with the user applying
each step is often clearer for them anyway.

## 4. Check it from two sides

After the draft is on the canvas, look at it before you report. Turn the
view with a short `run_query_script` that calls `cad.editor.setView` and
`cad.editor.fit`, then take a `screenshot`; do it again from a second
direction. A perspective and a front or side view catch most mistakes. Turn
the view from a query script, not an edit script: a new `run_edit_script`
would replace the draft you're checking. End on a view that shows the whole
model. Fix what is wrong (a part
floating above another, a part through a wall, a block placed at the wrong
base point) with a new version of the whole script.

Measure what matters with `run_query_script` rather than judging from the
picture: overall extents, the gap between parts that should touch, the count
of each block's instances.

## 5. Report

Say in two or three sentences what you built, its overall size, and what you
estimated. If the draft is waiting, say it's waiting for them to apply in
Aircad.

When the user asks how a command or feature works while you model, call
`docs_search` and link the page.
