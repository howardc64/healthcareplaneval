# Health Plan Evaluator

A single-file, browser-based tool that compares health insurance plans for a married couple. Enter your expected annual health needs, enter each plan's premium and cost-sharing, and it shows the total yearly cost of every plan in a normal year and in a "stress" year (ER visit, hospital stay, surgery). HSA plans also show the maximum contribution and the real, after-tax cost of contributing.

Everything runs locally in your browser. No server, no build step, no dependencies, and nothing is uploaded.

## Quick start

1. Download or clone this repo.
2. Open `index.html` in a current browser (Chrome or Edge 112, Safari 16.5, Firefox 117 or newer; the page uses CSS nesting).
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
| `health-plan.schema.json` | Common JSON Schema (2.2) for one health plan: marketplace (SBC + plan-details page) or Medicare Advantage (plan-details page, Summary of Benefits) |
| `fill-health-plan-prompt.md` | Prompt for the LLM to fill a plan file (schema 2.2, marketplace and Medicare) |
| `plans/AB_Vital_Gold.plan.json`, `plans/AB_Select_Bronze_HSA.plan.json` | Filled plan files (Ambetter Cascade Select Vital Gold and Select Bronze HSA, 2027) |
| `plans/Aetna_Medicare_Enhanced_PPO.plan.json`, `plans/Aetna_Medicare_Signature_PPO.plan.json` | Filled Medicare Advantage plan files (Aetna Enhanced H5521-687 and Signature H5521-431, King County WA, 2027) |

## How to use

Sections 1, 2, 3 and 4 each have a **Hide** checkbox in the upper right (hidden by default; the choice is saved with your file).

HSA features (HSA limits in Settings, the tax rate, HSA rows and legend entry, net-after-tax rows) are shown only while at least one plan is marked **HSA-eligible plan**.

**1. Household annual health needs**
Start with **Coverage for**: *Married couple (family plan)* or *Single person (self-only plan)*. A single person has one name, age and PCP visit count, one person in the stress scenario, the plan's **individual** deductible and out-of-pocket maximum (half the family amount, with a notice, if only the family amount is entered), and the self-only HSA limit, HDHP minimum deductible and HDHP out-of-pocket cap. A couple uses the family amounts. Switching back and forth keeps everything you entered.

Names and ages of both spouses, your combined federal tax rate (include NIIT, e.g. 24 + 3.8 = 27.8), and your expected annual use: PCP visits per spouse, specialist visits, specialist procedures, blood work, X-rays, ultrasounds, MRIs, CTs, urgent care (visits per year, with blood work, X-rays, ultrasounds, MRIs and CTs per visit), medication fills by tier (tier 5 to tier 1), and your yearly **dental** needs: cleanings, root canals and crowns (household totals).

**2. Costs**
Your estimate of the allowed price per unit for ER visit, specialist procedure, labs (blood work), X-ray, ultrasound, MRI, CT, hospital cost per day, surgery (facility + surgeon, per procedure) the dental cleaning, root canal and crown,  Each of these fills in for any plan whose own field is empty. The medication tier 3 price and the Part B premium are in **Defaults** (in Health plans). The deductible and coinsurance are applied to these prices for every plan. A price in a plan's *Evaluator prices* overrides it for that plan (and a plan with no value in a field uses the Costs value); with neither, the app uses the copay.

**3. Stress scenario**
Tick one spouse or both, then enter ER visits, blood work, X-ray and imaging per ER visit (blood work, X-ray, US, MRI, CT), days hospitalized (with blood work, X-ray, US, MRI and CT per hospital day), and surgeries.

**4. Health plans**
At the top is a **Defaults** block, used for any plan that has no value of its own: *cleanings covered per person per year* (2; applies when a plan's dental cleaning has no max), the *medication tier 3 price per fill* ($250; the plan's Evaluator price wins) and the *Part B premium* ($203 a month in 2026, growing 5.25% a year; each Medicare Advantage plan uses its own plan year, the plan's own Part B premium wins, and an optional override replaces the calculation). Tick **Hide** in the section's upper right corner to fold the whole section away; hidden plans still count and are saved. The Defaults block has its own **Hide** checkbox. The Part B (Medicare premium) group appears only while a Medicare Advantage plan is in the list.

Add as many plans as you like (add, duplicate, delete). Tick **Hide** in the upper right corner of a plan to collapse it to its name. Each plan card holds every field of `health-plan.schema.json`, grouped into sections:

- Identity and source documents, network rules, premium, deductible / out-of-pocket maximum / coinsurance
- Five groups of services (office and urgent care; tests and imaging; surgery, emergency and hospital; mental health and maternity; rehab, home care, equipment and children's). Every service has its own **cost share**: how you pay (copay, coinsurance, no charge, not covered, not applicable, unknown), copay amount, your coinsurance %, whether the deductible applies first, unit, max units charged, limits and a source quote. Primary care, chiropractic and outpatient mental health also have "discounted first visits" (count + cost share).
- Prescription drugs (tiers 1 to 5, insulin cap, days supply, mail-order multiplier)
- **Evaluator prices**: your allowed price per unit for each service the calculation uses
- Excluded and other covered services, SBC coverage examples, extraction notes, and (HSA plans) the planned HSA contribution

Every section has a **Hide** checkbox so a plan is never overwhelming; **Hide all sections** / **Show all sections** sit next to Duplicate and Delete. Sections that do not change the cost (identity, network, mental health and maternity, rehab and other services, the text lists, coverage examples, extraction notes) start hidden. Hidden sections keep their values and still count; the choice is saved with your file.

Services tagged **used in cost** feed the results (primary care, specialist, urgent care, lab / blood work, X-ray and ultrasound, CT / MRI, outpatient surgery, ER, hospital, drug tiers 1 to 5, dental cleaning, root canal and crown). The others are recorded for reference only.

**Dental** has its own section on each plan card (**Services: dental**): a cost share for cleaning, root canal and crown, a dental deductible, a dental annual maximum (what the plan pays; you pay everything above it) and whether cleanings count toward that maximum. The deductible and the maximum are per person; a couple gets two of each.

**Line-item detail tab**
Click the **Line-item detail** tab (next to **Evaluator**) and pick a plan (and, if you like, the normal year or the normal year plus the stress scenario). Every service, medication and dental procedure in your annual needs is listed with its units, base (allowed) cost, how the plan covers it, how much of the deductible it uses, what you pay and what the insurer pays. Subtotals, the out-of-pocket maximum reduction and the totals match the results table. Rows are one per kind of service (not one per visit), because the deductible is shared across services in proportion to their allowed price.

Both this table and the Annual cost table scroll inside their own frame. The frame is sized to fit below the blue top pane, so you can scroll to the last row with the column headers still in view. In a very short window the frame keeps a minimum height of 220 px.

**Results** (one column per plan)

1. Annual premium
2. All other costs: itemized, then the total with no deductible limit (listed prices paid in full) and the total with deductible, coinsurance and max out-of-pocket applied
3. Complete cost (1 + 2), both ways
4. Complete cost + stress scenario, both ways
5. HSA plans: maximum HSA contribution, contribution used, tax savings, and real contribution after the tax deduction
6. For HSA plans, an explicit block: complete cost − tax reduction, and complete cost with stress − tax reduction
7. Net cost after HSA tax savings

Plan names use the short form shown on the bars; hover or tap a name to see it in full. The **Show/hide rows** dropdown above the table collapses Household, Costs, Stress scenario, Health plans, HSA details and HSA plans (all shown by default). The lowest cost in each comparison row is highlighted green. Hover over (or tap) any dollar amount to see exactly how it was calculated.

**Load a plan from plan documents**

1. Give an LLM that reads PDFs `health-plan.schema.json`, the plan's Summary of Benefits and Coverage (SBC) and, if you have it, the marketplace plan-details page (it has the premium).
2. Save its JSON answer as a `.json` file (a reply wrapped in a code fence still loads). Two filled examples are in `plans/`.
3. Click **Load health plan** (next to **Add plan**) and pick one or more files. Loaded plans are added to your list; nothing is replaced and no save file is written to by the load itself.
4. Each loaded plan shows a yellow import note listing fields to enter by hand, estimated values to verify, and notes.

The plan file records **facts from the documents**: for every service a cost share (copay amount, coinsurance percentage, whether the deductible applies, limits) with a source quote. The optional `evaluator_inputs.prices` block holds **your own dollar estimates** and is kept separate from the facts. The app picks each price like this:

- A number in `evaluator_inputs.prices` wins over the Costs value (use it for services the documents price only as coinsurance, for copays charged after the deductible, and for anything not listed, such as specialist procedures).
- Otherwise a copay is used as the allowed price, and "no charge" is $0.
- Coinsurance has no dollar price in an SBC, so the price is left empty and listed in the import note.

Everything in the schema is loaded onto the card. Ultrasound, MRI, PET and CT all use the single "imaging (MRI, PET, CT, ultrasound)" cost share (ultrasound is not part of "x-ray and diagnostic imaging"), surgery is the facility fee plus the surgeon fee, and the hospital price is per day. Premiums are not in an SBC; take them from the marketplace page. Plan files from schema 1.x are not read; the app says so when you load one.

**Save, restore and print**

- **Save as…** opens your system's file window so you choose the folder and file name. **Save** then rewrites that same file, and **Auto-save to file** (on by default) rewrites it after every change. **Open file** only loads a saved file (it writes nothing) and makes it the current file. **Load example** and **Reset** turn auto-save off and forget the current file so a real file is never overwritten. Rewriting a chosen file needs Chrome or Edge; Firefox and Safari fall back to downloading a copy each time.
- Your last session is also kept automatically in your browser's local storage.
- **Print** prints the whole page; **Print results only** prints just the comparison.

## Medicare Advantage plans

Set **Plan category** to *Medicare Advantage* at the top of a plan card (loading a plan file with `plan_category: medicare_advantage` does it for you). The card then shows extra sections and fields:

- **Medicare facts**: star rating, Part D, enrollment contacts, eligibility, Extra Help, traveler program.
- **Supplemental benefits**: dental, eye exam, eyewear, hearing exam, hearing aids, fitness, transportation, meals, worldwide emergency (allowances and details, not costed).
- **Out-of-network cost shares** for 15 services (reference only; the results use in-network costs).
- **Pharmacy channels**: preferred retail, standard retail and mail order (read-only summary of the file). The tier fields hold the plan's best everyday channel, and tier numbers are positional (Medicare Tier 2 is generic).
- Extra fields: Medicare plan id, service area, Part B premium, out-of-network deductible, combined in/out-of-network out-of-pocket maximum, Part D deductible and prescription out-of-pocket cap.

How the numbers change for a Medicare plan:

- **Premium** = (plan premium + optional Part B premium) × 12 × the number of enrolled people. Enrolled people are those at or above the Medicare age in Household; if nobody is, every person is counted and a notice says so.
- **Deductible and maximum out-of-pocket** are per person; a couple uses 2 × the individual amounts (Medicare plans have no family amounts).
- **Separate deductibles**: a Medicare plan has a medical deductible (often $0) and a separate per-person Part D drug deductible. The medical deductible applies only to medical services; the drug deductible applies only to drug tiers marked "deductible applies". Marketplace plans keep one deductible shared by medical and drugs.
- **Prescription out-of-pocket cap**: if a Medicare plan has a prescription out-of-pocket cap (per person, field on the plan card), what you pay for medications is limited to it (a couple uses 2 × the amount). The cap is applied to the medication cost share first; the combined out-of-pocket maximum then applies to what is left. Line-item detail shows the reduction as its own row. If no cap is entered, medication costs are not capped and a notice says so.
- **Not modeled**: out-of-network use, free first 20 skilled-nursing days, and Medigap or employer coverage interaction. A notice lists these.

## How the numbers are calculated

Deductible and out-of-pocket amounts are **family** (household) amounts; if only the individual amount is given, 2 × that is used.

- **Annual premium** = monthly premium × 12.
- **Allowed price per unit** = your number in the plan's *Evaluator prices* if there is one, otherwise your cost in Costs, otherwise the copay amount. A service that is only coinsurance and has no price counts as $0, and the results show a notice naming it.
- **Each service line** (units × allowed price) goes into one bucket according to its cost share:
  - *No charge / not applicable*: you pay $0.
  - *Deductible does not apply*: you pay the copay (per charged unit) or your coinsurance % of the allowed price from the first dollar. It counts toward the max out-of-pocket but not toward the deductible.
  - *Deductible applies*: the allowed price counts toward the deductible. You pay 100% of it until the deductible is met, then the copay or coinsurance. When several services share the deductible it is spread across them in proportion to their allowed price.
  - *Not covered*: you pay the full price, outside the max out-of-pocket.
  - *Not entered / unknown*: treated as your general coinsurance % after the deductible (this is also how specialist procedures are costed).
- **Max units charged** limits how many copays are charged (for example 5 hospital days per stay, per person). On a **dental** service the same field is **Max covered per person per year** (for example 2 cleanings): units above it are not covered and you pay their full price, outside the dental annual maximum.
- **Primary care** = the discounted first visits per person per year, then the regular cost share.
- **Surgery** = facility fee + surgeon fee. A surgery price in *Evaluator prices* is split evenly between the two.
- **Dental** is costed outside the medical deductible and the medical out-of-pocket maximum. Each procedure (cleanings, then root canals, then crowns) takes its cost share (copay, coinsurance, no charge or not covered) after the dental deductible, if the share says the deductible applies. The plan pays at most the dental annual maximum (cleanings count toward it only if the plan says so); you pay everything above it. A dental service with no cost share entered counts as not covered. Dental is in the results as three listed-price rows and as an "of which dental" row under the with-deductible total, and as its own group in Line-item detail.
- **Urgent care** = visits × visit cost + visits × (blood work, X-rays and imaging per visit × their costs).
- **No deductible limit total** = every listed price paid in full, with no deductible, copay, coinsurance or cap.
- **With deductible total** = first-dollar copays and coinsurance + the deductible part + the after-deductible copays/coinsurance, capped at the max out-of-pocket (a blank or 0 max means no cap), plus anything not covered.
- **Stress scenario**: hidden by default; turn it on with the **Stress scenario** button in the toolbar. Counts apply to each selected spouse. Blood work, X-ray and imaging counts are per ER visit. The stress charges are added to the normal-year charges **before** the deductible and cap are applied, so the deductible is never counted twice. "Extra cost the stress adds" is the difference.
- **HSA maximum** = family limit + the catch-up amount for each spouse at or above the catch-up age and below the Medicare age.
- **Real contribution after tax** = contribution × (1 − tax rate). **Tax savings** = contribution × tax rate.
- **Tax reduction from HSA** = tax rate × the full HSA contribution. The deduction depends on the contribution, not on how much care is paid from the HSA. The contribution is treated as a long-term investment, not a cost, so no unspent balance is tracked.
- **Net cost after HSA tax savings** = complete cost − tax reduction.

Hover over (or tap) any dollar amount to see the calculation. For services the tooltip lists each line: units × price, where the price came from, and the cost share applied; the "with deductible" total shows the first-dollar amount, the deductible part, the after-deductible part, the cap and anything not covered.

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

A JSON object: `{ "app": "health-plan-evaluator", "version": "...", "savedAt": "...", "state": { "household": {...}, "plans": [...], "stress": {...}, "settings": {...} } }`. `costs` holds the Costs prices and `view.secHide` the hide state of sections 1 to 3. Each plan mirrors the schema (`identity`, `network`, `premium`, `limits`, `services`, `drugs`, `prices`, ...) plus `hide`, `collapsed` and `hsaContrib`. Missing fields are filled with defaults when a file is opened. Saves from 2.0.0 and earlier (one flat price per service) are converted on open; their primary care copays become flat copays.

## Limitations

- Models family coverage for one married couple. Two separate self-only plans are not modeled.
- Federal tax only; no state tax, FICA savings through payroll HSA contributions, or employer HSA contributions.
- Uses the prices you enter. It does not model separate in-network/out-of-network rates, embedded per-person deductibles, separate service deductibles, or mail-order pricing.
- Services without a household usage input (mental health, maternity, rehab, home health and so on) are recorded on the card but not costed.
- Medication tiers use one price per fill; combination or specialty-pharmacy rules are not modeled.
- Estimates only. This is not tax, financial, or insurance advice; confirm figures with your plan documents and a tax professional.
