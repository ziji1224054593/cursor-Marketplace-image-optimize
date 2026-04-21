---
name: prepare-upload-pipeline
description: Plan a compression-and-upload workflow using rv-image-optimize upload or pipeline commands.
---

Prepare a safe image upload workflow using the official `rv-image-optimize` package.

Requirements:

- Prefer `npx rv-image-optimize` when available in the current project
- Prefer `--json` for structured output
- Recommend `upload` for single output uploads
- Recommend `pipeline` when the user wants batch compression plus upload orchestration
- Suggest `--config` when request headers or form fields become complex
- If compression output is not effective, say so before proposing upload replacement flows
- Do not propose deleting or replacing originals unless the user explicitly requests it
