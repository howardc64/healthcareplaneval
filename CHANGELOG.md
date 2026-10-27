# Changelog

All notable changes to this project are documented here. The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and the project uses [Semantic Versioning](https://semver.org/).

## [2.13.0] - 2026-10-27

### Added
- **Medicare Advantage plans.** New **Plan category** on each plan card. Medicare plans get the sections Medicare facts, Supplemental benefits, Out-of-network cost shares and Pharmacy channels, plus fields for plan id, service area, Part B premium, out-of-network deductible, combined out-of-pocket maximum, Part D deductible and prescription cap.
- **Schema 2.1** (backward compatible with 2.0): `plan_category`, `out_of_network_services`, `medicare`, `supplemental_benefits`, `drugs.pharmacy_channels`, `drugs.tier_labels`, `limits.drug_deductible`, `limits.drug_oop_max`, and six services (annual physical, diagnostic procedure, mammogram, colonoscopy, diabetic supplies, continuous glucose monitor). Plan type gains HMO-POS and PFFS.
- Two filled plan files: Aetna Medicare Enhanced (PPO) H5521-687 and Signature (PPO) H5521-431.
- Notices for Medicare plans (who is counted, what is not modeled).

### Changed
- The premium on a Medicare plan is counted per enrolled person (plus Part B if entered), and tooltips show the formula.
- A Medicare plan with a $0 medical deductible uses the per-person Part D deductible as its shared deductible.
- Version in the code is now 2.13.0 (it still said 2.6.0).

## [2.12.1] - 2026-10-27

### Changed
- The HSA tax-savings area is now a faint row of centered dots instead of dashes.
- The dashed outline to the maximum possible cost now starts at the end of the solid bar and runs across the HSA tax-savings area too, so it always ends at premium + out-of-pocket maximum.

## [2.12.0] - 2026-10-27

### Added
- **Dollar axis under the bar chart**, with a tick every $5,000 labeled $5k, $10k and so on. It lines up with the bars and stays visible when the chart scrolls.

### Changed
- The HSA tax-savings area is now just a faint dashed line through the middle of the segment instead of a cross-hatch.
- The dashed outline to the maximum possible cost is fainter still.

## [2.11.0] - 2026-10-27

### Added
- **Per hospital day tests in the stress scenario**: blood work, X-ray, ultrasound, MRI and CT per hospital day. They are counted for each selected person × days hospitalized, use the plan's lab, X-ray and imaging cost shares, add the row "Stress: tests and imaging during hospital stay" to the results, and show in the line-item detail tab. Older saves open with 0.
- **Maximum cost column** to the right of each bar's cost: premium + out-of-pocket maximum (with a tooltip).

### Changed
- The HSA cross-hatch and the dashed maximum outline are fainter so they draw less attention.
- Removed the "Solid bar = …" label from the bar chart legend.

## [2.10.0] - 2026-10-27

### Changed
- **HSA tax savings on the bar chart are now a cross-hatch fill** instead of a dashed outline. It still is not counted in the total.

### Added
- **Dashed outline to the maximum possible cost.** Every bar extends with a dashed outline to premium + out-of-pocket maximum, so you can see how close the year is to the worst case. For HSA plans it starts after the hatched area. Hover it for the maximum and the room left. The bar scale now fits the longest maximum.

## [2.9.1] - 2026-10-27

### Changed
- **Number box arrows step once per click.** The browser's built-in up/down arrows repeat quickly while the mouse button is held. They are replaced by ▲ ▼ buttons that change the value by one step per click (respecting each box's minimum and maximum). Typing works as before.

## [2.9.0] - 2026-10-27

### Added
- **Calculation tooltips in the line-item detail tab.** Hover (or tap) any number to see how it is figured: units (people × visits × per-visit counts), base cost, base total, the shared-deductible share, what you pay (copay or coinsurance plus the deductible portion), what insurance pays, the group subtotals, the out-of-pocket maximum reduction and the totals, premium and you-pay-plus-premium.

### Changed
- "Urgent care visits" no longer carries "(household)", so the urgent care inputs line up vertically with the others.

## [2.8.0] - 2026-10-27

### Added
- **Premium shading on the bar chart.** The premium part of each bar is a slightly darker shade; the rest of the bar is out of pocket.
- **Tooltips on bar segments.** Hover (or tap, or focus) the premium segment, the out-of-pocket segment or the dashed HSA tax-deduction outline to see how that part is figured. For HSA plans the out-of-pocket tooltip shows care costs minus the HSA tax deduction.

## [2.7.0] - 2026-10-27

### Changed
- **Ultrasound is now classified with MRI, PET and CT**, not with X-ray and diagnostic imaging. The four are a single plan entry, "Imaging (MRI, PET, CT, ultrasound)", and ultrasound is costed with that cost share in the results, line-item detail and import notes. The plan files' evaluator notes were updated to match.

### Added
- **HSA tax benefit on the bar chart.** HSA plan bars are followed by a dashed outline showing the tax savings. It gives a visual cue only: the bar length and the dollar amount still show the cost after tax savings, and the dashed part is not counted in the total.

## [2.6.0] - 2026-10-26

### Added
- **Single person evaluation.** A new **Coverage for** choice at the top of section 1 switches between *Married couple (family plan)* and *Single person (self-only plan)*. For a single person: spouse 2 and the second PCP count disappear, the stress scenario covers one person, the calculation uses each plan's individual deductible and out-of-pocket maximum (half the family amount, with a notice, when only that is entered), and the HSA maximum, HDHP minimum deductible and HDHP out-of-pocket cap use the self-only figures. Catch-up applies to the one person.
- HSA settings gain the 2027 self-only values (Rev. Proc. 2026-24): contribution limit $4,500, HDHP minimum deductible $1,750, HDHP maximum out-of-pocket $8,700.

### Changed
- Saves from earlier versions open as *Married couple*; results are unchanged. The printout header names the single person.

## [2.5.0] - 2026-10-26

### Added
- **Day and night theme.** The app follows the device's light or dark setting (`prefers-color-scheme`) and switches live when the setting changes. Colors are now CSS variables; printing always uses the light theme.

## [2.4.0] - 2026-10-26

### Changed
- **Result bar chart now sits in the blue header**, which stays on screen while you scroll, so you can change any input in sections 1 to 4 and see the effect at once.
- Bars glide from the previous to the new length, and the dollar amounts count up or down, whenever an input changes. Plans added or removed grow in or drop out. Animation is skipped if the system asks for reduced motion.
- The bar chart was removed from the Results card at the bottom (the table remains). It is not part of the printout.

## [2.3.1] - 2026-10-26

### Fixed
- A hidden plan could not be shown again because its Hide checkbox was hidden with the rest of the card. The checkbox now stays visible.

### Changed
- Price sources in the cost tooltips and the line-item detail tab now read "Costs section (2)", "plan details: Evaluator price" or "plan details: copay".

## [2.3.0] - 2026-10-26

### Added
- **Line-item detail tab**: choose a plan (and normal year or normal year + stress) to list every service and medication with units, base cost, insurance coverage, deductible used, you pay and insurance pays, plus subtotals and the out-of-pocket maximum reduction.
- **Specialist procedure** and **hospital cost per day** in section 2 (Costs).

## [2.2.0] - 2026-10-26

### Added
- **Section 2, Costs**: allowed price per unit for ER visit, labs (blood work), X-ray, ultrasound, MRI, CT and surgery, used for every plan. A price under a plan's *Evaluator prices* overrides it for that plan; with neither, the copay is used. Cost tooltips say which source supplied the price.
- **Hide checkbox** in the upper right of sections 1, 2 and 3 (hidden by default, saved with the file).
- **Hide checkbox** in the upper right of every health plan; a hidden plan collapses to its name and HSA checkbox.

### Changed
- Stress scenario is now section 3 and Health plans is section 4.
- Saves from 2.1.0 open normally; sections 1 to 3 start hidden and the new cost fields are blank.

## [2.1.0] - 2026-10-26

### Changed
- **Plan cards rebuilt around the schema.** Every field of `health-plan.schema.json` is now an input: identity, network rules, premium, deductible / out-of-pocket / coinsurance, all 33 services (each with structure, copay, coinsurance %, deductible applies, unit, max units, limits, source quote; primary care, chiropractic and outpatient mental health also have discounted first visits), drug tiers and drug extras, evaluator prices, excluded / other covered services, SBC coverage examples, extraction notes.
- **Hide checkbox on every plan section** (plus Hide all / Show all sections per plan). Sections that do not affect cost start hidden. The choice is saved with the file.
- **Cost calculation uses each service's cost share.** Copays and coinsurance that skip the deductible are paid from the first dollar and do not count toward the deductible; services where the deductible applies use it, then the copay or coinsurance; not-covered services are paid in full outside the max out-of-pocket; "max units charged" caps copays (for example 5 hospital days per stay). The deductible is shared across services in proportion to their allowed price. Allowed price = your estimate, else the copay. Previously one general coinsurance % and the deductible were applied to every price.
- **Cost tooltips** list each line (units × price, where the price came from, the cost share applied), and the "with deductible" tooltip shows first-dollar costs, the deductible part, the after-deductible part, the cap and anything not covered.
- **Load health plan** loads the whole file onto the card (not just prices) and lists services that still need a price.
- Saves from 2.0.0 are converted on open; results can differ slightly because primary care copays are now flat copays after the deductible instead of being cut to your coinsurance share.

### Added
- Notice in the results when a service you use has no price (it counts as $0).
- `evaluator_inputs.prices` accepts `primary_care_visit`, `specialist_visit` and `urgent_care_visit` (allowed price per visit) in `health-plan.schema.json`.

## [2.0.0] - 2026-10-26

### Changed
- **New common plan schema (2.0)**, built from the Ambetter Vital Gold and Select Bronze SBCs and marketplace pages. It records each service as a cost share (copay amount, member coinsurance %, whether the deductible applies, unit, limits, source quote) and covers identity, network rules, premium, deductible, out-of-pocket maximum, drugs, exclusions and the SBC coverage examples. Your own price estimates go in a separate optional `evaluator_inputs.prices` block.
- **Load health plan** reads schema 2.0. Prices come from `evaluator_inputs.prices` first, then from copays; coinsurance services are listed as "enter by hand". Schema 1.x plan files are rejected with a clear message.
- Plan files now live in `plans/` as `AB_Vital_Gold.plan.json` and `AB_Select_Bronze_HSA.plan.json`.

## [1.7.0] - 2026-10-26

### Changed
- **Simpler deductible rule:** everything you pay except the premium counts toward the deductible. You pay 100% of all listed prices up to the deductible, then your coinsurance share of the rest, capped at the max out-of-pocket. The cost breakdown tooltip is now five short lines. Results are unchanged for plans whose total spending is above the deductible, and for plans below it.
- The calculation code lost its copay/"subject to deductible" split.

### Removed
- Per-plan options "Copays count toward the deductible" and "Medication costs are flat copays (skip the deductible)", and `medications_flat_copays_skip_deductible` in plan files and the schema (old files that contain it still load; the value is ignored).

## [1.6.0] - 2026-10-26

### Added
- **X-ray** next to blood work everywhere: household needs, urgent care (per visit), ER stress scenario (per ER visit), plan price, results rows and cost breakdown tooltips.
- `health-plan.schema.json` (schema 1.1): new `blood_work`, `xray` and `urgent_care_visit` cost items. `examples/example-new-fields.json` shows them filled.

### Changed
- "Labs" renamed **Blood work** in the UI and code (`bloodWork`, `ucBlood`, `erBlood`, `bloodCost`). Saves from 1.5.0 and plan files using `lab_test` still load.

## [1.5.0] - 2026-10-26

### Added
- **Labs** in household needs (number of labs per year) and a **Lab test** price on each plan. New "Labs" row in section 2.
- **Urgent care** in household needs: visits per year, plus labs, ultrasounds, MRIs and CTs **per visit**. Each plan has an **Urgent care visit** price (a flat copay on non-HSA plans). New "Urgent care (visits, labs, imaging)" row in section 2.
- **Labs per ER visit** in the stress scenario, and a "Stress: labs during ER" row in section 4.
- Per-plan option **Copays count toward the deductible** (non-HSA plans, on by default).
- Health plan files can carry `lab_test` and `urgent_care_visit` costs (if absent, the app lists them as "enter by hand").

### Fixed
- On non-HSA plans, PCP, specialist, urgent care and flat medication copays were paid on top of a full deductible, so the "with deductible" total in sections 2 to 4 could equal the "no deductible limit" total even when spending passed the deductible. Copays now use up the deductible first. Untick the new option on a plan to get the old behavior.

## [1.4.0] - 2026-10-26

### Added
- "Hide rows" checkboxes above the results table for sections 1, 2, 3, 4, HSA details, and HSA plans: cost after tax. All are off by default; the choice is saved with your file.

### Changed
- Long plan names are truncated in the results header and cost bars. Hover (or tap) a name to see the full text.

## [1.3.0] - 2026-10-26

### Added
- `health-plan.schema.json`: JSON Schema describing one health plan so an LLM can fill it from a plan summary PDF (SBC), with per-field instructions, cost basis (copay, no charge, price estimate, not covered, not applicable, unknown) and source quotes.
- `fill-health-plan-prompt.md`: copy-paste prompt, SBC row to field mapping table, and optional inputs (premium, reference prices).
- `examples/example-health-plan.json`: filled sample.
- **Load health plan** button: loads one or more filled plan files and adds the plans to the list. Tolerates code fences and surrounding text, checks the schema version, and shows an import note on each plan (fields to enter by hand, estimates to verify, LLM notes) that can be dismissed.

## [1.2.0] - 2026-10-26

### Added
- Hover (or tap, or keyboard-focus) any dollar amount in the results and cost bars to see how it was calculated, step by step.

### Changed
- **Open file** now only loads the file. It never writes to the previous or the newly opened file.
- **Load example** and **Reset** turn off Auto-save to file and forget the remembered save file, so a real file cannot be overwritten. Choosing a file with Save as… or Open file turns auto-save back on.

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
