---
name: clone-website
description: Reverse-engineer and rebuild websites with high visual fidelity by extracting real assets, computed styles, responsive behavior, and interaction states. Use for clone, replicate, rebuild, reverse-engineer, or pixel-perfect website requests. Provide one or more URLs.
argument-hint: "<url1> [<url2> ...]"
user-invocable: true
---

# Clone Website

Reverse-engineer and rebuild **$ARGUMENTS** with high visual fidelity.

This skill is adapted from the MIT-licensed `JCodesMore/ai-website-cloner-template` workflow. It is intentionally installed alongside UI UX Pro Max so design/UX intelligence can be used during implementation and QA without modifying the existing UI UX Pro Max skill.

## Workflow

1. **Pre-flight:** Require browser automation; validate URLs; verify the project builds; inventory existing routes/assets; create a collision-free output plan. Never overwrite user-authored routes without explicit approval.
2. **Reconnaissance:** Capture desktop/mobile screenshots; extract fonts, colors, assets, DOM structure, computed CSS, and page topology.
3. **Behavior sweep:** Scroll before clicking; test every apparent click/hover interaction; capture sticky behavior, observers, animation, carousels, tabs, modals, dropdowns, responsive transitions, and every reachable state. Save findings to `docs/research/<site-key>/<page-key>/BEHAVIORS.md`.
4. **Foundation:** Establish scoped fonts/design tokens/types/icons and download real assets into namespaced paths before parallel component work.
5. **Specs first:** Before building each component, write `docs/research/<site-key>/<page-key>/components/<component>.spec.md` with exact hierarchy, computed styles, assets, text, interaction model, states, transitions, responsive behavior, and destination file.
6. **Build small:** Split complex sections into focused components. Parallelize independent builders only after the shared foundation is fixed. Each task must pass `npx tsc --noEmit`.
7. **Assembly:** Wire components into the planned route while preserving existing routes. Implement exact page-level scrolling/sticky/observer behavior. Run `npm run build`.
8. **Visual QA:** Capture clone/source at matching 1440px and 390px viewports, compare section-by-section, repair discrepancies from the source/spec, and retest all interactive states.

## Extraction Requirements

Never guess when browser measurement is possible. Capture relevant `getComputedStyle()` properties including typography, colors, backgrounds, spacing, dimensions, flex/grid, borders, radius, shadows, overflow, position, z-index, opacity, transforms, transitions, object-fit/object-position, filters, whitespace, and text overflow.

Extract real visible text, images, videos, background images, inline SVGs, icons, fonts, and layered assets. Determine whether each interactive section is driven by scroll, click, hover, time, resize, or a combination. Capture all states, exact triggers, before/after values, transition duration/easing, and responsive behavior at 1440px, 768px, and 390px.

## Component Spec Minimum

Every spec must contain:
- Target component path and reference screenshot.
- Exact DOM hierarchy.
- Exact measured computed styles.
- Interaction model and trigger mechanism.
- Every state and its content/styles.
- Local paths for all assets.
- Verbatim visible text.
- Desktop/tablet/mobile behavior and breakpoints.

## Guardrails

- Do not claim to clone private backend/database/authentication/server source that is not observable from the browser.
- Do not overwrite unrelated routes/components/assets.
- Do not skip responsive or interaction extraction.
- Do not substitute generic assets/content when the real browser-visible assets/content can be extracted.
- Do not dispatch a builder before its spec exists.
- Do not declare completion until typecheck/build and visual QA pass.

## UI UX Pro Max Integration

When the existing `ui-ux-pro-max` skill is available, use it as a secondary QA/design-intelligence layer for accessibility, touch targets, responsive behavior, typography, performance, motion, navigation, and visual consistency. Source fidelity takes priority when the user explicitly requests an exact reproduction; otherwise use UI UX Pro Max recommendations to improve usability while preserving the target's visual language.

## Completion Report

Report URL→route mappings, routes preserved/replaced, sections/components/specs created, downloaded assets, typecheck/build status, visual QA status, and remaining limitations.

## Attribution

Adapted from `JCodesMore/ai-website-cloner-template`, MIT License, Copyright (c) 2025 JCodesMore.
