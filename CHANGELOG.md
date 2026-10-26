# Changelog

All notable changes to this project are documented here. The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and the project uses [Semantic Versioning](https://semver.org/).

## [1.1.0] - 2026-10-26

### Added
- **Save as…** button opens the system file window to choose the location and file name.
- **Save** rewrites the current file without prompting; **Open file** also sets the current file. Optional auto-save to file after each change. Browsers without file-handle support fall back to downloads.
- HSA plans show "complete cost − tax reduction" and "complete cost with stress − tax reduction" as explicit rows.
- Option to count tax savings on the full HSA contribution instead of only on care paid from the HSA.

## [1.0.0] - 2026-10-26

### Added
- Household input: both spouses' names and ages, combined federal tax rate (including NIIT), and annual needs (PCP visits per spouse, specialist visits, specialist procedures, US / MRI / CT imaging, medication fills for tiers 5 to 1).
- Plan editor: add, duplicate, and delete plans. Each plan holds name, HSA checkbox, monthly premium, deductible, coinsurance share after the deductible, max out-of-pocket, PCP copays (1st annual, 2nd, and later visits), specialist copay, specialist procedure cost, imaging costs, medication costs by tier, ER cost per visit, hospital cost per day, and surgery cost per procedure.
- Stress scenario: per-spouse or both, with ER visits, imaging per ER visit, hospital days, and surgeries.
- Results per plan: annual premium, itemized other costs, totals with and without the deductible limit, complete cost, and complete cost plus stress scenario.
- HSA analysis: maximum contribution (with catch-up per eligible spouse), contribution used, tax savings, real after-tax contribution, tax-adjusted net cost, and unspent balance.
- Editable HSA limits panel with 2027 IRS defaults (Rev. Proc. 2026-24), plus warnings for HDHP rule violations and Medicare-age spouses.
- Cost comparison bars and green highlighting of the lowest cost in each row.
- Print support (full page or results only) with a print-optimized layout.
- Save to and restore from a JSON file, plus automatic session recovery in the browser.
- Example data, reset, README, and this changelog for GitHub.
