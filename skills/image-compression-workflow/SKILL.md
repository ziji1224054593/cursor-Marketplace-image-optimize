---
name: image-compression-workflow
description: Use rv-image-optimize CLI for safe single-file or batch image optimization with structured results.
---

# Image compression workflow

## Trigger

Use this skill when the user wants to:

- compress one image
- optimize a folder of images
- convert image formats
- prepare images for upload
- decide how to integrate `rv-image-optimize` into a project

## Required inputs

- Input path: one file or one directory
- Output directory, if the user wants files written to disk
- Target format and quality, if specified
- Whether replacing or deleting originals is allowed

## Workflow

1. Check whether the package is available in the current project or globally.
2. Prefer `npx rv-image-optimize` when the package is installed in the current project.
3. If the global command is available, `rv-image-optimize` is an acceptable fallback.
4. Prefer the CLI with `--json` so the result is machine-readable.
5. Default to a safe output directory instead of overwriting originals.
6. Inspect `isEffective`, `savedSize`, or `savedPercentage` before recommending replacement of the original.
7. If the user asks for integration help, choose the right entry:
   - React runtime: `rv-image-optimize`
   - Vue or vanilla JS runtime: `rv-image-optimize/utils-only`
   - Vite build stage: `rv-image-optimize/vite-plugin`
   - Webpack build stage: `rv-image-optimize/webpack-plugin`
   - Node scripts: `rv-image-optimize/node-compress`
8. Summarize the result with success count, failure count, output path, and any follow-up action.

## Guardrails

- Do not delete or replace originals unless the user explicitly approves it.
- Do not invent CLI flags; use the official package behavior.
- Keep the plugin focused on orchestration and guidance, not reimplementing compression logic.
- Call out clearly when compression succeeded technically but was not effective for file size.
- Explain that already compressed formats such as `webp` and `jpeg` may become larger after recompression.
