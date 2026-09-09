# Local Setup & GitHub Publishing Guide

This guide assumes Windows + PowerShell.

## Milestone A — Put your final files in place

The starter package already contains the correct folder structure.

### 1. Copy your Power BI file

Copy your final `.pbix` file into:

```text
pbs-pharma-market-intelligence\pbix\
```

Rename it:

```text
PBS_Market_Intelligence.pbix
```

### 2. Add screenshots

Take clean screenshots of the two final dashboard pages and save them as:

```text
screenshots\page1-market-overview.png
screenshots\page2-trend-analysis.png
```

Recommended screenshot checklist:

- no Power BI editing panes covering the report
- Page 1 shows the final year selection you want recruiters to see
- Page 2 shows a representative ATC class
- no selected visual handles/borders
- titles and data notes are readable
- crop out unnecessary desktop/window chrome if possible

### 3. Decide whether to include raw AIHW data

In File Explorer:

1. Find the original AIHW Excel file(s).
2. Right-click each file → **Properties**.
3. Check **Size**.

If the combined raw files are under roughly 5–10 MB, copy them into:

```text
data\raw\
```

If they are larger, leave `data/raw/` empty and rely on the AIHW links in the README.

Do not include transformed temporary exports or duplicate copies.

### 4. Final Power BI check before publishing

Open the PBIX and confirm:

- `DimATCClass` has 15 rows.
- `IsAggregate = TRUE` for exactly one row.
- `IsAggregate = FALSE` for 14 rows.
- `All PBS prescriptions` does not appear in the Page 1 class chart.
- `All PBS prescriptions` does not appear in the Page 2 slicer.
- `All PBS prescriptions` does not appear in the Page 2 movers table.
- Page 2 movers table has 14 ATC rows and no Power BI grand-total row.
- Page-level geography is `National`.
- Page 2 uses 2025 for the YoY movers table.
- The trend charts use `DimDate[MonthStart]` on a continuous X-axis.
- Expenditure and prescription trends are separate charts.
- Latest-three-month preliminary-data note is visible.
- The final `FactPBS` row count is checked.

If the final row count is 18,630, you may replace `18,000+ records` in README.md with `18,630 records`.

---

## Milestone B — Initialise Git locally

Open PowerShell.

Navigate to the parent folder containing the project folder. Example:

```powershell
cd "C:\Users\YOUR_NAME\Documents"
```

Enter the project:

```powershell
cd .\pbs-pharma-market-intelligence
```

Check the files:

```powershell
Get-ChildItem -Recurse
```

Initialise Git:

```powershell
git init
```

Check status:

```powershell
git status
```

You should see README.md, .gitignore and your project folders as untracked files.

Add everything:

```powershell
git add .
```

Check exactly what will be committed:

```powershell
git status
```

Create the first commit:

```powershell
git commit -m "Initial Power BI market intelligence project"
```

If Git asks you to configure your identity:

```powershell
git config --global user.name "YOUR GITHUB NAME"
git config --global user.email "YOUR GITHUB EMAIL"
```

Then repeat:

```powershell
git commit -m "Initial Power BI market intelligence project"
```

---

## Milestone C — Create the GitHub repository

On GitHub:

1. Sign in.
2. Click **New repository**.
3. Repository name:

```text
pbs-pharma-market-intelligence
```

4. Suggested description:

```text
Power BI market-intelligence analysis of Australian PBS expenditure and prescription trends across therapeutic drug classes, 2015–2026.
```

5. Set visibility to **Public**.
6. Do **not** initialise with:
   - README
   - .gitignore
   - license

Your local project already contains these.

7. Click **Create repository**.

GitHub will show the repository URL.

---

## Milestone D — Connect local repo to GitHub

Replace `YOUR-USERNAME` below with your GitHub username:

```powershell
git remote add origin https://github.com/YOUR-USERNAME/pbs-pharma-market-intelligence.git
```

Rename the branch to `main`:

```powershell
git branch -M main
```

Push:

```powershell
git push -u origin main
```

If GitHub authentication opens in the browser, complete the sign-in flow.

After the push, refresh the GitHub repository page.

You should see:

- README rendered on the front page
- `pbix/`
- `screenshots/`
- `data/`
- `.gitignore`

---

## Milestone E — Verify the public repository

Check all of these on GitHub:

### README

- images render correctly
- headings are readable
- no placeholder wording you intended to remove
- exact row count is only used if revalidated

### Screenshots

Click both PNGs and ensure they open.

### PBIX

Click `pbix/` and confirm the PBIX is present.

> GitHub cannot preview PBIX files in-browser. That is why screenshots and README documentation matter.

### Raw data

If raw source files are included:

- confirm only public AIHW files are present
- make sure there are no local/private files
- ensure README source links remain present for attribution

---

## Useful Git commands for future updates

See changed files:

```powershell
git status
```

Stage changes:

```powershell
git add .
```

Commit:

```powershell
git commit -m "Polish dashboard and documentation"
```

Push:

```powershell
git push
```

Typical complete update flow:

```powershell
git status
git add .
git commit -m "Update project"
git push
```

---

## Recommended final GitHub polish

After the repository is live:

1. Add repository topics such as:
   - `power-bi`
   - `dax`
   - `power-query`
   - `data-analysis`
   - `healthcare-analytics`
   - `pbs`
   - `business-intelligence`

2. Add the short repository description from Milestone C.

3. Pin the repository on your GitHub profile if this is one of your strongest portfolio projects.

4. Add the repository link to your resume or LinkedIn project section.

---

## Resume wording

Use these bullets unless your final validation changes the scope:

- Built an end-to-end Power BI analytics project using Australian government AIHW/PBS healthcare data, covering **18,000+ records** through data cleaning, star-schema modelling and DAX measure development.
- Identified and resolved multiple analytical integrity risks, including aggregate-row leakage, national/state aggregation issues, inconsistent category labels and measurement-precision artifacts.
- Derived evidence-based business insights from therapeutic-class expenditure and utilisation trends, including corroborating the 2016 antiinfectives expenditure spike against official AIHW evidence on hepatitis C DAA PBS listings.
- Documented a nine-point data-quality and limitations assessment covering source precision, preliminary observations, aggregation risks, partial-year data and analytical scope.

Once the final `FactPBS` row count is rechecked as 18,630, you can safely change the first bullet to `18,630 records`.
