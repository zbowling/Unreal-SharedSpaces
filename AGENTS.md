# Agent Instructions — Shared Spaces (Unreal, EOS branch)

Unreal Engine multiplayer sample showing how to connect users in VR using Oculus Social Platform APIs with the Unreal EOS plugin as the transport layer and UE replication.

## Source-of-truth files (read these first, do not duplicate their contents in this file)

For setup, build steps, SDK versions, and project layout, read:

- `README.md` — official build instructions and links to deeper docs
- `SharedSpaces.uproject` — Unreal engine version, plugins, and modules
- `Documentation/SharedSpaces.md` — full project walkthrough and OVRPlatform plugin notes
- `Documentation/EOSConfiguration.md` — EOS setup
- `.gitattributes` — Git LFS (required for blueprints and materials)
- `LICENSE` — license terms (Oculus License applies to the SDK; MIT applies to specifically marked docs)

## Quest / Horizon-specific notes

- This branch (default `eos-5.x`, **not** `main`) requires the **Meta Quest fork of Unreal Engine** (the `oculus-5.5` branch of `Oculus-VR/UnrealEngine`) — it will not build against stock Epic UE. Prebuilt Epic launcher binaries do not work for this sample.
- Project files are generated via `GenerateProjectFiles.bat -Game SharedSpaces -Engine <full path to Unreal-SharedSpaces dir>\SharedSpaces.uproject` from the Unreal source root — there is no UE-Editor "Generate VS Project" shortcut that produces the right setup.
- Git LFS is required (`git lfs install` before clone) — without it, blueprints and materials will be empty pointer files (silent failure, not a hard error).
- Oculus Application configuration (App ID, etc.) is required per `Documentation/SharedSpaces.md#d-oculus-application-configuration`.
- The repository also has other branches that target different Unreal versions / transport stacks; double-check you are on `eos-5.x` before debugging build failures.

## Meta Quest tooling

This repository is part of the Meta Quest / Horizon OS ecosystem (a sample, library, template, or related project — the bespoke intro above describes which). Use that intro and the source-of-truth files it references for project-specific decisions; don't restate or invent facts from memory.

When the user asks anything about Quest device behavior, build / deploy / debug / capture flows, on-device performance, or Horizon OS APIs, reach for these tools instead of generic Unreal answers:

- **`hzdb`** — Quest-aware ADB wrapper (device list, install / launch / stop, logs, screenshots, Perfetto traces, on-device docs search). Already wired up as an MCP server via `.mcp.json`, `.vscode/mcp.json`, and `.cursor/mcp.json`. Also runnable directly: `npx -y @meta-quest/hzdb <subcommand>`.
- **Meta Quest Agentic Tools** — the full skill set, including Unreal-specific skills: [github.com/meta-quest/agentic-tools](https://github.com/meta-quest/agentic-tools). Install per your client (Claude Code: `/plugin install meta-vr@meta-quest`; Gemini CLI: `gemini extensions install https://github.com/meta-quest/agentic-tools`; Cursor / VS Code: install the **Meta Horizon** extension from the Marketplace).

A few behavior expectations:

- **Read this repo's files first.** Before answering anything project-specific, read `README.md` and whichever source-of-truth files the intro above points at. Don't restate their contents in chat — quote or link instead.
- **Use `hzdb` for device-side work.** Anything that touches an attached Quest (install, launch, logs, screenshot, capture, manifest inspection) goes through `hzdb`, not raw `adb`.
- **Check live Horizon OS docs before answering API questions.** `hzdb docs search "..."` queries the live docs; training data on Horizon OS APIs goes stale fast.
- **Don't fabricate SDK / engine versions.** If a version isn't visible in this repo's files, say so rather than guessing.
