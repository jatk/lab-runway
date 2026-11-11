# Lab Runway

A single-page app for projecting lab budgets across grants, fellowships, startup and departmental support.

It answers "how long is the lab funded?" by projecting every cost month by month against the support that pays for it, with history going back as far as your records do.

## Running it

Open `index.html` in a browser. There's no build step and nothing to install.

If your browser blocks features when opening a local file, serve the folder instead:

```sh
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Where data is stored

| Where you run it | Where your lab's data lives |
|---|---|
| The published Claude artifact | Your Claude account (synced) |
| This local copy | The browser's local storage, on this machine only |

The two don't sync. To move data between them, use **Setup → Export backup** in one and **Setup → Import backup** in the other. Backups are plain JSON, so they're safe to keep alongside the code. They're excluded from git by default because they contain salary data (see `.gitignore`).

## Main features

- **Overview**: "funded through" date, balance chart with past and projected months, total support available, alerts.
- **Funding map**: month-by-month grid of who pays for each cost, with grouping and collapsible groups.
- **Support**: grants, startup, departmental and fellowship support, each with a detail view of how its money is spent. Also includes funding composition charts and spending by fiscal year.
- **Costs**: personnel and other costs with roles, raises, fringe, and current/past/upcoming status. Funding is set by clicking months on a per-person timeline.
- **History**: automatic and named versions, with the ability to view or restore any of them.
- **Indirect costs**: MTDC or TDC, either on top of or within the award.
- **Fellowships**: tied to a person, paying a total award, a percentage of salary, or a fixed monthly amount, with or without fringe.

## Project layout

```
index.html   the whole app: HTML, CSS and JavaScript in one file
README.md    this file
.gitignore   keeps backups and system files out of the repo
```

## Notes for development

- The app is deliberately one self-contained file so it can be published as a Claude artifact unchanged.
- Code that talks to `window.claude` (account storage, downloads) only runs inside the published artifact. When it's missing, the app falls back to `localStorage`, and exports appear as copyable text.
