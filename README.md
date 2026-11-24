# Félix web accessibility

Webflow accessibility skills for auditing and fixing Félix Main pages to meet WCAG 2.1 Level AA. Neither skill publishes the site.

The hour plan and the page list live in [Accessible website — Félix Main](https://app.notion.com/p/41509747501e81fe88f6f010566816af).

## Skills in this repo

Both skills live where Cursor reads them automatically:

- `.cursor/skills/felix-page-accessibility/` — Félix Main one-page WCAG 2.1 Level AA fix loop. Checks images, contrast, focus, forms, headings, iframes, and keyboard structure in the Designer, then loops until the checklist passes.
- `.cursor/skills/webflow-mcp-accessibility-audit/` — Webflow's headless WCAG 2.1 audit (`webflow-mcp:accessibility-audit`). Runs without opening the Designer, scores a page (or multiple pages), generates a report, and offers approved attribute fixes. Skips image alt text and color contrast.

## Once

1. Make sure the Webflow MCP connection in Cursor is signed in.
2. If you are running `felix-page-accessibility`, open **Félix - Main** in the Webflow Designer and keep that tab in front. (`webflow-mcp:accessibility-audit` runs headlessly and does not need the Designer open.)

Claude Code reads skills from `.claude/skills/`. Copy the folders there once if you use Claude Code:

`.cursor/skills/felix-page-accessibility/` → `.claude/skills/felix-page-accessibility/`
`.cursor/skills/webflow-mcp-accessibility-audit/` → `.claude/skills/webflow-mcp-accessibility-audit/`

## Running `felix-page-accessibility` (one-page fix loop)

Start a new chat. One page per chat. Paste this and replace the bracket:

```
Use the felix-page-accessibility skill on [page name or path].
Félix - Main only. Change the Designer. Do not publish.
```

For English or Portuguese, name the locale in the same sentence: `on /en/refer-app, English locale.`

The reply starts with a table of every change: the element or class, where it lives, the value before, and the value after. Check those changes in the Designer before anyone publishes. Shared components and shared classes affect other pages.

Then publish the page yourself, check the keyboard, and run ANDI on the live URL. The page is done when the checklist passes, the keyboard path is clean, and ANDI shows no Danger alerts.

## Running `webflow-mcp:accessibility-audit` (headless audit)

Use this for a fast WCAG 2.1 audit report without connecting to the Webflow Designer. Start a new chat and paste:

```
Use the webflow-mcp:accessibility-audit skill on [page name, path, or page ID] on Félix - Main.
Run a full audit and show the report before making any changes. Do not publish.
```

You can also narrow or expand the scope in your prompt:

- **Critical issues only (WCAG Level A):** replace `Run a full audit` with `Check critical issues only`.
- **Multiple pages:** list several pages or ask the skill to list available pages first.
- **After the report:** approve specific attribute fixes (`all`, specific item numbers, or `none`) or ask to export the report as Markdown, JSON, or CSV.

Because this skill skips image alt text and color contrast, use `felix-page-accessibility` (plus manual keyboard and ANDI checks after publishing) before marking a Félix Main page done.
