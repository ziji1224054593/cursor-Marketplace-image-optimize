# RV Image Optimize Cursor Plugin

This plugin brings `rv-image-optimize` into Cursor as a practical workflow for image compression, batch processing, upload preparation, and framework-aware integration guidance.

It is intentionally thin: the plugin does not reimplement the image engine. Instead, it teaches Cursor and agents to use the official `rv-image-optimize` package safely, consistently, and with structured output.

## Components

- `skills/image-compression-workflow`: guides safe single-file and batch optimization
- `rules/prefer-rv-image-optimize-cli`: makes agents prefer the official CLI and structured output
- `commands/batch-optimize-images`: batch image optimization workflow
- `commands/recommend-project-integration`: recommends the right runtime or build-time entry
- `commands/prepare-upload-pipeline`: prepares compression + upload automation steps
- `agents/image-optimization-orchestrator`: coordinates larger image optimization tasks

## Installation and availability

This plugin is saved under Cursor local plugins and is immediately available to Cursor.

The underlying package still needs to be available in one of these ways:

1. installed in the current project, so Cursor can run `npx rv-image-optimize`
2. installed globally, so `rv-image-optimize` is on `PATH`

Recommended package install:

```bash
npm install rv-image-optimize
```

If the package is not installed yet, `npx rv-image-optimize` can often fetch it on first run. That first execution may be slower and depends on network availability.

## Usage model

Prefer these execution patterns in order:

1. `npx rv-image-optimize`
2. `rv-image-optimize`

Prefer `--json` whenever the output will be summarized by Cursor or another agent.

## Validated behavior

The local workflow has been validated with a real `webp` file through:

```bash
npx rv-image-optimize "<input>" --output-dir "<output-dir>" --json
```

The command succeeded and produced structured output with fields such as `outputPath`, `compressedSize`, `savedPercentage`, and `isEffective`.

One important takeaway from the validation: compression is not always beneficial. For already efficient images, the output may become larger. Agents should check `isEffective` before recommending replacement of the original file.

### Why a `webp` or `jpeg` can become larger

This is expected in some cases.

- `webp` and `jpeg` are already compressed formats, so they often have little redundant data left to remove
- a recompression step may rebuild the file with different encoding decisions or container overhead
- as a result, the command can succeed technically while the final file becomes larger

So the correct decision rule is not "did the command run successfully", but "is `isEffective` true".

## Safety defaults

- write optimized files to a separate output directory by default
- never delete or replace originals without explicit approval
- prefer official package entry points over custom one-off scripts
- check `isEffective` before suggesting replacement of originals

## Marketplace direction

This local plugin is structured so it can be evolved into a Marketplace-ready plugin:

- valid `.cursor-plugin/plugin.json`
- focused scope
- documented components
- discoverable rules, skills, commands, and agents
- real execution path validated with `npx rv-image-optimize`

## Repository

Source project: https://github.com/ziji1224054593/Rv-image-optimize
