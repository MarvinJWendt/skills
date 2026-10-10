---
name: quick-html
description: Build a single self-contained HTML file with Tailwind and CDN imports, no build step. Reports, local experiment frontends, and debug UIs served by a backend.
disable-model-invocation: true
---

# quick-html

One `.html` file that opens in a browser and needs nothing else: no build step, no bundler, no Node. Dependencies load from jsDelivr and the markup stays readable, so the next agent to touch the page edits the thing that actually runs.

Three shapes come up: a report handed to a human, a frontend for a local experiment, and a debug UI a backend serves out of its own binary. Same file either way.

Write the file to disk and print the path. This never becomes a published artifact.

## Naming

A page a backend serves is `index.html`. A file a human opens is named after what it holds, so `kubernetes-cost-report-2026.html` rather than `report.html`. It lands in the working directory unless the repo has an obvious place for static files.

## Stack

Tailwind v4 through the browser build, `https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4`. Configuration goes in an inline `<style type="text/tailwindcss">` block, not a JS config object.

Alpine drives every page, the theme toggle and the tabs included. Any state beyond those is Alpine too.

Everything else is your call. These are the defaults to beat:

| Need | Package |
| --- | --- |
| charts | `chart.js` |
| tables that sort, filter or page | `tabulator-tables`, otherwise plain markup driven by Alpine |
| markdown | `marked` |
| syntax highlighting | `shiki` |
| icons | `lucide` |
| CSV parsing | `papaparse` |
| diagrams | `mermaid` |
| dates | native `Intl`, no package |

Shiki is ESM only, so it loads through `<script type="module">` from `https://cdn.jsdelivr.net/npm/shiki@<major>/+esm`. Its dual-theme mode emits both palettes as CSS variables in one pass, which is what keeps highlighted code readable on both sides of the theme toggle.

### Versions

Pin the major: `chart.js@4`. Never `@latest`, never a full version. Patches then arrive on their own and a new major cannot.

Resolve that major as you write the file, and again when you edit a page whose pins look old:

```sh
curl -s https://registry.npmjs.org/chart.js/latest | jq -r .version
```

If the major moved, pin the new one and migrate the code that used the old API.

## Chrome

A navbar across the top: the project or tool name as plain text on the left, tabs in the middle once there is more than one view, theme toggle on the right. A live page may put a refresh button and a last-updated timestamp beside the toggle. Nothing else belongs up there.

Tabs route through the hash (`#/logs`), so a reload keeps the view and a link points at one.

### Theme

Three states: system, light, dark. System is the default and follows `prefers-color-scheme` live through a `matchMedia` listener, not only at load. The choice persists in `localStorage`.

Two things break this quietly. Tailwind v4 resolves `dark:` against the media query alone, so class-based switching needs `@custom-variant dark (&:where(.dark, .dark *));` declared in the Tailwind style block. And the class has to land on `<html>` from an inline script in `<head>` that runs before the first paint, or every load flashes light.

### Looks

Professional, technical, and dense. These are data pages, so spacing stays tight. System font stack, no webfont. Monospace for anything a human scans rather than reads: IDs, hashes, durations, timestamps.

A neutral base (`slate` or `zinc`) plus one accent. Take the accent from the project when it has a palette of its own, otherwise pick one that suits what the tool does. Pages across different projects do not have to look alike.

Real `<button>` elements, visible focus rings, labelled inputs. That is the whole accessibility bar.

## Data

A page a backend serves fetches from that backend. A page handed to a human carries its data inline in `<script id="data" type="application/json">`.

Fetching pages need all three states: loading, empty, and failed. The failure state prints the status and the response body, since the page exists to debug something and a swallowed error defeats it.

Live pages refresh on a button, plus an interval the user can switch on and off and see. Poll silently and nobody can tell whether the page or the tool went stale. Reach for SSE or a WebSocket only when the backend already speaks one.

A report gets a `@media print` block, so it prints to a PDF worth sending to someone who will never run the tool.

## Readability

Agents do most of the later editing, and the file is their input. Keep it legible:

- A comment at the top: what the page is, where its data comes from, how to run it.
- Order: header comment, Tailwind theme block, markup, then one `<script>` holding the Alpine components.
- Section comments between major blocks of markup.
- `x-data` stays a single line on the element. Longer components live in the script as `Alpine.data('name', ...)`.
- Nothing minified, nothing generated, nothing pasted in as a blob.

## Prose on the page

Load `unslop` for the text that ships in the interface: labels, empty states, error copy, tooltips, headings. Load `technical-writing` too when prose carries the page, as in a report built of findings and paragraphs.

Charts route to `dataviz`. Colour that holds up in both themes is its subject, not this one.

## Editing a page that exists

Bring it to these rules, including the parts it currently contradicts, and report what you changed. A page on Tailwind v3 or without a theme toggle gets migrated, not matched.

## Checking it

Opening the page costs time, so spend it where it pays: once after finishing a one-shot report, or when part of the page is involved enough that you are unsure it works. The user saying something looks wrong is the other trigger. Not after every edit.

## When to stop

Say so instead of pushing the single file further once it needs a build step, routing past tabs, or components shared across pages, and when the repo already has a frontend stack this belongs in.
