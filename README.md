# GGWash ANC candidate tool

Live preview once this is pushed to GitHub Pages: `https://kaihallggwash.github.io/kai-anc-tool/`

## Files you will never need to edit

- `index.html`, `anc-tool.js`, `anc-tool.css` — the tool itself.
- `data/anc.geojson`, `data/smd.geojson` — the current DC GIS ANC/SMD boundary shapes. DC updates these in place at the source when boundaries change, so these should only need re-downloading if DC redraws the map again (not expected again this decade — current boundaries took effect Jan 1, 2023).

## Files you WILL replace, one per election cycle

- `data/roster.csv` — every declared candidate, whether or not they answered the questionnaire. Columns: `SMD, Candidate Name, Website`. This is what makes a candidate show up on the map at all, even with no questionnaire response.
- `data/responses.csv` — the **raw, unedited CSV export straight out of SurveyMonkey**. Don't clean it up or reformat it — the tool is built to read SurveyMonkey's export shape as-is (two header rows: the question text, then SurveyMonkey's own response-type label). Whatever questions you ask this year, however many there are, the tool will automatically build a chart for each one. The only two things it needs to find by name in that export:
  - A question with **SMD** somewhere in its text (e.g. "Select the SMD in which you are running:") — used to know which district a response belongs to.
  - SurveyMonkey's built-in **Name** field from the contact-info block — used to match a response to a candidate.

  If you ever add/remove/reword other questions, nothing needs to change — new questions just get new charts automatically.

## The endorsement file (updated *after* responses go up)

- `data/endorsements.csv` — starts out empty (headers only). Columns: `SMD, Candidate Name, Pull Quote, Writeup Link`. As GGWash announces endorsements ward by ward, add one row per endorsed candidate:
  - `SMD` and `Candidate Name` must match exactly what's in `responses.csv`/`roster.csv` for that person.
  - `Pull Quote` — type in whatever quote the endorsement committee picked to highlight, by hand. The tool doesn't try to guess this from their survey answers.
  - `Writeup Link` — link to the ward endorsement post, if there is one.

  A candidate with no row in this file just shows normally, no ribbon. Adding their row later and re-uploading the file is all it takes to add the green "GGWash endorsed" ribbon and quote to their card.

## How to update anything

All of the above are plain CSV files. On GitHub, open the file, click the pencil (edit) icon, make your change, and commit directly to `main`. No local software needed. The live tool re-reads these files fresh every time someone loads the page — there's no build step and nothing to redeploy.

## Embedding in an ExpressionEngine post

See `ee-embed-snippet.html` in this repo for the exact HTML to paste into the post's Inline Code Snippet field. It points at the absolute `kaihallggwash.github.io` URLs rather than relative paths, since it'll be running on ggwash.org, not on GitHub Pages.
