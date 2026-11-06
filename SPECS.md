# AgentHub Admin Panel — Specification

This document is the contract for the admin panel prototype. An implementer should be able to build the panel from this file alone. Do not add a backend, a build step, or a framework.

## 1. Product

AgentHub is a SaaS platform where companies rent preconfigured AI agents. Each agent can have skills enabled (capabilities such as browsing the web, reading documents, or managing a calendar) and is deployed for a client's business tasks.

The person using this screen is an AgentHub internal administrator. They review revenue, client accounts, rented agents, the skill catalog, rental contracts, and agent execution errors. They do not edit billing rules or call an API in this prototype. Every figure and record is hardcoded.

The interface is in English.

## 2. Tech stack and constraints

- One file, `index.html`, at the repository root. Structure, Tailwind configuration, and behavior all live in that file.
- Styling uses Tailwind CSS loaded only from `https://cdn.tailwindcss.com`. The page sets `tailwind.config` with `darkMode: "class"` so `dark:` utilities follow the `dark` class on `<html>`. The same config holds the color tokens in section 5 and the font families in the next bullet. There is no other theme.
- No custom CSS file. No `<style>` block. No `style` attribute anywhere in `index.html`.
- Behavior uses one vanilla JavaScript block at the end of `index.html`. No React, Vue, jQuery, Alpine, or other library. No bundler and no npm build.
- No network calls for data. No form is submitted. No live search.
- Fonts are set in `theme.extend.fontFamily` and are not loaded from a font CDN. `font-sans` is `Arial, Helvetica, sans-serif` and is the UI face (`font-sans` on `body`). `font-mono` is `Consolas, "Courier New", monospace` and is used only for the system-prompt textarea and the error trace. Title elements (`h1`, `h2`, `h3`, and the top-bar section title) use `font-bold` (700).
- Icons are inline SVG (Heroicons-style outline, 24×24, `stroke="currentColor"`, `fill="none"`). Do not use an icon font or an image for icons.
- Local preview may use the template `server.py` (Flask, port 3000). The panel must also open correctly from a static file server.

## 3. Information architecture

The panel is one page with six sections. Only one section is visible at a time.

| Section id | Nav label | Hash |
| --- | --- | --- |
| `dashboard` | Dashboard | `#dashboard` |
| `users` | User Management | `#users` |
| `agents` | Agent Management | `#agents` |
| `skills` | Skills | `#skills` |
| `contracts` | Agent Contracts | `#contracts` |
| `errors` | Error Log | `#errors` |

Default section when the hash is empty or unknown: Dashboard.

Navigation uses real links (`<a href="#users">` and so on) inside a `<nav>`. JavaScript intercepts the click, does not reload the page, shows the matching `<section>`, updates the hash with `history.replaceState`, moves keyboard focus to that section's `<h2>` (`tabindex="-1"`), and scrolls the window to the top. On `DOMContentLoaded` and on `hashchange`, the visible section follows the hash.

Switching sections closes any open dropdown, any open modal, and the mobile sidebar.

## 4. Layout

```text
+------------------+--------------------------------------+
| Sidebar (sticky) | Top bar (sticky): title + theme      |
| Brand + nav      | Main: the active section only        |
+------------------+--------------------------------------+
```

- Semantic skeleton: `header` (top bar), `nav` (inside `aside`), `main`, and one `section` per view. Listings that are tabular use `table`, `thead`, `tbody`, `tr`, `th` (with `scope="col"`), and `td`. Each table has a `caption` with the class `sr-only`. Agent entries and skill entries are `article` elements. The skill explanation is an `aside`.
- Page background: `bg-canvas` (`#F7F8FA`) in light mode, `dark:bg-canvas-dark` (`#10151C`) in dark mode. Text: `text-ink` (`#18202B`) / `dark:text-ink-dark` (`#F7F8FA`).
- Sidebar: dark in both themes. Light mode uses `bg-ink` (`#18202B`); dark mode uses `dark:bg-sidebar-dark` (`#0C1117`). The `h1` and idle nav links use `text-canvas` (`#F7F8FA`). The secondary lines ("Admin panel", "Prototype · no backend") use `text-subtle` (`#E7ECF2`). Width 15rem, full height, sticky. It stays on screen at the `md` breakpoint and up (≥768px). Below 768px it is off-canvas and slides in when the top-bar Menu button is pressed. A backdrop (`bg-overlay`, `rgba(0,0,0,.56)`) covers the page while the off-canvas sidebar is open; clicking the backdrop or a nav link closes it. The sidebar is translated with Tailwind classes (`-translate-x-full` and `translate-x-0`), not inline styles. Its border is `border-border` (`#788598`) in both themes.
- Top bar: `bg-surface` (`#FFFFFF`) / `dark:bg-surface-dark` (`#1B2430`), bottom border `border-border` / `dark:border-border-dark` (`#9AA7B8`), sticky, `z-20`. Left side: Menu button (visible only below `md`) and the current section title (the same words as the nav label) in an element that is not the page `h1`. The single `h1` is the word "AgentHub" in the sidebar. Right side: the theme toggle. Text on the bar is `text-ink` / `dark:text-ink-dark`.
- Main padding: `p-4` below `md`, `p-6` from `md` up. Content is `min-w-0` so tables can scroll instead of widening the page.
- Tables sit in a `overflow-x-auto` wrapper. On a 768px viewport the sidebar and the active section are both usable without overlapping; wide tables scroll horizontally inside the wrapper.
- On a 1280px viewport the four metric cards sit on one row. From 640px to 1279px they are a 2×2 grid. Below 640px they stack in one column.
- Cards, menus, and the modal panel use `rounded-xl`, a 1px `border-border` / `dark:border-border-dark` border, `bg-surface` / `dark:bg-surface-dark`, and `shadow-sm`.
- Focusable controls use `focus-visible:outline-none` and a 2px ring with a 2px offset. On light content surfaces the ring is `focus` (`#164DCC`) and the offset is `surface`. In dark mode those controls use `ring-canvas` (`#F7F8FA`) and offset `surface-dark`, because `#164DCC` is below 3:1 on the dark surfaces. Sidebar links use `ring-canvas` in both themes, with offset `ink` in light mode and `sidebar-dark` in dark mode.
- The footer under `main` stays `bg-surface` (`#FFFFFF`) in both themes, with a `border-border` top rule and `text-muted` (`#505E70`). It is the lockup plate and is not switched to a dark token.
- A visually hidden `aria-live="polite"` region (`#action-status`, class `sr-only`) announces deletes and resolve actions.

## 5. Color and badges

Every color in `index.html` is one of the tokens below, declared in `tailwind.config` under `theme.extend.colors`. Light tokens are the SIGNAL set. Dark tokens exist because this prototype must keep a `dark:` theme; SIGNAL does not define them. No other hex value is used.

| Token | Value | Use |
| --- | --- | --- |
| `canvas` | `#F7F8FA` | Light page background. Also the light text on the dark sidebar (`text-canvas`) and the focus ring on dark surfaces and on the sidebar (`ring-canvas`). Idle nav hover is `hover:bg-canvas/10` (the same color at 10% opacity). |
| `surface` | `#FFFFFF` | Light cards, top bar, menus, modal panel, tables, chart placeholder, and the footer in both themes. Also the light focus-ring offset. |
| `ink` | `#18202B` | Light body text, and the sidebar background in light mode (`bg-ink`). Also the light focus-ring offset on sidebar links, and the code-trace background (`bg-ink`) with `text-canvas`. |
| `muted` | `#505E70` | Secondary text on light surfaces: descriptions, table headers, the `⋮` trigger, and the footer credit. |
| `border` | `#788598` | 1px borders and dividers on light surfaces, and the sidebar border in both themes. |
| `subtle` | `#E7ECF2` | Light hover fill, skill-name pills, and the neutral badge background. Also the secondary sidebar text (`text-subtle`). |
| `action` | `#B53A17` | Active nav link and the sidebar mark, with `on-action` text. |
| `on-action` | `#FFFFFF` | Text on `action`. |
| `action-hover` | `#8F2D12` | Declared in the config. No control uses it. |
| `action-pressed` | `#73230E` | Dark-mode hover of the Delete item (`dark:hover:bg-action-pressed`). |
| `selected` | `#FCEDE6` | Light hover of Delete, the skill-explanation background, and the noscript notice background. |
| `focus` | `#164DCC` | Focus ring on light content controls only. |
| `danger` | `#A32A26` | Delete text in light mode. Solid badge and dark-mode Delete fill. |
| `success` | `#236344` | Solid badge and the Total revenue icon tile. |
| `warning` | `#765000` | Solid badge, the Discount losses icon tile, and the noscript border. |
| `info` | `#204EA0` | Solid badge and the Active agents icon tile. |
| `on-status` | `#FFFFFF` | Text on `success`, `warning`, `danger`, and `info` fills, including the metric icon tiles. |
| `link` | `#B53A17` | Declared in the config. Same value as `action`. No control uses it. |
| `overlay` | `rgba(0,0,0,.56)` | Sidebar backdrop and modal backdrop (`bg-overlay`). |
| `canvas-dark` | `#10151C` | Dark page background. |
| `surface-dark` | `#1B2430` | Dark cards, top bar, menus, modal panel, tables, and chart placeholder. Also the dark focus-ring offset on content controls. |
| `ink-dark` | `#F7F8FA` | Text on dark surfaces. Same hex as `canvas`. |
| `muted-dark` | `#C5D0DC` | Secondary text on dark surfaces. |
| `border-dark` | `#9AA7B8` | Borders and dividers on dark content surfaces. |
| `subtle-dark` | `#2A3646` | Dark hover fill, dark skill pills, and the dark neutral badge. |
| `sidebar-dark` | `#0C1117` | Sidebar background in dark mode, and the dark focus-ring offset on sidebar links. |

Status and type badges are pills: `inline-flex`, `rounded-full`, `px-2 py-0.5`, `text-xs`, `font-medium`. Solid status badges use the same classes in both themes.

| Token | Classes | Used for |
| --- | --- | --- |
| `success` | `bg-success text-on-status` | Active, Resolved |
| `warning` | `bg-warning text-on-status` | Suspended, Authentication, Rate limit, Empty response |
| `danger` | `bg-danger text-on-status` | Failing, Timeout, Tool failure |
| `info` | `bg-info text-on-status` | Parse error |
| `subtle` | `bg-subtle text-ink` and `dark:bg-subtle-dark dark:text-ink-dark` | Inactive, Ended, Configuration |

Metric icon tiles use `text-on-status` on a solid fill:

| Metric | Tile |
| --- | --- |
| Total revenue | `bg-success` |
| Discount losses | `bg-warning` |
| Active agents | `bg-info` |
| Failing agents | `bg-danger` |

The active nav item is `bg-action text-on-action`. The skill explanation is `bg-selected` with `border-border` and `text-ink` (`dark:bg-subtle-dark`, `dark:border-border-dark`, `dark:text-ink-dark`). The failing-agents icon tile is the only `bg-danger` on the dashboard.

## 6. Shared behaviors

### 6.1 Action dropdown

Every repeated entry (each user row, agent card, skill card, contract row, and error row) has one actions control.

- The trigger is a `button type="button"` whose visible label is the character `⋮`. `aria-haspopup="menu"`, `aria-expanded` is `true` only while open, and `aria-label` is `Actions for {record name}`.
- The menu is a sibling `div` with `role="menu"`, `w-44`, hidden when closed. In the markup it is absolutely positioned to the right edge of the trigger (`right-0 z-30 mt-1`). While it is open, script moves it to `document.body` and places it with fixed Tailwind classes, right-aligned to the trigger. It opens above the trigger when there is room, so it does not cover the next row's action button; otherwise it opens below. Items are `button type="button"` with `role="menuitem"`, full width, left aligned, `text-sm`.
- Clicking the trigger toggles that menu and closes every other menu.
- Clicking anywhere outside the dropdown closes every menu.
- Choosing an item runs the action and closes the menu.
- Menu contents:
  - Users, skills, contracts, errors: "View detail" then "Delete", except errors, which use "View detail" then "Mark as resolved".
  - Agents: "Configure" then "Delete".

### 6.2 Modal

One modal shell is reused.

- Root: `#modal-root`, `hidden` when closed, `fixed inset-0 z-50 flex items-center justify-center bg-overlay p-4`.
- Panel: `role="dialog"`, `aria-modal="true"`, `aria-labelledby="modal-title"`, `w-full max-w-2xl max-h-[85vh] overflow-y-auto`, surface colors `bg-surface` / `dark:bg-surface-dark`.
- Header row: `h2#modal-title` and a `button type="button"` labeled "Close" (`data-modal-close`).
- Body: `#modal-body`.
- Opening a modal closes dropdowns and the mobile sidebar, removes the `hidden` attribute, sets `document.body` to `overflow-hidden`, and focuses the Close button.
- The modal closes when the user activates Close, and when the user clicks the backdrop. A click closes on backdrop only when `event.target === modalRoot`. Clicks inside the panel do not close it.
- Closing restores `hidden`, removes `overflow-hidden`, and returns focus to the control that opened the modal.
- "View detail" opens this modal in four sections: User Management, Skills, Agent Contracts, and Error Log. "Configure" opens it from Agent Management. Delete and Mark as resolved do not open it.

### 6.3 Delete and resolve

These actions change only the current page. Nothing is stored.

- Delete removes that entry's `tr` or `article` from the DOM and sets `#action-status` to `Deleted {name}.`
- Mark as resolved replaces the error type badge text with `Resolved` and switches the badge to the success classes in section 5. The "Mark as resolved" item becomes `disabled` and its text becomes `Resolved`. `#action-status` becomes `Marked {agent name} error as resolved.`

### 6.4 Collapsible skill list

Each agent card contains one collapsible region, collapsed by default.

- Trigger: `button type="button"`, `aria-expanded="false"`, `aria-controls` pointing at the region id (`skills-atlas`, `skills-ledger`, `skills-inbox`, `skills-field`, `skills-compliance`). Visible text: `Skills` and the count.
- Panel: CSS grid with `grid-rows-[0fr]` when collapsed and `grid-rows-[1fr]` when open. Class includes `transition-[grid-template-rows] duration-300 ease-in-out motion-reduce:transition-none`. The inner wrapper is `overflow-hidden`. The open list is a `ul` of skill names as small pills, with `pt-3` so the expand animation reveals them.
- A chevron SVG on the trigger has `transition-transform duration-300 motion-reduce:transition-none` and gains `rotate-180` while expanded.
- Clicking the trigger toggles `aria-expanded` and the grid class. Clicking again collapses the list. No other agent is forced open or closed.

### 6.5 Dark mode

- The toggle is a `button type="button"` in the top bar, `#theme-toggle`.
- Light mode (no `dark` class on `<html>`): the button shows a moon icon and the word `Dark`. `aria-label` is `Switch to dark mode`. `aria-pressed` is `false`.
- Dark mode (`class="dark"` on `<html>`): the button shows a sun icon and the word `Light`. `aria-label` is `Switch to light mode`. `aria-pressed` is `true`.
- Every surface listed in this spec includes `dark:` classes: page, top bar, cards, tables, dropdowns, modal, badges, borders, muted text, chart placeholder, and form control.
- The class lives on `<html>`, so choosing a mode and then following a sidebar link keeps that mode. Section changes must not remove the class.
- A script in `<head>` reads `localStorage` key `agenthub-theme` (`light` or `dark`) before the body paints. If the key is missing, it uses `prefers-color-scheme`. The toggle writes the same key, so a reload keeps the choice.

### 6.6 Configure textarea

The Configure modal shows the agent name in the title (`Configure Atlas Research`), the owner line, the status badge text, and a `label` "System prompt" associated with a `textarea`. The textarea is editable (no `readonly`, no `disabled`), uses `rows="8"`, `w-full`, border, padding, and `font-mono text-sm`. Helper text under it: `Edits stay in this browser session only.` If the admin edits the text, closes the modal, and opens Configure on the same agent again, the edited text is still there.

## 7. Hardcoded data

November 2026 is the reporting month. Money is USD, shown with a dollar sign and thousands separators (`$5,200`). Dates use `YYYY-MM-DD`.

### 7.1 Dashboard arithmetic

Recognized revenue this month is one month of fees from contracts that cover November 2026:

- Atlas Research, CTR-1042: $1,600
- Ledger Clerk, CTR-1048: $1,500
- Compliance Watch, CTR-1102: $2,100

Inbox Triage (ended 2026-10-31) and Field Notes (ended 2026-08-31) contribute $0. Total revenue = **$5,200**.

Discount and coupon losses this month = **$480**: a 10% Northwind coupon on the Atlas month ($160) plus a Lumen Labs commit credit ($320).

Active agents (status Active) = **3** (Atlas Research, Ledger Clerk, Compliance Watch). Failing agents = **1** (Inbox Triage).

### 7.2 Users

| id | Name | Email | Plan | Status | Company | Joined | Agent |
| --- | --- | --- | --- | --- | --- | --- | --- |
| user-elena | Elena Vargas | elena.vargas@northwind.io | Business | Active | Northwind Analytics | 2025-11-02 | Atlas Research |
| user-marcus | Marcus Chen | marcus.chen@lumenlabs.com | Enterprise | Active | Lumen Labs | 2025-06-18 | Ledger Clerk |
| user-priya | Priya Shah | priya.shah@orbitmail.co | Pro | Active | Orbit Mail | 2026-01-09 | Inbox Triage |
| user-jonah | Jonah Adler | jonah.adler@fieldnote.dev | Starter | Suspended | Fieldnote | 2025-04-22 | Field Notes |
| user-amira | Amira Hassan | amira.hassan@cedarops.com | Business | Active | Cedar Ops | 2025-09-30 | Compliance Watch |
| user-luis | Luis Ortega | luis.ortega@picoform.io | Pro | Inactive | Picoform | 2026-02-14 | None |

Jonah's modal note: `Suspended because the last payment failed.` Luis's modal note: `Account is inactive and has no rented agent.` Other users' note: `Account in good standing.`

The users table shows Name, Email, Plan, and Status. Company, Joined, Agent, and Note appear in the View detail modal.

### 7.3 Skills

| id | Name | Description | Enabled on |
| --- | --- | --- | --- |
| skill-browse | Web Browse | Opens public web pages and extracts visible text. It cannot log in or submit forms. | 3 — Atlas Research, Inbox Triage, Compliance Watch |
| skill-docs | Document Read | Reads PDF and text documents supplied by the client and quotes passages with page numbers. | 4 — Atlas Research, Ledger Clerk, Field Notes, Compliance Watch |
| skill-calendar | Calendar | Reads busy time and proposes events. It cannot invite attendees. | 2 — Atlas Research, Field Notes |
| skill-email | Email Draft | Drafts email text. Sending stays with the client. | 1 — Inbox Triage |
| skill-sheet | Spreadsheet | Reads tabular files and computes sums, averages, and mismatches. | 1 — Ledger Clerk |
| skill-policy | Policy Check | Scores a document against a fixed checklist and returns pass or fail per item. | 1 — Compliance Watch |

The card shows the description and the sentence `Enabled on {n} agent` when the count is 1, or `Enabled on {n} agents` otherwise. The modal repeats the description, the count, and the agent names as a list.

### 7.4 Agents

| id | Name | Owner | Company | Status | Skills |
| --- | --- | --- | --- | --- | --- |
| atlas | Atlas Research | Elena Vargas | Northwind Analytics | Active | Web Browse, Document Read, Calendar |
| ledger | Ledger Clerk | Marcus Chen | Lumen Labs | Active | Document Read, Spreadsheet |
| inbox | Inbox Triage | Priya Shah | Orbit Mail | Failing | Email Draft, Web Browse |
| field | Field Notes | Jonah Adler | Fieldnote | Inactive | Document Read, Calendar |
| compliance | Compliance Watch | Amira Hassan | Cedar Ops | Active | Web Browse, Document Read, Policy Check |

Owner line on the card: `{Owner} · {Company}`.

System prompts (initial textarea values):

- Atlas Research: `You are Atlas Research, a research assistant for Northwind Analytics. Use Web Browse and Document Read to gather sources, and Calendar to propose briefing slots. Never invent citations. Summarize findings with dates and links. Ask before any external message.`
- Ledger Clerk: `You are Ledger Clerk for Lumen Labs. Read invoices and spreadsheets, reconcile totals, and flag mismatches. Do not change source files. Report amounts in USD with two decimals.`
- Inbox Triage: `You are Inbox Triage for Orbit Mail. Draft replies and classify mail. Never send email. Use Web Browse only to check public status pages linked by the customer.`
- Field Notes: `You are Field Notes for Fieldnote. Turn site notes into structured visit reports and suggest follow-up calendar holds. This agent is inactive and must not run jobs.`
- Compliance Watch: `You are Compliance Watch for Cedar Ops. Compare draft policies with the checklist skill and cite the clause that failed. Do not approve a document that fails Policy Check.`

### 7.5 Contracts

Amount paid = monthly fee × months billed. The modal lists each skill's monthly price. The sum of those prices equals the monthly fee.

| id | Client | Agent | Skills (monthly price) | Start | End | Months billed | Amount paid | Contract status |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CTR-1042 | Northwind Analytics | Atlas Research | Web Browse $400, Document Read $900, Calendar $300 | 2026-09-01 | 2026-11-30 | 3 | $4,800 | Active |
| CTR-1048 | Lumen Labs | Ledger Clerk | Document Read $800, Spreadsheet $700 | 2026-08-01 | 2026-11-30 | 4 | $6,000 | Active |
| CTR-0988 | Orbit Mail | Inbox Triage | Email Draft $600, Web Browse $500 | 2026-10-01 | 2026-10-31 | 1 | $1,100 | Ended |
| CTR-1102 | Cedar Ops | Compliance Watch | Web Browse $400, Document Read $900, Policy Check $800 | 2026-07-01 | 2027-01-31 | 5 | $10,500 | Active |
| CTR-0904 | Fieldnote | Field Notes | Document Read $400, Calendar $300 | 2026-06-01 | 2026-08-31 | 3 | $2,100 | Ended |

The table shows Client, Agent, contracted skill names separated by commas, Start, End, and Amount paid. Contract status is a badge in the table as well.

The View detail modal shows the contract id as the title (`Contract CTR-1042`), client, agent, start, end, status, months billed, a table with columns Skill and Monthly price, the monthly fee, and the amount paid.

### 7.6 Error log

| id | Timestamp | Agent | Type | Badge | Description |
| --- | --- | --- | --- | --- | --- |
| err-1 | 2026-11-05 14:22 UTC | Inbox Triage | Timeout | danger | Web Browse exceeded 30s on status.orbitmail.co. |
| err-2 | 2026-11-05 09:03 UTC | Inbox Triage | Authentication | warning | Email Draft token was rejected by the client mailbox. |
| err-3 | 2026-11-04 18:47 UTC | Atlas Research | Rate limit | warning | Web Browse hit 60 requests/hour for Northwind public docs. |
| err-4 | 2026-11-04 11:16 UTC | Ledger Clerk | Parse error | info | Spreadsheet skill could not read sheet Q4-accruals. |
| err-5 | 2026-11-03 16:02 UTC | Compliance Watch | Tool failure | danger | Policy Check returned an empty checklist. |
| err-6 | 2026-11-02 08:28 UTC | Field Notes | Configuration | subtle | Calendar skill is disabled because the agent is inactive. |
| err-7 | 2026-11-01 19:40 UTC | Inbox Triage | Empty response | warning | Email Draft returned no body for thread ORB-441. |

Traces, shown in `pre` with `whitespace-pre-wrap font-mono text-xs` inside the modal:

- err-1: `TimeoutError: Web Browse exceeded 30000ms` / `url: https://status.orbitmail.co` / `agent: Inbox Triage` / `skill: Web Browse`
- err-2: `AuthError: mailbox token rejected` / `provider: orbit-mail` / `agent: Inbox Triage` / `skill: Email Draft`
- err-3: `RateLimitError: 60 requests/hour` / `host: docs.northwind.io` / `agent: Atlas Research` / `skill: Web Browse`
- err-4: `ParseError: unknown sheet Q4-accruals` / `file: lumen-q4.xlsx` / `agent: Ledger Clerk` / `skill: Spreadsheet`
- err-5: `ToolFailure: checklist payload was empty` / `agent: Compliance Watch` / `skill: Policy Check`
- err-6: `ConfigError: agent status is inactive` / `agent: Field Notes` / `skill: Calendar`
- err-7: `EmptyResponse: draft body length 0` / `thread: ORB-441` / `agent: Inbox Triage` / `skill: Email Draft`

The modal also repeats timestamp, agent, type, and description.

The same agent names Atlas Research, Ledger Clerk, Inbox Triage, Field Notes, and Compliance Watch appear in Agent Management, Agent Contracts, and Error Log.

## 8. Section specifications

### 8.1 Dashboard

1. Four metric cards in a responsive grid (1 column, then 2×2 from 640px, then 4 columns from 1280px). Each card contains an SVG icon in a tinted tile, the label (Total revenue, Discount losses, Active agents, Failing agents), the sublabel (This month, Coupons and credits, Across all clients, Needs attention), and the hardcoded value from section 7.1. Cards use distinct accent tiles and `shadow-sm`.
2. The values are exactly `$5,200`, `$480`, `3`, and `1`. A line under the grid reads `November 2026 · hardcoded prototype`.
3. Below the cards, a full-width placeholder (`h-64`, dashed 2px border, centered) represents the weekly activity chart. It contains the label `Weekly activity chart` and the sentence `Chart data is not connected in this prototype.` It has `role="img"` and `aria-label="Weekly activity chart placeholder"`.

### 8.2 User Management

1. A table of the six users in section 7.2, columns Name, Email, Plan, Status, Actions. Status is a badge. Plan is plain text.
2. Each row's `⋮` menu contains View detail and Delete. View detail opens the modal with name, email, plan, status, company, joined date, assigned agent, and the note from section 7.2.
3. The modal closes from the Close button and from a click on the backdrop. Delete removes only that row.

### 8.3 Agent Management

1. A vertical list of five `article` cards, one per agent in section 7.4, in that order. Each card shows the agent name, the owner line, a status badge, and a skill region that is collapsed when the page loads.
2. The expand control reveals that agent's skill names with the 300ms grid-row transition. Activating it again collapses the list. The control's `aria-expanded` value matches the visible state.
3. Each card's `⋮` menu contains Configure and Delete. Configure opens the modal with that agent's system prompt in an editable textarea, following section 6.6.

### 8.4 Skills

1. An `aside` at the top of the section explains what a skill is. Heading: `What is a skill?` Body: `A skill is a capability that can be attached to an agent — for example browsing the web, reading documents, or managing a calendar. A skill does not run by itself. It becomes available only when an agent has it enabled and a contract includes it.`
2. A responsive catalog (one column, two columns from `md`) of six articles. Each article shows the skill name, the description, and the enabled-agent sentence from section 7.3. Counts of 1 use `agent`; every larger count uses `agents`.
3. Each article's `⋮` menu contains View detail and Delete. View detail opens the modal with the description, the count, and the list of agent names.

### 8.5 Agent Contracts

1. A table of the five contracts in section 7.5 with columns Client, Agent, Contracted skills, Start, End, Amount paid, Status, and Actions.
2. Each row's `⋮` menu contains View detail and Delete.
3. View detail opens the modal with the itemized skill table and each skill's monthly price, plus months billed, monthly fee, and amount paid. The itemized prices for CTR-1042 are Web Browse $400, Document Read $900, and Calendar $300.

### 8.6 Error Log

1. A table of the seven errors in section 7.6 with columns Timestamp, Agent, Type, Description, and Actions. Type is a color-coded badge using the badge column of that table.
2. Each row's `⋮` menu contains View detail and Mark as resolved. View detail opens the modal with the full trace for that id.
3. Mark as resolved updates the badge to the success Resolved state defined in section 6.3 and does not open the modal.

## 9. Component inventory

| Component | Role | Where it is used | States |
| --- | --- | --- | --- |
| Sidebar | Persistent navigation (`aside` + `nav`) | Every section | Current link active; off-canvas closed or open below 768px |
| Top bar | Section title and theme toggle (`header`) | Every section | Title matches the open section |
| Metric card | Icon, label, sublabel, value | Dashboard only | Four accent colors |
| Data table | Tabular records | Users, contracts, errors | Horizontal scroll on narrow widths |
| Status badge | Color pill | Users, agents, contracts, errors | See section 5 |
| Action dropdown | `⋮` menu | Every user, agent, skill, contract, and error | Closed; open; resolved item disabled |
| Modal | Overlay dialog | Users, agents (Configure), skills, contracts, errors | Closed; open |
| Collapsible skill list | Expand/collapse region | Each agent card | Collapsed by default; expanded |
| Dark mode toggle | Class toggle on `<html>` | Top bar | Light (`Dark` label); dark (`Light` label) |
| Chart placeholder | Non-interactive dashed region | Dashboard | Static |
| Skill explanation | `aside` copy block | Skills | Static |

## 10. Acceptance criteria

1. `index.html` is the only UI file and loads Tailwind from `https://cdn.tailwindcss.com` with `darkMode: 'class'`.
2. `index.html` contains no `style` attribute and the repository contains no stylesheet written for this panel.
3. The page contains `header`, `nav`, `main`, six `section` elements, and at least one `table`.
4. The sidebar lists Dashboard, User Management, Agent Management, Skills, Agent Contracts, and Error Log. Activating a link shows only that section and marks the link with `aria-current="page"`.
5. At 1280×800 the sidebar is visible without the Menu button and the four metric cards are on one row. At 768×1024 the sidebar is still visible and the metric cards wrap to two columns. At 390×844 the sidebar is hidden until Menu is pressed, and tables scroll inside their wrapper.
6. The Dashboard shows `$5,200`, `$480`, `3`, and `1` with the labels Total revenue, Discount losses, Active agents, and Failing agents, each with an SVG icon.
7. The Dashboard shows a full-width dashed placeholder whose text includes `Weekly activity chart`.
8. User Management renders six users with email, plan, and a status badge. Each row has a `⋮` menu with View detail and Delete.
9. View detail on a user opens a modal that contains the email and the company. The Close button hides it. A click on the backdrop hides it. A click on the panel does not.
10. Agent Management renders five agents. On load, each skill list is collapsed (`aria-expanded="false"` and no skill pill visible). Activating the control reveals the skill names with a non-zero grid-template-rows transition, and activating it again collapses them.
11. Configure on Atlas Research opens a modal whose textarea value starts with `You are Atlas Research` and is not read-only.
12. The Skills section shows the heading `What is a skill?` and six skills. Web Browse reads `Enabled on 3 agents`. Document Read reads `Enabled on 4 agents`. Each skill has View detail and Delete.
13. Agent Contracts renders five rows. The Atlas row shows Northwind Analytics, Atlas Research, and `$4,800`. View detail shows Document Read and `$900` in the itemized breakdown.
14. Error Log renders seven rows. Timeout uses the danger badge, Rate limit uses the warning badge, and Configuration uses the subtle badge. View detail on the first row shows `TimeoutError`.
15. Mark as resolved on an error changes that badge text to `Resolved` and does not open the modal.
16. Delete on Luis Ortega removes that user's row and leaves the other users in place.
17. Opening any `⋮` menu and then clicking outside it closes the menu. Opening a second menu closes the first.
18. Activating the theme toggle adds `dark` to `<html>`, switches the toggle label to `Light`, and leaves `dark` in place after navigating from Dashboard to Error Log.
19. The strings `Atlas Research`, `Ledger Clerk`, `Inbox Triage`, `Field Notes`, and `Compliance Watch` each occur in the agents section, the contracts section, and the errors section.
20. No JavaScript framework object (`React`, `Vue`, `jQuery`) is referenced, and the page does not fetch JSON.

## 11. Out of scope

Form submission, live search, pagination, real chart data, authentication, persistence of deletes, and any HTTP API are out of scope. Escape closes the topmost overlay: the modal first, otherwise an open action menu, otherwise the mobile sidebar. Focus returns to the control that opened it.
