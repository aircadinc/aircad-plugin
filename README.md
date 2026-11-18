# Aircad

Draft and model in [Aircad](https://aircad.com), online CAD for 2D drafting
and 3D modeling, from a conversation with your assistant. The plugin connects
the Aircad MCP server and adds skills for modeling, drawing sets, and
reusable commands.

Aircad opens and saves DWG and DXF drawings with their layouts, blocks, and
dimensions; imports and exports STEP, Rhino 3DM, glTF and GLB, STL, and OBJ;
imports SVG; and exports drawing sets to PDF. Your assistant works on any
drawing open in Aircad, whichever format it came from.

It works in Claude (chat, Cowork, and Claude Code), ChatGPT and Codex,
Antigravity, and Gemini CLI.

## Install

In the Claude and ChatGPT apps, add Aircad from the plugin directory. From a
terminal:

```
# Claude Code
/plugin install aircad --marketplace aircadinc/aircad-plugin

# Gemini CLI
gemini extensions install https://github.com/aircadinc/aircad-plugin

# Antigravity CLI
agy plugin install https://github.com/aircadinc/aircad-plugin
```

Any other MCP client can connect to the server directly at
`https://mcp.aircad.com/mcp`.

## Use it

1. Install the plugin and connect Aircad. You sign in with your Aircad
   account; no server address or key to paste.
2. Open a file in Aircad, in a browser tab or the desktop app.
3. Ask for what you need: "What's in this drawing?", "Model a steel base
   plate with four bolt holes", "Make a layout with plan and front views at
   1:20", "Make a command that draws a slot from two points".

The first time an assistant works on a file, Aircad asks you to allow it.
Every change arrives as a draft, tinted on the canvas, and lands only when
you apply it in Aircad, unless you turn on Auto-apply file edits for that
assistant. The assistant can list, open, create, and fork your files, but it
can't delete, rename, move, or share them.

## Skills

- **model-in-aircad**: build a 3D model from a description, sketch, or
  reference image, with repeated parts as blocks and a check from two views.
- **drawing-set**: layouts, viewports at a drawing scale, sections,
  dimensions, notes, and a title block.
- **write-a-command**: save a command with inputs and a preview, then try it
  on the command line.

## Data

The assistant reaches only the files you allow, through `mcp.aircad.com`,
while they are open in Aircad. What it reads and writes there is sent to the
assistant you use, under that assistant's terms. The plugin itself is
Markdown and JSON: it stores nothing and sends nothing on its own. See the
[privacy policy](https://aircad.com/privacy) and the
[assistants guide](https://aircad.com/docs/assistants), which also covers
disconnecting an assistant.

## Support

[aircad.com/docs/assistants](https://aircad.com/docs/assistants), or report
a problem from the app menu in Aircad (Shift+Cmd+B, or Shift+Ctrl+B).

## License

MIT
