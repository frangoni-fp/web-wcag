---
name: felix-page-accessibility
description: >-
  Audits and fixes one Félix Main Webflow page for the Compliance accessibility
  requirements, then rechecks and repeats until the Designer checks pass. Use
  when a developer asks to make a single felixpago.com page or CMS template
  accessible, run the page accessibility skill, or fix WCAG issues on one
  Webflow page. One page per run. Never publishes.
---

# One-page accessibility fix

Fix one page on **Félix - Main** (`663002023d3d42ffa6937084`, felixpago.com). Audit it, change only what fails, read it back, and repeat until the Designer checks in [checklist.md](checklist.md) pass or a stop rule fires.

The standard is WCAG 2.1 Level AA. The five requirements are text alternatives, keyboard access, 4.5:1 text contrast (3:1 for large text, icons, borders, and text on a photo), captions or a transcript for media, and form fields with a visible label and a clear error. Headings, buttons, links, and labels must be real ones, in an order a screen reader can follow.

## Scope

- One page or one CMS template per run. If several are named, do the first and stop. Do not walk the site, a folder, or a collection.
- Félix - Main only. Do not open Félix - GET or Félix Checkout.
- On a CMS template, fix the template. Include one CMS item only when the developer names that item. Do not update the rest of the collection.
- Default locale is Spanish. Check English or Portuguese only when that locale is named.
- A class or component used on other pages (menu, footer, skip link, a shared button style) may be fixed once. Say that the change is shared. Do not add a second skip link or a second focus style on the page.

## Do not publish

Save changes in the Designer. Do not publish the site, a page, a branch, a staging domain, or a CMS item. Do not call a publish action on `data_sites_tool`, `data_pages_tool`, or `data_cms_tool`.

Do not change the slug, draft flag, folder, or page title except to fill an empty page title. Do not create or delete pages. Do not remove elements. Do not rewrite marketing copy. Link text changes only when the name is empty or is only “click here”, “read more”, or the Spanish or Portuguese equivalent, and the destination is already on the link.

## Tools

Use the Webflow MCP. Call `webflow_guide_tool` once at the start. Read a tool schema before the first call to that tool. Every call needs `context` (15–25 words, third person), `session_id` (`start` on the first call, then the returned `ses_` value), and a stable `agent_id`.

| Tool | Use it for |
| --- | --- |
| `designer_tool` | `switch_page` to this page. `open_component_view` only to fix a shared component, then close it. |
| `data_element_tool` | `query_elements` for Heading, Image, Link, Button, FormForm, FormTextInput, FormSelect, FormTextarea. Then `get_attributes`, `set_attributes`, `set_heading_level`, `set_text`, `set_link`. |
| `element_snapshot_tool` | See an image before writing its alt text. |
| `data_style_tool` | `query_styles` for the classes on this page, including `focus` and `focus-visible`. `update_style` for contrast and a visible focus style. |
| `data_pages_tool` | `get_page_metadata` for the page title and locale. `list_pages` only to resolve the one named page. |

Copy element ids as `{ component, element }` from the tool result. Do not shorten them.

`get_all_elements` on a full page is too large. Query by type, in batches of 50.

## Loop

1. Confirm the page name or path. If it is missing, ask for one page and stop.
2. Open that page in the Designer. If the Designer is not connected, stop and ask the developer to open Félix - Main in the Designer.
3. Audit against [checklist.md](checklist.md). Record each failure with the element id, what is wrong, and the fix.
4. Apply the fixes. Prefer an attribute, a heading level, existing label text, or a class color. Leave anything the checklist marks as a human check.
5. Read back only the elements and styles just changed.
6. Repeat from step 3.

Stop when every Designer check passes, or after 3 full passes, or when the same failure is still there after a second attempt. A repeated failure is blocked. Report it. Do not keep editing it.

## Fix rules

- **Images.** Look at the snapshot first. A meaningful image gets alt text that describes what is in the picture. A decorative image gets `alt=""`. If the snapshot is unclear, do not invent a description. Report it.
- **Contrast.** Compute a ratio only when both colors are solid. Text needs 4.5:1. Icons, borders, and text on a photo need 3:1. Text on a photo gets a solid background behind the words. Do not guess a ratio off an image. A shared class color change must be named in the report.
- **Focus.** If a link or button class sets `outline: none` and has no other focus style, add a visible `focus-visible` outline on that class.
- **Forms.** The visible label is the label. Placeholder text is not. Use `aria-label` only when no label element exists, and still report that a visible label is missing. Do not invent error copy. If the Designer has no error state, leave it for the developer.
- **Headings.** Close skipped levels with `set_heading_level`. Do not change the words.
- **Names.** An icon button or icon link needs a name, for example “Félix on Instagram”. Do not put the word “button” or “graphic” inside the name.
- **Keyboard structure.** `tabindex` greater than 0 goes to `0` or is removed. A div that acts as a button gets `role="button"` and `tabindex="0"`, and the report says a real button is the better fix. Do not add custom code.
- **Media.** If a video is set to autoplay, turn autoplay off when the element setting allows it. Captions and transcripts that are not already on the page are a human check. Do not write them.
- **Iframes.** An iframe with no title has no accessible name. Add a `title` on the `<iframe>` itself. Use the heading or label already next to it. Do not describe footage that was not seen, and do not put the word “iframe” in the title. Leave `src`, autoplay, loop, and muted untouched while adding the title. A background iframe that is only decoration, with the same information already in text, gets `aria-hidden="true"` and `tabindex="-1"` instead of a title. Say which choice was made in the QA list.
- **Motion.** Anything that can flash, parallax, or scrolljack is a human check. The limit is 3 flashes in any one second (2.3.1). Do not claim it is clear from the element tree.
- **Widgets.** A custom control needs a name, a role, and a state (4.1.2). The visible label is the start of the accessible name (2.5.3). Do not invent a state that is not in the element tree.
- **Messages.** A result that appears without a page load, such as a rate or an error, needs a status announcement (4.1.3). If the Designer has no live region, report it as a human check. Do not invent the announcement.
- **Money and time.** A form that submits a transfer, a payment, a legal commitment, or a deletion must allow review, correction, or confirmation before it is final (3.3.4). A time limit must be adjustable unless it is essential (2.2.1). Both are human checks. Do not build a new confirmation step.
- **Language of parts.** A passage in a different language from the page needs that language set on the element (3.1.2). Do not guess the language from a proper name.

## Report

End every run with the change list first, so the developer can QA it. Include only writes that succeeded. If a write was not made, do not list it as a change. Say “No other Designer writes” after the list. Call out video, autoplay, and shared components by name when they were not written, if the developer might think they were.

```
Page: [name] · [path] · [locale]
Designer: clean | blocked
Passes: 1–3

Changes for QA
| Element or class | Where | Before | After |
| --- | --- | --- | --- |
| [name] | This page, or Shared: [component or class] | [previous value] | [new value] |

No other Designer writes.

Blocked
- [element] — [why a second attempt did not clear it]

Human check, after the developer publishes
- Keyboard: Tab, Shift+Tab, Enter, Space, Escape. Focus visible and in visual order.
- ANDI on the live URL: no Danger alerts. This skill does not publish, so ANDI was not run.
- [any caption, transcript, error state, or contrast-on-photo left open]
```

Do not say the page is accessible on the live site. Designer-clean means the checks in [checklist.md](checklist.md) passed in the Designer.
