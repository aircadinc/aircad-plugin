# Aircad

This extension connects the Aircad MCP server (`https://mcp.aircad.com/mcp`),
which works on the files the user has open in Aircad. Its server
instructions explain sessions, drafts, and the script API; follow them.

For longer workflows, read the skill that fits the request:

- `skills/model-in-aircad/SKILL.md`: building a 3D model from a description,
  sketch, or reference image.
- `skills/drawing-set/SKILL.md`: layouts, viewports, sections, dimensions,
  and title blocks.
- `skills/write-a-command/SKILL.md`: a reusable command the user can run
  again.

When the user asks how to do something in Aircad, call `docs_search` and
answer from the page it returns.
