---
name: write-a-command
description: Make a reusable command in Aircad that the user can run again from the command line, with inputs they pick on the canvas, a live preview, and options. Use when the user asks for a command, a tool, a macro, or a way to repeat a drawing task ("make me a command that draws a slot", "I keep drawing these brackets"), or wants to change a command they have.
---

# Write a command in Aircad

A command is a small program saved in the file. It asks for its inputs the
way Aircad's own commands do (points that snap, typed lengths, picked
entities), shows a preview while the user picks, and makes its change when
they finish. You write it, save it with `save_command`, and the user tries
it. Read `references/making-commands.md` before you write one: it is the
guide to the manifest, inputs, options, previews, and saving, with two
whole examples.

## 1. Pin down what it does

Before writing, agree on:

- what the user picks or types each run (two points, a length, some
  entities): those are inputs,
- what stays the same between runs and has a default (a count, a mode, a
  toggle, a fixed list): those are options,
- what it makes or changes, on which layer, and what the preview shows.

When the user describes a one-off change, make the change with
`run_edit_script` instead and offer a command only if they'll repeat it.

## 2. Write and save it

Call `script_api_reference` if you haven't, and write the whole module. Ask
for each input in the order a person would pick them, and keep the preview
up to date with each pick. Then call `save_command` with the source.

A command that won't save says why in the result: a manifest that isn't
plain data, a capability missing, an input asked for that isn't declared.
Fix it and save again with the `scriptId` from the first result.

## 3. Have the user try it

Tell the user the command is saved in the file's Scripts panel, where they
can try it, and that Add to Command Line there puts it on the command line.
Ask them to try it on a real case and tell you what's off. Change it by
calling `save_command` again with the same `scriptId` and the whole
corrected source. Read the saved source with `cad.doc.scripts.list()` in a
`run_query_script` before changing it, rather than from memory.

When the user asks how commands, aliases, or the command line work, call
`docs_search` and link the page.
