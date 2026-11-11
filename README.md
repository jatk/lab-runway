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

Your lab's data lives in the browser's local storage on the machine where you open the page. There is no server and no account, and nothing is uploaded anywhere.

That also means the data is tied to one browser profile on one machine, and clearing site data will erase it. To move a lab between machines or browsers — or just to keep a safety copy — use **Setup → Export backup**, then **Setup → Import backup** on the other side. Backups are plain JSON. They are excluded from git by default because they contain salary data (see `.gitignore`).

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
LICENSE      MIT license
.gitignore   keeps backups and system files out of the repo
```

## Notes for development

- The app is deliberately one self-contained file: no build step, no dependencies and no network calls.
- State is saved to `localStorage` under the `labRunway.*` keys — the lab itself, the version history index, and one entry per saved snapshot.
- Exports are built in the page and handed to the browser as a blob download.

## License

MIT — see [LICENSE](LICENSE).
