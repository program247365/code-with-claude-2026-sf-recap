# Code with Claude · SF 2026 — Interactive Timeline

An unofficial fan recap of [**Code with Claude San Francisco**](https://claude.com/code-with-claude/san-francisco?ref=kbr.sh) (May 6, 2026) and [**Code with Claude Extended**](https://claude.com/code-with-claude/san-francisco-extended?ref=kbr.sh) (May 7, 2026) — the full schedule as a single interactive timeline, with embedded session videos, themes, and venue photos pulled from live notes.

**→ [program247365.github.io/code-with-claude-2026-sf-recap](https://program247365.github.io/code-with-claude-2026-sf-recap/)**

![Code with Claude SF 2026 — Interactive Timeline](./og-image.png)

## What's in the site

- **39 sessions** across two days, organized as a single scrollable timeline with day breaks and per-talk metadata
- **Embedded YouTube videos** for all 19 Day 1 sessions (the official San Francisco recordings). The Extended day wasn't recorded; six Day 2 workshops link the London edition of the same session, labeled with its presenter
- **Themes view** — high-level patterns from the conference, each linked to the source talk that surfaced it
- **Around the room** — art-directed venue gallery from personal photos, HEIC → JPEG with EXIF scrubbed
- **Light + dark mode** with a deliberately gentle light masthead
- **Claude FM** — an optional ambient stream that plays as the masthead background; pill-toggleable
- **Open Graph + Twitter cards** for clean previews when shared

## How it's built

One HTML file. Inline CSS, inline JS, no build step. ~2,300 lines, all in [`index.html`](./index.html). Session data lives in a single `const SESSIONS = [...]` array near the bottom.

The trade-offs of this choice:

- **No framework, no transpile, no `node_modules`** — the file you edit is the file the browser runs. Diffs are honest. Behavior is one Cmd+F away.
- **No CMS** — adding a session is adding one object literal in source control. No content service, no API, no migration.
- **Trivially hostable** — any static file server works. GitHub Pages is just where it happens to live.

The cost is real: components can't be reused across pages, and one file does a lot. For a single-page recap that gets edited a few times a week, that's a great deal.

## Run it locally

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

## How the timeline was kept current

While recordings were still being published, a script crawled the official [San Francisco playlist](https://www.youtube.com/playlist?list=PLmWCw1CzcFim2obQ-w3ohbULOfwp5lApR) and both conference pages, matched video titles to session titles, and checked that every theme still pointed at a real session. It never wrote prose, added sessions, or rewrote themes — those were judgment calls.

The conference is over and every published recording is linked, so the scheduled run was retired in November 2026. The site is now static.

## Adding or editing a session

Find `const SESSIONS` in [`index.html`](./index.html) and edit or add an entry:

```js
{
  day: 2,                          // 1 or 2
  time: "10:00",                   // ordering is by array position
  title: "…",
  speaker: "…",
  type: "talk",                    // keynote | announce | talk | workshop | officehours
  summary: "…",                    // short blurb on the timeline card
  tags: ["evals", "agents"],
  youtubeId: "dQw4w9WgXcQ",        // or null → shows "No recording published"
  takeaways: ["…", "…"],           // optional bullets in the modal
  sessionUrl: "https://…"          // optional link in the modal footer
}
```

The session count, the play-bubble overlay, the modal, and the themes view all derive from this array.

## Credits

Made by [Kevin B. Ridgway](https://kbr.sh) and [Claude](https://claude.ai?ref=kbr.sh).

Talk descriptions are paraphrased from the official session pages on [claude.com/code-with-claude](https://claude.com/code-with-claude/san-francisco?ref=kbr.sh). Videos embed from the official [@claude](https://www.youtube.com/@claude) uploads. Venue photos taken on-site. Not affiliated with Anthropic.
