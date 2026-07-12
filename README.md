# Liam Career Companion v3.1.5B

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
- `export_manifest.json`
- `liam_companion_backup.json`

The canonical dossier root is:

```text
/Users/shubham/Documents/Liam_Dossier
```

CSV exports are complete season-scoped snapshots. The team CSV includes all statuses; the player CSV includes only `START` and `SUB`. JSON backup remains a complete all-season application backup.

The export contract uses stable `Match_ID`, per-match `Season`, `H/A/N` home-away values, `CLUB/INTERNATIONAL` competition type values, pipe-delimited event minutes, and canonical performance fields such as `Dribbles_Attempted` and `Distance_Sprinted`.

`Shots_On_Target` is optional raw data and is not derived from shot accuracy.

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

## v3.1.5B notes

- No cloud sync.
- No screenshot attachments.
- No fixture schedule import.
- Minutes are derived from entry/exit values using a 90-minute default when no exit is entered.
- Home venue is derived from Settings; away venue is left blank because the app does not yet maintain an opponent stadium registry.
- Existing v3 localStorage is migrated in place. Matches missing per-match `Season` are assigned the saved settings season once and listed in `migrationNotes`.


## v2 changes

- Competition now has its own full-width row on the Fixture screen.
- Competitions can be added or removed in Records → Setup / season settings, with Club or International classification.
- A new empty draft defaults to 1 July of the selected season's starting year. Changing season resets the draft date only when the active draft is empty, so an in-progress match is not silently altered.
- Post-match entry now records Shots + Shot Accuracy on one row. Shots on target is derived for CSV compatibility by rounding `shots × accuracy / 100`.
- Dribbles + Dribble Success and Yellow + Red are paired in rows to follow the FC performance screen more naturally.


## Version 3 persistence and date rules

- Settings, custom tournaments, active drafts, completed matches, and record totals persist across app closures.
- Existing v1/v2 browser data is migrated automatically when available.
- After a match is saved, the next fixture defaults to two calendar days later.
- After the season changes, the fixture resets to 1 July of the season starting year.
- The app saves again when it is backgrounded or closed and requests persistent browser storage when supported.
- Continue using JSON backup periodically. Browser storage is durable but should not be treated as the only permanent backup.
