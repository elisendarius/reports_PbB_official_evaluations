# How to add a new evaluation run

You only need to do **two things**:

## 1. Create the folder and put your file in it

In the repository root, create a folder named `Run-YYYY-MM` (year then month).
Put the report inside it (a `.pdf`, `.html`, or anything else).

Examples:

```
Run-2026-06/report.html
Run-2026-06/results_June_2026r_NAVPbB.pdf
```

The folder name **must** match the pattern `Run-YYYY-MM` (e.g. `Run-2026-06`, not `run_2026_06` or `Run-2026-6`).

## 2. Add one line to `runs.json`

Open `runs.json` and add a new entry inside the `"runs"` array:

```json
{ "folder": "Run-2026-06", "file": "report.html" }
```

That's it. Save the file, refresh the page, and the new run will appear automatically — sorted by date, with the newest one tagged "Latest", and grouped under the right year (current year expanded, older years collapsed).

## A complete example

Say it's June 2026 and you just produced a new PDF report. You would:

1. Create `Run-2026-06/` and put `results_June_2026r_NAVPbB.pdf` inside it.
2. Edit `runs.json` so it looks like this:

```json
{
  "runs": [
    { "folder": "Run-2026-06", "file": "results_June_2026r_NAVPbB.pdf" },
    { "folder": "Run-2026-05", "file": "report.html" },
    { "folder": "Run-2026-04", "file": "results_April_2026r_NAVPbB.pdf" },
    { "folder": "Run-2026-03", "file": "report.html" },
    { "folder": "Run-2025-11", "file": "report.html" }
  ]
}
```

(The order in the file doesn't actually matter — the page sorts them automatically — but keeping newest-on-top makes it easy to scan.)

## To remove a run

Delete its line from `runs.json`. The folder can stay or be deleted; the page only shows what's listed in `runs.json`.

---

## Notes

- Runs are grouped by year automatically. The most recent year is shown expanded; older years collapse into a "Run – YYYY" section.
- The newest run gets a red "Latest" badge.
- Because the page reads `runs.json` via JavaScript, it needs to be served over HTTP/HTTPS. GitHub Pages, Netlify, any web server — all fine. If you want to test locally, run `python3 -m http.server` from the repo folder and open `http://localhost:8000`.
