# Liam Career Companion v1

A mobile-first offline-capable PWA for logging Liam Murdock's FC26 matches with minimal friction.

## Included workflow

1. **Fixture** — date, competition, stage, opponent, home/away/neutral, venue, table positions, context.
2. **Events** — goal and assist minutes during the match.
3. **Post-match** — score, status, substitution minutes, rating, shots, dribbles, offsides, possession lost, sprint distance, cards, notes and story tags.
4. **Records** — local season totals, saved matches, editing, deletion and exports.

## Storage

Data is stored locally in the browser using `localStorage`. Export a JSON backup periodically. Clearing browser/site data will remove local records unless backed up.

## Dossier exports

The app exports:

- `current_season_team_matches.csv`
- `current_season_matches.csv`
- `liam_companion_backup.json`

The two CSVs preserve the Liam dossier's existing starter columns and append these new columns at the end:

- `Assist_Minutes`
- `Dribbles`
- `Dribble_Success_Pct`
- `Offsides`
- `Possession_Lost`
- `Distance_Sprinted_Km`

The current dossier build will safely ignore unknown appended columns until its views are extended to use them.

## Run locally on a Mac

From this folder:

```bash
python3 -m http.server 8080
```

Then open:

```text
http://localhost:8080
```

## Install on iPhone

The PWA needs to be served over HTTPS for reliable iPhone installation and offline caching. The easiest eventual deployment is GitHub Pages, Netlify, or Cloudflare Pages.

After hosting:

1. Open the site in Safari.
2. Tap Share.
3. Tap **Add to Home Screen**.

## v1 limitations

- No cloud sync.
- No screenshot attachments.
- No fixture schedule import.
- Minutes are derived from entry/exit values using a 90-minute default when no exit is entered.
- Home venue is derived from Settings; away venue is left blank because the app does not yet maintain an opponent stadium registry.


## v2 changes

- Competition now has its own full-width row on the Fixture screen.
- Competitions can be added or removed in Records → Setup / season settings, with Club or International classification.
- A new empty draft defaults to 1 July of the selected season's starting year. Changing season resets the draft date only when the active draft is empty, so an in-progress match is not silently altered.
- Post-match entry now records Shots + Shot Accuracy on one row. Shots on target is derived for CSV compatibility by rounding `shots × accuracy / 100`.
- Dribbles + Dribble Success and Yellow + Red are paired in rows to follow the FC performance screen more naturally.
