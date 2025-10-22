# Repository helper for CI & data conversion

This repository includes a helper HTML page (index.html) to inspect the provided attachments, detect problems, and produce corrected/converted files you can download locally. It also documents what is missing from the repository required by the task.

Important items the task asked for (summary)
- Fix the non-trivial typo in `execute.py` (the original attachment contains a spelling error).
- Convert `data.xlsx` (attachment) to `data.csv`.
- Add a GitHub Actions workflow at `.github/workflows/ci.yml` that:
  - Runs `ruff` and prints results in CI logs.
  - Runs `python execute.py > result.json`.
  - Publishes `result.json` using GitHub Pages.
- Do NOT commit `result.json`.

What is provided in attachments (authoritative)
- execute.py (attachment)
- data.xlsx (attachment)

What this repository currently contains (and how to act)
- index.html — an interactive page that:
  - Loads the provided attachments (by the exact filenames/URLs included with the task),
  - Detects problems (missing files and a typo),
  - Converts `data.xlsx` to `data.csv` (client-side) using a robust XLSX parser,
  - Produces a corrected `execute.py` (fixes the detected typo) for download,
  - Logs what files and columns were read and any mismatches to the console.
- README (this file)

How to use index.html locally
1. Serve the repository content over a local HTTP server (recommended) so the browser can fetch attachment files using relative URLs:
   - Python 3: `python -m http.server 8000` (from repo root) and open http://localhost:8000/index.html
   - Or use any static server of your choice.
2. Open `index.html` in your browser.
3. The page will attempt to fetch the exact attachment URLs included with the task:
   - `./35f0c98f-cfd1-4781-87d5-a863bacaafb3-execute.py` (this maps to the provided execute.py)
   - `./739e1fa5-f5e2-4958-a2fd-3ff946f6d23c-data.xlsx` (this maps to the provided data.xlsx)
4. If the page detects a typo (the string "revenew"), you will be offered a button to generate a corrected `execute.py` (downloadable).
5. You can convert the `data.xlsx` attachment to `data.csv` and download the CSV output.
6. The page will also check whether `data.csv` and `.github/workflows/ci.yml` already exist in the repository and will show clear messages if they are missing (they are expected to be added/committed by you).

Guidance for committing the required files
- After using the page (or editing locally), commit:
  - The fixed `execute.py` (replace the original file in the repo).
  - `data.csv` produced by the conversion (must equal the content of `data.xlsx`).
  - `.github/workflows/ci.yml` — a workflow that:
    - Runs `ruff` and prints its output.
    - Runs `python execute.py > result.json`.
    - Publishes `result.json` to GitHub Pages.
  - Do NOT commit `result.json`.

Notes about reproducibility and safety
- index.html only fetches files using the exact filenames/URLs provided with the task. It does not invent or assume other filenames.
- If something required is missing, the page will show a clear, visible error and log details to the console (see the "Console" tab in devtools).
- The XLSX -> CSV conversion uses a well-known public CDN for the SheetJS library; if that CDN fails to load the library the page will report a graceful error.

License
- This README is provided under the MIT License. See LICENSE in the repository root for the full text.