---
name: clone-website
description: Reverse-engineer and clone one or more websites in one shot — extracts assets, CSS, and content section-by-section and proactively dispatches parallel builder agents in worktrees as it goes. Use this whenever the user wants to clone, replicate, rebuild, reverse-engineer, or copy any website. Also triggers on phrases like "make a copy of this site", "rebuild this page", "pixel-perfect clone". Provide one or more target URLs as arguments.
argument-hint: "<url1> [<url2> ...]"
user-invocable: true
---

# Clone Website

You are about to reverse-engineer and rebuild **$ARGUMENTS** as pixel-perfect clones.

This installed skill is based on the MIT-licensed JCodesMore/ai-website-cloner-template clone-website workflow. Preserve attribution when redistributing substantial portions.

When multiple URLs are provided, preserve every pathname as a distinct route and isolate each target's research, screenshots, components, and assets. Parallelize page work only after the shared foundation and output plan are fixed so concurrent builders cannot overwrite one another.

## Scope Defaults

- **Fidelity level:** Pixel-perfect — exact colors, spacing, typography, and animations.
- **In scope:** Visual layout/styling, component structure/interactions, responsive behavior, and mock data where necessary.
- **Out of scope:** Private backend/database code, authentication internals, real-time infrastructure, or proprietary server-side logic that cannot be observed from the browser.
- **Customization:** None unless the user requests it.

## Pre-Flight

1. Browser automation is required. Prefer Chrome MCP, otherwise use Playwright, Browserbase, Puppeteer, or another browser automation tool.
2. Parse and validate every target URL and verify it is reachable.
3. Verify the base application builds before editing. The upstream workflow expects a modern Next.js + TypeScript + Tailwind/shadcn scaffold.
4. Inventory all existing routes, components, screenshots, research artifacts, and public assets before writing.
5. Create an output plan mapping each source URL to a destination route and unique research/component/asset namespaces. Never overwrite an existing user-authored route without explicit approval.
6. For multiple pages from one origin, establish shared fonts, tokens, and layout behavior sequentially before parallel page work.

## Guiding Principles

### Completeness beats speed
Every builder must receive screenshots, exact computed CSS values, real content, real assets, DOM structure, responsive behavior, and all interaction states. If a builder has to guess a color, spacing value, font size, asset, or transition, extraction is incomplete.

### Small tasks produce better fidelity
Split complex sections into focused components. If a builder brief grows beyond roughly 150 lines of detailed specification, split the work further.

### Extract real content and assets
Inspect and capture actual text, images, videos, background images, inline SVGs, icons, fonts, and layered compositions visible from the browser. Do not substitute generic mock content unless the source is session-specific or inaccessible.

### Foundation first
Establish fonts, color/design tokens, shared types, icons, asset namespaces, and any truly global behavior before dispatching parallel component work.

### Reproduce behavior, not just screenshots
For every interactive element determine whether its behavior is driven by click, hover, scroll, time, resize, or a combination. Capture before/after states, trigger thresholds, transition durations/easing, sticky behavior, observers, scroll snapping, carousels, modals, dropdowns, and responsive changes.

### Extract every state
For tabs, pills, accordions, menus, sticky headers, hover effects, scroll-driven sections, carousels, and other stateful UI, capture every reachable state and its exact content/styles.

### Specs are the source of truth
Before building a component, write a component spec under `docs/research/<site-key>/<page-key>/components/<component>.spec.md`. The spec must include DOM structure, exact computed styles, interaction model, states/behaviors, assets, verbatim visible text, responsive behavior, and target file path.

### Build must compile
Every component task must end with TypeScript validation. After assembly, run the full project build and fix all errors before declaring completion.

## Phase 1 — Reconnaissance

Use browser automation to inspect the target.

1. Capture full-page screenshots at desktop (1440px) and mobile (390px), plus tablet (768px) where useful.
2. Extract fonts and weights actually used.
3. Extract the color palette and design tokens from computed styles.
4. Enumerate `<img>`, `<video>`, background images, favicons, inline SVGs, and other visual assets.
5. Perform a full scroll sweep from top to bottom before clicking anything. Record sticky/fixed behavior, scroll-triggered animation, section changes, smooth-scroll libraries, and scroll snap.
6. Click every interactive-looking control and capture every state.
7. Hover links, buttons, cards, nav items, and images; record exact changed properties and transitions.
8. Repeat at 1440px, 768px, and 390px and document breakpoint behavior.
9. Save interaction findings to `docs/research/<site-key>/<page-key>/BEHAVIORS.md`.
10. Save page section order, overlays, z-index relationships, dependencies, and interaction models to `PAGE_TOPOLOGY.md`.

## Phase 2 — Foundation

For each origin, sequentially:

1. Merge or scope fonts and layout behavior without breaking existing routes.
2. Merge or scope design tokens and global CSS carefully.
3. Create namespaced TypeScript interfaces for observed content structures.
4. Extract/deduplicate SVG icons into page- or site-scoped icon modules.
5. Download discovered assets into `public/sites/<site-key>/<page-key>/` or an approved same-site shared namespace.
6. Build the project and verify all previously existing routes still work.

## Phase 3 — Component Extraction, Specs, and Build

For each page section from top to bottom:

1. Capture a section screenshot.
2. Extract the section DOM and relevant `getComputedStyle()` values, including typography, colors, background, padding, margin, dimensions, flex/grid, borders, radius, shadows, overflow, position, z-index, opacity, transforms, transitions, object fit/position, filters, whitespace, and text-overflow properties.
3. Capture every state by triggering scroll/click/hover/time behaviors and recording property differences.
4. Extract all visible text, alt text, labels, placeholders, and per-state content.
5. Map every section asset to its local namespaced file path.
6. Write a component specification before implementation.
7. Build simple components as focused tasks. Split complex sections into sub-components.
8. Verify `npx tsc --noEmit` for each completed component task.
9. Keep extracting the next section while independent builders work in parallel when the coding environment supports parallel agents/worktrees.
10. Merge incrementally and run `npm run build` after merges.

## Component Spec Template

```markdown
# <ComponentName> Specification

## Overview
- Target file: `src/components/sites/<site-key>/<page-key>/<ComponentName>.tsx`
- Screenshot: `docs/design-references/<site-key>/<page-key>/<screenshot>.png`
- Interaction model: static | click-driven | scroll-driven | hover-driven | time-driven | mixed

## DOM Structure
<exact hierarchy>

## Computed Styles
### Container
- <property>: <exact computed value>
### Child elements
- <property>: <exact computed value>

## States & Behaviors
- Trigger: <exact mechanism/threshold>
- State A: <values>
- State B: <values>
- Transition: <duration/easing/properties>
- Implementation approach: <observer/listener/CSS/etc.>

## Per-State Content
<all states and exact visible content>

## Assets
<local paths for images/videos/SVGs/fonts>

## Text Content
<verbatim visible source text>

## Responsive Behavior
- Desktop 1440px: ...
- Tablet 768px: ...
- Mobile 390px: ...
- Breakpoint(s): ...
```

## Phase 4 — Assembly

Wire all built sections into the exact route from the output plan. Preserve existing routes. Implement page-level sticky positioning, scroll containers, observers, animation, snapping, smooth-scroll behavior, and responsive layout. Run `npm run build` and repair all errors.

## Phase 5 — Visual QA

1. Capture the finished clone and source at identical 1440px and 390px viewports.
2. Compare section-by-section from top to bottom.
3. For every discrepancy, check the component spec. If extraction was wrong, re-extract and update the spec; if implementation differs from the spec, fix the implementation.
4. Test every click, tab, hover, scroll-driven state, modal, dropdown, carousel, sticky header, animation, and responsive transition.
5. Do not declare completion until visual QA and the production build pass.

## Pre-Dispatch Checklist

- Spec file exists and is complete.
- CSS values were measured with browser computed styles, not guessed.
- Interaction model is identified.
- Every reachable state is documented.
- Scroll triggers and transitions are recorded.
- Hover states are recorded.
- Layered/overlay images are accounted for.
- Desktop and mobile behavior are documented.
- Visible text is copied accurately.
- Builder scope is small enough for high fidelity.

## What Not To Do

- Do not confuse click-driven and scroll-driven behavior.
- Do not capture only the default state.
- Do not miss overlay or layered assets.
- Do not rebuild a video/canvas/Lottie sequence as static HTML without first identifying what it actually is.
- Do not approximate CSS when computed values can be measured.
- Do not overwrite unrelated routes, assets, or components.
- Do not skip responsive extraction.
- Do not skip real asset extraction.
- Do not dispatch a builder before its spec exists.
- Do not claim access to private backend source code that the browser cannot expose.

## Completion Report

When done, report:
- Source URL → destination route mapping for every page.
- Existing routes preserved and any approved replacements.
- Total sections/components/spec files created.
- Total downloaded assets by type.
- Build and typecheck status.
- Visual QA results.
- Any remaining limitations.

## Attribution

Workflow adapted from `JCodesMore/ai-website-cloner-template`, MIT License, Copyright (c) 2025 JCodesMore.
