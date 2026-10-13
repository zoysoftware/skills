---
name: html-communication
description: Write visual explanations, specifications, audits, technical plans and UI comparisons as self-contained HTML. Prefer theme-aware inline replies through T3 Code's html_preview and html_render when available; deliver a standalone file otherwise. Not for implementing product websites.
---

# HTML communication

Explain the decision or relationship visually. In T3 Code, make the page feel
like part of the reply, with the chat's theme, typography and reading width.

## Choose delivery

- When the current runtime exposes `html_preview` and `html_render`, use the
  native inline flow. Names may have an MCP prefix. Read
  [the T3 Code contract](references/t3-code.md) before drafting for this mode,
  and prefer the live tool definitions if their contract has changed.
- When the user explicitly requests a downloadable HTML file, or native tools
  are unavailable, deliver one standalone UTF-8 file. Use the current app's
  private attachment mechanism when available, otherwise a local file link.
  A local file is a valid delivery; do not require hosting or invent an upload
  destination. A request for a document does not authorize public publishing.
- Build one self-contained document, at most **512,000 UTF-8 bytes** including
  inline CSS, SVG, scripts and embedded assets. Keep it smaller when practical.
  No external fonts, stylesheets, frames or runtime dependencies by default.
  Inline local images for file delivery; T3's native tools can embed them from
  absolute paths. Evidence links may point to their original sources.

## Explain before styling

Read and apply the installed **unslop** skill before drafting and before
delivery. Resolve it through the runtime catalog or `../unslop/SKILL.md`, never
an assumed global path. Install both skills when sharing this package. Never
use em dashes, including HTML entities that render as em dashes.

Start with the answer or recommendation and the reason that matters. Include
purpose, status and the decision needed when relevant. Distinguish observed
facts, measurements, assumptions, synthetic examples and proposals. Cite
evidence close to its claim. Do not invent results, savings or completed work.

Choose a visual that exposes what the reader must understand. A simple fact
may need only a sentence. Do not turn every paragraph into a card or force every
document into a dashboard.

| Reader's question | Useful form | What it must reveal |
| --- | --- | --- |
| What changes? | Before/after with matching examples | The concrete difference and its consequence |
| How does this work? | Labeled steps or an inline SVG flow | Order, ownership, inputs and outputs |
| Where is the problem? | Annotated diagram or compact evidence table | The failing point and its supporting evidence |
| Which option should we choose? | Lettered alternatives and a comparison table | Shared criteria, tradeoffs and recommendation |
| What happens next? | Phases or a checklist | Dependencies and observable completion criteria |

- Follow the answer with the main explanatory visual when useful. Put source
  detail close to its claim or in native `details`. Keep the decision, critical
  constraints and essential caveats visible.
- Use a worked example when it clarifies an abstract rule. Label synthetic
  examples. Name actors and actions in diagrams and what moves along arrows.
- Make diagrams understandable without hover, with visible labels and a caption.
  Give meaningful SVGs a `viewBox`, accessible title and description. Stack or
  use native scrolling rather than shrinking dense diagrams to fit a phone.
- Charts need supplied or verified data, units and an explanation of the relevant
  comparison. Avoid invented percentages, decorative gauges and fake progress.

## Fit the host

In T3 inline mode, leave `html`, `body` and the outermost element transparent.
Use fluid width, zero outer horizontal padding and no enclosing card, border
or banner title. A compact content heading is fine when it explains the answer.
Let content determine height. Avoid `100vh`, viewport-based minimum heights and
`height: 100%` on the document; the frame grows to fit it. Use fixed pixel chart
heights. Background panels that serve the content need at least 16px padding
on every side and `var(--radius, 0.625rem)` corners.

Use host variables through `var(--foreground, fallback)` and similar expressions.
Never redefine T3's token names on `:root`, force `color-scheme: dark`, or copy
its theme/message bridge into the page. T3 updates the theme live. For a
standalone file, add scoped light/dark fallbacks, a readable page background and
modest outer gutters. The [starter](assets/t3-inline.html) includes an explicit
`data-delivery="standalone"` mode; read it when a reusable CSS base would help.
Adapt its structure to the question instead of preserving its sample content.

- Use system sans-serif for prose and monospace for identifiers, through the
  host's font variables in native mode. Start at 14-16px with 1.5-1.65 line
  height and compact headings. Prefer whitespace and quiet dividers to boxes.
- Use semantic surface/text pairs and one accent for the recommendation or a
  relationship worth following. Status colors need text labels. Check normal
  text at 4.5:1 contrast, large text at 3:1 and legible muted text in both modes.
- Avoid gradients, glow, glass effects, oversized hero type, decorative icons,
  repeated badges and generic card grids. Build an explanation, not a landing
  page. Keep tool names and rendering mechanics out of ordinary reader content.
- Use descriptive anchors, visible keyboard focus and native `details` for
  supporting material. Long documents can have compact contents navigation.
- Do not animate content into view, stagger sections, loop effects or hide
  information behind hover. If a short transition helps a control, name its
  properties, avoid `transition: all` and respect `prefers-reduced-motion`.
  Gate hover decoration behind `(hover: hover) and (pointer: fine)`.

## Compare and interact

- Label UI alternatives **A**, **B**, **C** in their visible headings. Compare
  the same content and states at the same scale with shared criteria. Stack
  alternatives on narrow screens, preserving their labels and reading order.
- Keep the page free of accidental horizontal overflow. Use `min-width: 0` on
  grid/flex children, `minmax(0, 1fr)` tracks, wrapping identifiers and bounded
  media. Put intentionally wide tables/code/diagrams inside a labeled,
  keyboard-focusable region with `max-width: 100%; overflow: auto`.
  Do not hide layout defects with body-level `overflow-x: hidden`.
- Default to semantic HTML, CSS, inline SVG and native controls. Small inline
  JavaScript is appropriate for a requested filter, simulation or comparison
  whose changing state helps understanding. Keep essential facts and the
  initial explanation readable without execution or network access. Skip
  scripts for ordinary specifications and static comparisons.
- Controls must work and state what they change. Keep interactions local to
  the document; do not imply they write to the repository, ERP or chat. Use
  native listeners and controls, no frameworks, remote scripts or JavaScript
  URLs. A user-requested static/no-JS deliverable takes precedence.

## Verify and deliver

1. Draft outside product source unless repository delivery is requested. Review
   UTF-8 size, references, assets, headings and substantive content. An upload
   receipt or screenshot alone does not prove the explanation is correct.
2. In T3, preview the exact document with `html_preview` before publishing.
   Check the reply width, a phone width and both appearances. Inspect screenshots,
   `contentHeight`, console errors and missing images. Revise and re-preview
   affected cases. Details are in [the native flow](references/t3-code.md#preview-and-render).
3. For a standalone file, local browser review is allowed before any upload.
   Use the runtime's preferred browser tools and check desktop, phone and 200%
   zoom where supported. For either mode, verify readable labels, keyboard
   focus, intentional scrolling and no body overflow. Exercise added scripts
   with actual controls; a static preview does not prove interaction works.
   Inspection scripts are not shipped unless part of the requested interaction.
4. In T3, call `html_render` with the reviewed document, short title and measured
   height. Preserve its successful attachment reference. Do not substitute a
   code block, local server, upload-URL preparation or full browser preview for
   native rendering. If native preview/render fails, diagnose the reported
   prerequisite or actionable error; if unavailable, deliver the standalone
   file and state the unverified part. Do not claim an inline render succeeded.
5. For file delivery, attach the exact reviewed bytes if a private mechanism is
   available. Wait for its successful receipt before claiming upload. Otherwise
   provide the local link. Review and redeliver changed bytes before calling
   an attachment current. Do not replace the HTML with a ZIP or framework.

After a successful inline render, the final reply adds only what the page does
not already say, such as a repository change or a verification limit. Do not
announce the page or repeat its conclusions. For file delivery, give its link
and a short summary, distinguishing download, local file and hosted page.
