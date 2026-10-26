# Health Plan Evaluator

A single-file, browser-based tool that compares health insurance plans for a married couple. Enter your expected annual health needs, enter each plan's premium and cost-sharing, and it shows the total yearly cost of every plan in a normal year and in a "stress" year (ER visit, hospital stay, surgery). HSA plans also show the maximum contribution and the real, after-tax cost of contributing.

Everything runs locally in your browser. No server, no build step, no dependencies, and nothing is uploaded.

## Quick start

1. Download or clone this repo.
2. Open `index.html` in any modern browser.
3. Click **Load example** to see it working, then replace the numbers with your own.

### Host on GitHub Pages

1. Push the repo to GitHub.
2. Go to **Settings → Pages**, choose the `main` branch and the `/ (root)` folder.
3. Your app will be live at `https://<your-user>.github.io/<repo>/`.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app (HTML, CSS, JavaScript) |
| `README.md` | This file |
| `CHANGELOG.md` | Version history |

## How to use

**1. Household annual health needs**
Names and ages of both spouses, your combined federal tax rate (include NIIT, e.g. 24 + 3.8 = 27.8), and your expected annual use: PCP visits per spouse, specialist visits, specialist procedures, ultrasounds, MRIs, CTs, and medication fills by tier (tier 5 to tier 1).

**2. Health plans**
Add as many plans as you like (add, duplicate, delete). Each plan has: name, HSA checkbox, monthly premium, deductible, your coinsurance share after the deductible, max out-of-pocket, PCP copays (1st annual visit, 2nd visit, each visit after 2), specialist copay, specialist procedure cost, imaging (US, MRI, CT), medication costs by tier, ER cost per visit, hospital cost per day, and surgery cost per procedure.

**3. Stress scenario**
Tick one spouse or both, then enter ER visits, imaging per ER visit (US, MRI, CT), days hospitalized, and surgeries.

**Results** (one column per plan)

1. Annual premium
2. All other costs: itemized, then the total with no deductible limit (listed prices paid in full) and the total with deductible, coinsurance and max out-of-pocket applied
3. Complete cost (1 + 2), both ways
4. Complete cost + stress scenario, both ways
5. HSA plans: maximum HSA contribution, contribution used, tax savings, real contribution after the tax deduction, and unspent balance
6. For HSA plans, an explicit block: complete cost − tax reduction, and complete cost with stress − tax reduction
7. Net cost after HSA tax savings

The lowest cost in each comparison row is highlighted green.

**Save, restore and print**

- **Save as…** opens your system's file window so you choose the folder and file name. **Save** then rewrites that same file, and **Auto-save to file** (on by default) rewrites it after every change. **Open file** restores a saved file and makes it the current file. Rewriting a chosen file needs Chrome or Edge; Firefox and Safari fall back to downloading a copy each time.
- Your last session is also kept automatically in your browser's local storage.
- **Print** prints the whole page; **Print results only** prints just the comparison.

## How the numbers are calculated

All deductible and out-of-pocket amounts are **family** (household) amounts.

- **Annual premium** = monthly premium × 12.
- **PCP cost (per spouse)** = 1st-visit copay (if ≥ 1 visit) + 2nd-visit copay (if ≥ 2) + (visits − 2) × later-visit copay.
- **Other items** = count × per-item cost (specialist visits, procedures, imaging, medication fills).
- **No deductible limit total** = every listed price paid in full, with no deductible, coinsurance, or cap.
- **With deductible total**:
  - Non-HSA plans: PCP and specialist copays are flat amounts outside the deductible. Medications are also flat if the plan's "flat copays" box is ticked. Everything else is subject to the deductible.
  - HSA plans: everything is subject to the deductible (typical for HDHPs).
  - Subject amounts: you pay 100% up to the deductible, then your coinsurance share of the rest.
  - The total is capped at the max out-of-pocket (a blank or 0 max means no cap).
- **Stress scenario**: counts apply to each selected spouse. Imaging counts are per ER visit. The stress charges are added to the normal-year charges **before** the deductible and cap are applied, so the deductible is never counted twice. "Extra cost the stress adds" is the difference.
- **HSA maximum** = family limit + the catch-up amount for each spouse at or above the catch-up age and below the Medicare age.
- **Real contribution after tax** = contribution × (1 − tax rate). **Tax savings** = contribution × tax rate.
- **Tax reduction from HSA** = tax rate × the amount of care paid from the HSA (the smaller of your contribution and your out-of-pocket spending). Tick "Count tax savings on the full HSA contribution" in the HSA panel to use the whole contribution instead.
- **Net cost after HSA tax savings** = complete cost − tax reduction. Unspent contributions stay in your account and are shown as the unspent balance rather than counted as a cost.

### HSA limits (defaults: calendar year 2027)

Defaults come from IRS Revenue Procedure 2026-24 for family HDHP coverage and are editable in the "HSA limits and rules" panel:

| Item | Default |
| --- | --- |
| HSA contribution limit (family) | $9,000 |
| Catch-up (age 55+, per spouse) | $1,000 |
| HDHP minimum deductible (family) | $3,500 |
| HDHP maximum out-of-pocket (family) | $17,400 |

The app warns if an HSA plan falls outside the HDHP deductible or out-of-pocket rules, or if a spouse is at or above the Medicare age.

## Save file format

A JSON object: `{ "app": "health-plan-evaluator", "version": "...", "savedAt": "...", "state": { "household": {...}, "plans": [...], "stress": {...}, "settings": {...} } }`. Missing fields are filled with defaults when a file is opened, so older saves keep working.

## Limitations

- Models family coverage for one married couple. Two separate self-only plans are not modeled.
- Federal tax only; no state tax, FICA savings through payroll HSA contributions, or employer HSA contributions.
- Uses the prices you enter. It does not model separate in-network/out-of-network rates, per-person deductibles, or copays that count toward the deductible on non-HSA plans.
- Medication tiers use one price per fill; combination or specialty-pharmacy rules are not modeled.
- Estimates only. This is not tax, financial, or insurance advice; confirm figures with your plan documents and a tax professional.
