---
name: html-communication
description: Write self-contained HTML specifications, audits, technical plans and visual option comparisons. Use when communicating analysis in an HTML document, not when implementing a product website.
---

# HTML communication

## Required output

- Deliver exactly one self-contained UTF-8 HTML file, at most **512,000 bytes** including CSS, SVG and embedded assets. This conservative cap satisfies 512K. Aim smaller.
- Default to dark mode with explicit readable background/text colors and `color-scheme: dark`. Use system fonts and inline CSS. No external fonts, stylesheets, images, frames or runtime dependencies.
- **No JavaScript.** No script elements, event handlers, JavaScript URLs, frameworks or JS-driven diagrams. Use semantic HTML, CSS, inline SVG, tables, anchors and native `details`/`summary`. All substantive content must be readable without execution or network access.
- Write a specification, not a landing page. Start with purpose, status and the decision needed. Present current behavior, evidence, constraints, alternatives, tradeoffs, recommendation and acceptance criteria as appropriate. No sales hero, slogans, decorative KPI cards or fake controls.
- Read and apply the installed **unslop** skill before drafting and again before delivery. Resolve it through the agent's skill catalog or the sibling `../unslop/SKILL.md`; do not assume a username, operating system or global installation path. Install both skills when sharing this package. Do not duplicate its rules here. Never use em dashes, including HTML entities that render as em dashes.
- Distinguish observed facts, measurements, assumptions and proposals. Cite evidence close to the claim. Do not fabricate benchmark results, financial savings or completed actions.

## Make the explanation visual

Start by identifying what the reader must understand or decide. Choose the visual
that exposes that relationship before styling the page. A workflow benefits from
a sequence, a system from a map of responsibilities, and a choice from comparable
alternatives. A simple fact may need only a sentence. Do not turn every paragraph
into a card or force every document into the same dashboard template.

| Reader's question | Useful form | What it must reveal |
| --- | --- | --- |
| What changes? | Before/after with matching examples | The concrete difference and its consequence |
| How does this work? | Labeled steps or an inline SVG flow | Order, ownership, inputs and outputs |
| Where is the problem? | Annotated diagram or compact evidence table | The failing point and the evidence supporting it |
| Which option should we choose? | Lettered alternatives and a comparison table | Shared criteria, tradeoffs and recommendation |
| What happens next? | Phases or a checklist | Dependencies and observable completion criteria |

- Put the answer or recommendation near the top, with the reason that matters to
  the reader. Follow it with the main explanatory visual when useful. Keep source
  detail close to its claim or in native `details`; do not collapse the decision,
  critical constraints or essential caveats.
- Use a concrete worked example when it makes an abstract rule easier to see.
  Label synthetic examples as examples. Name actors and actions in diagrams;
  label arrows with what moves or causes the transition.
- Make each diagram understandable without hover: visible labels and a caption
  explaining what to notice. Give meaningful SVGs a `viewBox`, accessible title
  and description. Keep text readable; stack or use a scrolling region rather
  than shrinking a dense diagram to fit a phone.
- Charts need real supplied or verified data, units and an explanation of the
  relevant comparison. Avoid decorative gauges, invented percentages, progress
  bars and numbers presented as evidence.

## Visual design and interaction

Use the design-engineering principles adapted from Emil Kowalski: each treatment
needs a purpose, defaults should require little setup, and the document should
feel cohesive. These principles are included here; `emil-design-eng` and its
framework examples are not installation dependencies.

- Establish hierarchy with type, spacing and alignment. Use system sans-serif
  for prose and monospace for identifiers. Start around 16px with 1.5-1.65 line
  height and 60-75 character prose lines. Keep headings compact and specific;
  use a wider area for comparisons and diagrams.
- Use a small set of CSS variables for surfaces, text, spacing, borders and one
  accent color. Reuse their meanings throughout the page. Separate sections
  primarily with whitespace and quiet dividers; use panels to group content that
  the reader actually compares or treats as one unit.
- Reserve accent for the recommendation, active navigation or a relationship
  worth following. Status colors need visible text labels. Keep normal text at
  least 4.5:1 contrast and large text at least 3:1; muted text must remain legible.
- Avoid gradients, glow, glass effects, oversized hero type, decorative icons,
  repeated badges and generic grids of cards unless the content gives them a
  concrete explanatory role. Remove ornament that competes with the evidence.
- Use native anchors for navigation, with descriptive link text and visible
  keyboard focus. On long documents, provide a compact contents list. Native
  `details` should disclose supporting material with a summary that names it.
- Reading and keyboard navigation must respond immediately. Do not animate
  content into view, stagger sections, run looping effects or hide information
  behind hover. If a short CSS color/opacity transition helps a native control,
  name the exact properties, avoid `transition: all`, and respect
  `prefers-reduced-motion`. Gate hover embellishments behind
  `(hover: hover) and (pointer: fine)`; keep equivalent keyboard focus feedback.

## Visual comparisons

- Label alternative UI mocks **A**, **B**, **C** in their visible headings so the user can choose by letter. Use only as many alternatives as the task needs.
- Compare the same content and states at the same scale, side by side where space permits. Use matching section order and evaluation criteria. On narrow screens retain labels and reading order.
- For process or architecture options, lettered diagrams and a comparison table are useful; do not invent UI mocks for a task without UI choices.
- Keep the page body free of accidental horizontal overflow. Use `min-width: 0` on grid/flex children, `minmax(0, 1fr)` tracks, wrapping long identifiers and bounded media.
- Place deliberately wide tables, code, timelines or diagrams inside a labeled, keyboard-focusable region with `max-width: 100%; overflow: auto`. Panning means native scrolling, not JavaScript drag handlers.
- Do not hide layout defects with body-level `overflow-x: hidden` or clip unreadable content. Do not shrink a broad comparison into illegible text.

## Review, upload, then view

1. Draft locally outside product source unless repository delivery is requested. Review byte size, script/event/remote-asset absence, links, accessible headings and the actual content using the available tools. No bundled validator or language runtime is required.
2. Discover an authorized upload/attachment destination. Prefer the current app's private attachment mechanism or a destination the user chose. A request for a document does not authorize publishing private project content on a public host.
3. Upload the exact reviewed bytes. Wait for an explicit successful receipt. Preserve the returned attachment ID or URL and verify the uploaded size/hash when supported. Preparing an upload URL, starting a local server, or writing a local file is **not** successful upload.
4. **Never open a browser or claim the document is hosted before upload succeeds.** Do not start a local preview server as a substitute. If upload fails or the destination is unknown, report that fact and provide the local file without opening it. Ask only for the missing destination/authorization.
5. After upload succeeds, browser review is allowed. Use the environment's preferred browser tools. Check a desktop width around 1440px, a narrow width around 390px and 200% zoom. Confirm readable diagram labels, visible keyboard focus, usable comparison scrolling, adequate contrast and no body overflow. Check that a reader can identify the decision, understand the main visual and find its evidence without opening every detail. Page content still must not require JavaScript. Browser inspection scripts may measure layout; they must never be shipped in the document.
6. If review changes the file, review the new exact version and upload it before claiming the link is current. Distinguish an attachment available for download from a hosted/rendered webpage.

Deliver the successful attachment/link with a short summary and any unverified limitations. Do not replace the HTML with a ZIP, multiple files or a framework project.
