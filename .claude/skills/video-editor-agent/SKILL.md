---
name: video-editor-agent
description: End-to-end AI video editing workflow for raw footage, transcripts, B-roll, motion graphics, captions, branding, Remotion composition, QA, and delivery. Use for social videos, explainers, listing videos, market updates, webinars, ads, and repurposing long-form footage into short-form edits.
---

# Video Editor Agent

## Purpose
Turn raw footage and supporting context into a polished, platform-ready video using an auditable, non-destructive workflow. Coordinate analysis, transcription, edit planning, B-roll research/capture, motion graphics, captions, branding, Remotion composition, QA, and final render.

## Core operating rules
1. Never overwrite source media. Work from copies/proxies and preserve originals.
2. Never invent quotes, facts, logos, product claims, market statistics, or visual evidence. If external facts are used, verify them and keep source notes.
3. Treat third-party footage, music, screenshots, and brand assets as licensed only when the user provides them or usage rights are verified.
4. Keep credentials, cookies, API keys, tokens, and secrets out of source control and rendered frames.
5. Prefer deterministic, editable project files over one-off black-box generations.
6. Before final render, run visual, audio, timing, caption, spelling, safe-area, and export QA.
7. When an existing project already has style rules, brand assets, or a master context file, preserve them unless the user explicitly requests a redesign.

## Tool routing
Use the best available tool for each stage:
- MarkItDown: ingest PDFs, DOCX, PPTX, XLSX, HTML, and reference docs.
- Agent Reach: research public web/social/video sources when external context or references are needed.
- Claude-Mem: recall prior project decisions, brand rules, and edit history when available.
- Video Shotcraft: shot design, motion language, transitions, cinematic composition, and motion recipes.
- Taste Skill: premium/editorial visual direction.
- UI UX Pro Max: readability, accessibility, contrast, and layout rules for graphics.
- Remotion: primary programmatic editing/compositing/rendering engine when available.
- Screen Studio or equivalent: capture high-quality website/app B-roll when available and permitted.
- ffmpeg: media probing, proxies, trims, audio normalization, transcoding, thumbnails, and packaging.
- Whisper or equivalent: transcript and word-level timestamps.
- LiteLLM: provider routing when configured.
- ECC / gstack / Ruflo: planning, orchestration, review, QA, or parallel-agent execution when useful; do not duplicate work merely because they exist.

If a named tool is unavailable, continue with the closest safe alternative and document the substitution.

## Workflow

### 1. Intake and media inventory
Create a manifest before editing: source videos, durations, frame size, frame rate, codec, orientation, audio tracks, supplied brand assets, references, target platform, aspect ratios, target duration, CTA, and destination URL. Probe all media and flag corrupt, variable-frame-rate, silent, clipped, or low-resolution assets.

### 2. Transcript and content map
Generate or import a time-coded transcript. Preserve the verbatim transcript separately from any cleaned script. Build a content map with hook, key claims, proof, emotional beats, filler/repetition candidates, possible cut points, CTA, and sections requiring B-roll or graphics. Do not silently change speaker meaning.

### 3. Edit brief
Define objective, audience, platform, aspect ratio, target length, pacing, visual language, caption style, graphic-card range, B-roll requirements, music/SFX direction, CTA treatment, and brand constraints. For short-form social, default to a strong opening in the first 1–2 seconds without inventing sensational claims.

### 4. Paper edit / timeline plan
Create a time-coded paper edit before full implementation. For each segment specify source in/out, spoken line or purpose, on-screen text, B-roll/visual, motion graphic, transition, and audio treatment. Keep timeline decisions machine-readable where practical.

### 5. B-roll and supporting visuals
Prioritize: user-provided footage/assets; purpose-recorded screen captures; licensed/public-domain material with verified rights; original graphics/diagrams; AI-generated imagery/video when requested. Hide private data, credentials, messages, account identifiers, and browser secrets before screen capture.

### 6. Motion graphics
Use graphics only when they improve comprehension or pacing. Suitable elements include title cards, lower thirds, kinetic quotes, statistic cards, comparison cards, diagrams, maps, timelines, browser/device frames, and CTA/end cards. Maintain a coherent visual system across typography, spacing, radii, shadows, strokes, iconography, and animation curves. Avoid generic AI design patterns unless requested.

### 7. Captions
Use word-level timestamps when possible. Correct obvious transcript errors against audio, keep chunks readable, preserve meaning, avoid covering faces or platform UI, honor safe zones, maintain strong contrast, and highlight words only when helpful.

### 8. Audio
Perform dialogue cleanup, silence/noise management, loudness consistency, music ducking, restrained SFX, fades, and clipping checks. Use only user-provided, licensed, platform-cleared, or rights-safe music.

### 9. Remotion implementation
When Remotion is available: create reusable components; separate timing/content data from presentation; use deterministic frame-based animation; preload media when useful; keep long operations out of render paths; use composition props for aspect ratio, brand, CTA, and variants; preserve editability for 9:16, 1:1, and 16:9.

Recommended structure:
```text
video/
  src/
    compositions/
    components/
    cards/
    captions/
    data/
    styles/
  public/
    media/
    logos/
    fonts/
  transcripts/
  references/
  renders/
```

### 10. QA
Content: claims match sources; no meaning changes; names, numbers, dates, URLs, and CTA are correct.
Visual: no clipped/off-screen elements, broken assets, unreadable text, unsafe placement, inconsistent margins, accidental black/frozen frames.
Audio: intelligible dialogue, no clipping/pops, balanced music, sync maintained.
Captions: spelling/punctuation checked, timing accurate, segmentation readable.
Technical: correct resolution/aspect ratio, duration, frame rate, codec/container, and playable/seeking final file.

### 11. Deliverables
Unless specified otherwise, preserve editable source, paper edit/timeline data, transcript, asset manifest, final master render, platform derivatives, thumbnail/poster when requested, and provenance notes for externally sourced assets.

## Default platform presets
Use only when no destination specs are provided; verify current production requirements when they may have changed.
- Vertical social: 9:16, 1080×1920
- Square social: 1:1, 1080×1080
- Landscape: 16:9, 1920×1080
Do not assume max duration, file size, bitrate, or codec constraints are stable.

## Editing modes
### Short-form social
Optimize for fast comprehension, strong opening seconds, purposeful visual changes, captions, and clear CTA.

### Long-form / webinar
Prioritize continuity, chapter structure, lower visual density, clean slides, and section transitions.

### Real-estate / property video
Preserve spatial truth. Never manipulate imagery in ways that materially misrepresent condition, view, room size, fixtures, boundaries, or surroundings. Clearly distinguish illustrative/generated visuals from actual property footage.

### Marketing/ad creative
Maintain an evidence trail for factual claims and testimonials. Build variants from a shared master so hook, copy, CTA, and duration can be tested without rebuilding the entire edit.

## Handoff protocol
At session end record what was completed, current timeline/render status, unresolved issues, missing assets, source files used, output paths, and next recommended action. When Claude-Mem is active, store only non-secret project decisions and references; never persist API keys, credentials, cookies, or private tokens.
