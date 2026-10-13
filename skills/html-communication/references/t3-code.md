# T3 Code inline HTML

Read this when native `html_preview` and `html_render` tools are available.
This contract comes from [pingdotgg/t3code](https://github.com/pingdotgg/t3code),
checked on 2026-10-13 at commit
`e9221e44dadd78126c83d2eeed0b51c25dcf0fb4`. The live runtime tool definitions
take precedence over this snapshot. No repository clone is needed for normal use.

## Theme and layout

T3 stores the page as a thread attachment and displays it above the final text
in a sandboxed iframe or mobile WebView. The inline frame is borderless and
aligned with the reply text. Its default desktop width is 728px; phones have
about 360px of content width. Wider chat settings and the expanded viewer need
fluid layout too.

T3 injects theme variables, base typography, a theme bridge and content-height
reporting. Do not reimplement that bridge or define the host token names in
your own `:root`. Use properties such as
`color: var(--foreground, #202124)` and scope any fallback palette under your
own names. CSS variables follow custom themes and appearance changes live.
Preview uses T3's stock light/dark palette and measurement fonts; it does not
prove contrast or line wrapping for every custom theme and user font.

| Purpose | Injected CSS properties |
| --- | --- |
| Page and prose | `--background`, `--foreground`, `--muted`, `--muted-foreground` |
| Content panels | `--card`, `--card-foreground`, `--popover`, `--popover-foreground` |
| Secondary controls | `--secondary`, `--secondary-foreground` |
| Borders and focus | `--border`, `--input`, `--ring` |
| Solid actions | `--primary`, `--primary-foreground` |
| Brand emphasis | `--accent`, `--accent-foreground`, `--accent-surface`, `--accent-surface-foreground` |
| Error | `--destructive`, `--destructive-foreground`, `--destructive-surface` |
| Warning | `--warning`, `--warning-foreground`, `--warning-surface` |
| Success and information | `--success`, `--success-foreground`, `--info`, `--info-foreground` |
| Code | `--code-background`, `--code-foreground` |
| Chart series | `--chart-1` through `--chart-6` |
| Shape and typography | `--radius`, `--font-sans`, `--font-mono` |

In this bridge, `--accent` means the brand color, unlike a neutral hover surface
in some UI libraries. Use `--accent-surface` with `--accent-surface-foreground`
for emphasis panels; use `--primary` with `--primary-foreground` for a solid
working action. Status foreground tokens are suitable for status text; do not
assume the status fill color provides readable text on every background.
Consume colors as CSS values rather than assuming hex or manually parsing RGB.

Leave the document and its outer wrapper transparent, without an enclosing
card, title banner or horizontal gutters. T3 paints the surrounding background.
Give an actual content panel at least 16px padding and host-radius corners.
Use a compact content heading only when the reader needs it. Do not build a
replica chat sidebar, composer or application shell around the answer.

Let content size the page. Avoid viewport-based document heights, including
`min-height: 100vh`, and percentage document heights. A resize-observed frame
can repeatedly grow when its own viewport drives the document height. Charts
should have a fixed CSS pixel height, with a fluid width. Deliberate wide
content scrolls in its own labeled, focusable region.

The [starter](../assets/t3-inline.html) uses host variables with fallback colors,
stacked mobile comparisons, a native evidence disclosure and no author scripts.
Keep `data-delivery="inline"` for native rendering. To export it as a standalone
file, change that attribute to `standalone`; this enables page background,
gutters and OS-based light/dark fallback colors without overriding host tokens.

## Preview and render

Tool names may be exposed as `html_preview`, `mcp__t3_code__html_preview` or
another harness prefix. Use the actual callable tool. Read its current schema;
the following describes the checked version, not a separate API.

1. Pass the complete HTML string to `html_preview` with `width: 728` and
   `appearance: "dark"`. Check again around 360-390px and in `"light"`.
   A compact responsive starter should be checked at both widths in both
   appearances. Use a wider case only when the content needs it. Preview widths
   currently accept 240-1600px.
2. Inspect the returned PNG, `contentHeight`, console output and `missingImages`.
   Console messages include log/info/warning/error and uncaught exceptions.
   T3 can embed local image paths in `src`, CSS `url()` and script strings.
   An HTTP resource is loaded as-is; it is not made offline by the tool.
3. Resolve overflow, clipped labels, missing resources or errors. Optional
   temporary instrumentation can log measured layout and focus checks during
   preview. Remove that instrumentation and preview the final bytes before
   delivery. Use the preferred collaborative browser when actual interaction
   needs verification; do not replace `html_preview` with that browser.
4. Call `html_render` with `html`, a short descriptive `title` and integer
   `height`. The checked range is 80-2000px. For an ordinary reply, use the
   desktop preview's `contentHeight`, clamped to that range. T3 measures several
   widths and adapts the frame for each reader. A value below the desktop
   content height intentionally caps the frame and makes it scroll internally.
   Avoid that extra scrolling for a compact explanation. Long content above
   2000px will scroll; keep essential decisions near the top.
5. Keep the returned `htmlRender.attachmentId` and check for tool failure. A
   render receipt is a thread attachment reference, not a public webpage URL.
   Call render once for the finished version; it is not an idempotent preview.
   When the result is ambiguous, inspect the receipt/thread before retrying to
   avoid duplicates. Add only information absent from the page in final prose.

Preview may initially report browser installation in progress. Follow that
reported prerequisite and retry after readiness instead of publishing an
unchecked page or creating a separate server. If native verification cannot
run, report the missing check and provide a standalone file. Local validation
does not require uploading the page first. Native render publishes into the
current thread and does not require a separate hosting destination.

## Interaction boundary

Author scripts run inside T3's sandboxed page, away from the app's session and
storage. Inline HTML is a visual reply, not an MCP App with tool permissions.
It cannot be assumed to send messages, execute agent tools or persist ERP
changes. Use scripts only for local reader interactions that clarify the
requested explanation. Native `details`, anchors and CSS are sufficient for
many documents. Do not add parent DOM access, custom `postMessage` protocols,
network writes or simulated application actions.

The host handles external link opening, expand, source viewing and save.
Use ordinary evidence links instead of duplicating those controls. For a
requested file, inline assets yourself and provide fallback styling, so the
artifact does not rely on T3's injected bootstrap to remain readable.

## Sources

- [Visual replies documentation](https://github.com/pingdotgg/t3code/blob/e9221e44dadd78126c83d2eeed0b51c25dcf0fb4/docs/user/html-renders.md) describes themes, sandboxing, expansion, source and save.
- [Shared rendering contract](https://github.com/pingdotgg/t3code/blob/e9221e44dadd78126c83d2eeed0b51c25dcf0fb4/packages/shared/src/htmlRender.ts) defines theme tokens, layout guidance, sizing and the injected bootstrap.
- [Native tool schemas](https://github.com/pingdotgg/t3code/blob/e9221e44dadd78126c83d2eeed0b51c25dcf0fb4/apps/server/src/mcp/toolkits/html/tools.ts) define preview/render inputs and outputs.
- [Preview implementation](https://github.com/pingdotgg/t3code/blob/e9221e44dadd78126c83d2eeed0b51c25dcf0fb4/apps/server/src/htmlRender/HtmlRender.ts) shows stock preview palettes, measurement fonts and image inlining.
- [Inline web frame](https://github.com/pingdotgg/t3code/blob/e9221e44dadd78126c83d2eeed0b51c25dcf0fb4/apps/web/src/components/chat/HtmlRenderFrame.tsx) and [document frame](https://github.com/pingdotgg/t3code/blob/e9221e44dadd78126c83d2eeed0b51c25dcf0fb4/apps/web/src/components/files/BrowserDocumentFrame.tsx) show sizing, expansion, theme updates and sandbox flags.
