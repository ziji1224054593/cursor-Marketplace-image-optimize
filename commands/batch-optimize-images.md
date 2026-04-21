---
name: batch-optimize-images
description: Optimize a folder of images with rv-image-optimize and summarize the result.
---

Use `rv-image-optimize` to optimize a user-provided image folder.

Requirements:

- Prefer `npx rv-image-optimize` when the package exists in the current project
- Fall back to `rv-image-optimize` only when the global command is available
- Prefer `--json` output
- Default to a separate output directory
- Report the number of successful and failed files
- Highlight files where compression completed but `isEffective` is false
- Do not delete or replace originals unless the user explicitly asks for it
