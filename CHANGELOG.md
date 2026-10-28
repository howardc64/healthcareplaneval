# Changelog

All notable changes to this project are documented here. The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and the project uses [Semantic Versioning](https://semver.org/).

## [2.28.1] - 2026-10-28

### Changed
- **HSA tax reduction is now always tax rate × the full contribution**, because the deduction does not depend on how much care is paid from the HSA. The contribution is treated as a long-term investment, not a cost.

### Removed
- The "Count tax savings on the full HSA contribution" checkbox and the two "Unspent HSA balance" result rows. Saved files that contain the old setting still open; it is ignored.

## [2.28.0] - 2026-10-28

### Changed
- **HSA limits and rules** is now a regular section with a **Hide** checkbox (like Household, Costs, Stress scenario and Health plans) instead of a triangle that opens and closes. It starts hidden, and the whole section only appears when a plan is marked HSA-eligible. The input boxes are bottom-aligned so they line up when a label wraps to two lines.
- **Section headings are no longer numbered**, and text that said "section 2" or "section 4" now names the section (Costs, Defaults).
- **Opening a file no longer shows the "Opened ... (nothing was written)" message.** The Current file name in the header still shows the file.

### Removed
- **Plan year and Medicare age settings.** Medicare age is fixed at 65 (the statutory age). A plan's own plan year is used for the Part B premium; a plan with no year uses another plan's year in the list. Saved files that contain the old values still open; the values are ignored.

## [2.27.1] - 2026-10-28

### Changed
- The Medical max amounts (and their column label) are right-aligned so the digits line up.

## [2.27.0] - 2026-10-28

### Changed
- **HSA features appear only when a plan is marked HSA-eligible.** With no HSA plan the app hides: the HSA limits and HDHP fields and the "count tax savings on the full contribution" option in Settings (the section is renamed "Settings: plan year and Medicare age", and Plan year and Medicare age stay because Medicare plans use them), the federal tax rate hint, the "HSA details" and "HSA plans: cost after tax" entries of the Show/hide rows menu, the "HSA savings" legend entry, and the duplicate "Net cost after HSA tax savings" rows of the results table (they equal the complete cost). Tick **HSA-eligible plan** on any plan card and everything returns. The **HSA-eligible plan** checkbox itself is always shown.

## [2.26.0] - 2026-10-28

### Added
- **Hide checkbox on section 4 (Health plans)**, like sections 1 to 3. Hiding it folds away the Defaults, every plan card and the Add / Load buttons. Nothing is removed: hidden plans keep their values, still count in the results and are saved with the file (`view.secHide.plans`, visible by default).
- **Defaults block inside Health plans.** Values used for any plan that has no value of its own:
  - **Cleanings covered per person per year** (default 2). Used when a plan's dental cleaning has no "Max covered per person per year"; cleanings above it are not covered and you pay their full price. The tooltips and Line-item detail say when the Default was used.
  - **Medication tier 3, per fill** (default $250), used when the plan has no Evaluator price for it.
  - **Part B premium, monthly, in 2026** (default $203) with a **yearly increase** (default 5.25%, compounded). Each Medicare Advantage plan uses the premium for its own plan year (2027 is $213.66, 2028 is $224.87), and a plan's own Part B premium still wins. An optional **override** replaces the calculated amount for every year. A preview of the next years is shown under the fields.

### Changed
- The tier 3 price and the Part B premium moved from section 2 (Costs) to the Defaults block. Saved files are upgraded on load: an old tier 3 price becomes the Default tier 3 price and an old Part B premium becomes the Part B override, so those files give the same results as before. Files that had left them empty now use the new defaults ($250 tier 3, calculated Part B).
- Aetna Medicare Enhanced and Signature plan files updated from the 2027 Summary of Benefits.

## [2.25.1] - 2026-10-27

### Changed
- Tooltips on the cost bars, the totals, the medical max and the legend are now one or two short lines (for example "Medical max $9,258 = premium $2,508 + out-of-pocket max $6,750. Dental not included."). The detailed step-by-step explanations stay on the results table and Line-item detail.

## [2.25.0] - 2026-10-27

### Changed
- **Dental is drawn as its own bar.** Dental out of pocket is no longer part of the "Other costs" segment. It is a violet bar directly below each cost bar, touching its bottom edge and starting where the bar above ends. Space for it is reserved on every row, with or without dental and with or without the stress scenario, so the gaps between rows stay equal. The total at the right of each bar still includes dental.
- **Medical max.** The maximum at the end of each row is now a column labeled "Medical max" (the label is above the values, the rows show only the amount). It no longer includes dental: it is the premiums (plan premium and Part B) + the out-of-pocket maximum + not-covered services. The dashed outline ends at the same value, and the bar scale takes the dental bar into account.
- **Amounts inside the segments.** Premium, other costs, medications and dental show their amount inside the segment, right-aligned, when the segment is wide enough; narrower segments show no label (their tooltips still do). Bars are slightly taller (14 px) to hold the text.
- Tooltips for the other-costs segment, the dental bar, the max and the legend are updated to match.

## [2.24.0] - 2026-10-27

### Changed
- **Top pane colors.** The pane is a deep navy (darker still in dark mode) instead of mid blue. The normal year is teal and the stress scenario amber, each with its own darker premium segment, lighter other-costs segment and striped medications segment, so the two scenarios and their parts are easy to tell apart. Light and dark themes have their own values.
- **Costs section.** The prices are grouped under headings (visits, hospital and surgery; tests and imaging; dental; medications and Medicare premium) on one five-column grid, with short one-line labels so every input lines up.
- The "max possible" tooltips now say premiums are included and itemize them (plan premium and Part B, per enrolled person).

## [2.23.1] - 2026-10-27

### Changed
- The cost bars are sorted from the lowest to the highest normal-year cost. With the stress scenario on, each plan's normal and stress bars move together as a pair.
- Every bar row now has the same height, so the gaps between bars are equal whether a plan name takes one line or two.

## [2.23.0] - 2026-10-27

### Added
- **Stress scenario button.** The toolbar has a **Stress scenario: off/on** button. It is **off by default** (and for files saved before this version). While off, section 3 (Stress scenario), the second bar of each plan and its legend entry, the "With stress" total in the collapsed blue pane, the stress rows of the results table (section 4, the HSA stress rows and "Complete + stress, net") and the "4. With stress" entry of the Show/hide rows menu are all hidden, and the bar scale ignores the stress totals. The choice is saved with the file (`view.showStress`) and in the browser.

### Fixed
- **Dental services limited per year (for example 2 cleanings).** "Max units" on a dental service now means the number the plan covers per person per year. Units above it (per person × people covered) are not covered: you pay their full price, outside the dental annual maximum. Before, a no-charge cleaning limit was ignored (every cleaning counted as free) and a copay limit was applied to the whole household instead of per person. The Max field on dental services is labeled "Max covered per person per year"; the dental tooltips and Line-item detail say how many units are covered and what the extra units cost.
- The Humana Gold Plus, Humana Value Choice, Kaiser Essential King and Kaiser Optimal plan files now carry `max_units: 2` for dental cleanings (the "2 per year" limit was only in the `limits` text). The schema description of `max_units` and the fill prompt explain the dental meaning.

## [2.22.0] - 2026-10-27

### Added
- Section 2 (Costs) has two new fields: **Medication tier 3, per fill** and **Medicare Part B premium, monthly per person**. Each is used by every plan that has no value of its own (the plan's tier 3 Evaluator price, the plan's Part B premium). A value on the plan card still wins. The Part B premium applies to Medicare Advantage plans only and is multiplied by the enrolled people, as before.

## [2.21.0] - 2026-10-27

### Added
- **Dental.** Section 1 has a yearly **Dental** needs block (cleanings, root canals, crowns) and section 2 has the price of each. Every plan card has a **Services: dental** section with a cost share for each, a dental deductible, a dental annual maximum and a "cleanings count toward the maximum" choice.
- Dental is costed outside the medical deductible and out-of-pocket maximum. The deductible and the annual maximum are per person (a couple gets two). The plan pays up to the maximum; you pay everything above it. A dental service with no cost share entered counts as not covered, and a notice says so.
- **Results:** three listed-price rows (dental cleanings, root canals, crowns), an "of which dental" row under the with-deductible total, and dental in the "no deductible limit" total and the bar tooltips. The "max possible" outline includes dental.
- **Line-item detail:** a Dental group with units, base cost, deductible used, what you pay and what insurance pays, a dental summary line, and tooltips that show the deductible and annual maximum.
- Schema 2.2 (2.0 and 2.1 files still load): `services.dental_cleaning`, `dental_root_canal`, `dental_crown`, `limits.dental_deductible`, `dental_annual_max`, `dental_preventive_counts_toward_max`, and the three dental prices under `evaluator_inputs.prices`.
- All nine plan files in `plans/` now carry dental cost shares (Aetna, Humana, Kaiser and Ambetter), with the choices made from the plan pages listed in each file's assumptions. The prompt (`fill-health-plan-prompt.md`) explains how to fill dental.

### Changed
- Results with no dental needs entered are identical to 2.20.0.

## [2.20.0] - 2026-10-27

### Added
- **Collapse button for the blue top pane.** Collapsed, the pane is one row: the toolbar, the tabs and the selected plan's totals (normal year, with stress, premium), with a plan picker. The choice is remembered in the browser.
- **Jump to results** link next to the tabs.
- **Show/hide rows** dropdown in Results replaces the six checkboxes (a checked row is shown; the label says how many are hidden). The saved file format is unchanged.

### Changed
- The blue pane is about 28 % shorter with five plans (411 px to about 290 px): smaller toolbar buttons, tighter bar rows, and a one-line legend whose explanations are on hover.
- Notices and Annual cost table headers use the short plan names of the bars ("KP MA Key King (HMO)") with the full name on hover.
- Notices with identical wording for several plans are merged into one ("Aetna MCR Enhanced, Aetna MCR Signature and 3 others: …").
- The federal tax bracket field and its hint show only when a plan is HSA-eligible.
- Line-item detail summary chips sit in a grid; "You pay + premium" is last and bold.
- Reset is separated from the other buttons at the far end of the toolbar and is labeled "Reset…" (it still asks for confirmation).

### Fixed
- The Evaluator / Line-item detail tabs now expose `aria-selected`, `aria-controls` and arrow-key navigation, and the two views are labeled tab panels.

## [2.19.2] - 2026-10-27

### Changed
- Line-item detail no longer adds a "Prescription out-of-pocket cap … not reached" row to the table. The table shows the cap row only when the cap reduces what you pay; the cap and what you pay for medications stay in the "Max out-of-pocket, drugs" line above the table.

## [2.19.1] - 2026-10-27

### Added
- Line-item detail for Medicare plans shows the drug out-of-pocket maximum: a "Max out-of-pocket, drugs" line in the summary above the table (the cap and what you pay for medications), and a table row that says the cap is not reached and how much is left, or shows the reduction when it is reached.

## [2.19.0] - 2026-10-27

### Added
- **Prescription out-of-pocket cap is now costed.** For Medicare Advantage plans, the "Prescription out-of-pocket cap (per person)" you enter (or import) limits what you pay for medications; a couple uses 2 × the amount, like the Part D deductible. The cap is applied to the medication cost share first, then the combined out-of-pocket maximum applies to the remainder.
- Line-item detail shows a "Prescription out-of-pocket cap reached: reduction" row when the cap applies, and the tooltips on the totals explain it. The cost bars' medication segment shows the capped amount.
- A notice appears for a Medicare plan with no cap entered, saying medication costs are not capped.

### Changed
- The "not modeled" notice and the plan import note no longer list the prescription out-of-pocket cap.
- Results are unchanged when the cap is blank or not reached.

## [2.18.6] - 2026-10-27

### Changed
- The Medicare Advantage notice no longer says "Part B premium counts only if entered" once a Part B premium (including 0) is entered for that plan; the note about what is not modeled stays.

## [2.18.5] - 2026-10-27

### Fixed
- In the blue top pane, the current file name now sits right next to "Current file:" instead of at the far right edge of the window.

## [2.18.4] - 2026-10-27

### Changed
- CSS cleanup with no change in appearance: the rules for the blue top pane are nested inside one `header.top { … }` block instead of repeating the `header.top` prefix 60 times, and the white overlays used there (12, 25, 28, 35, 55 and 60 % opacity) are shared `--w12` … `--w60` variables.
- The page now needs a browser with CSS nesting: Chrome and Edge 112, Safari 16.5 or Firefox 117 or newer. Older browsers lose the top pane styling.
- Comment on `renderResults` saying what it redraws.

## [2.18.3] - 2026-10-27

### Changed
- Code cleanup with no change in results or appearance. The deductible and out-of-pocket maximum lookups share one helper. The HSA check reads each of them once. An unused argument was removed from the out-of-pocket remainder helper.
- CSS: merged the split cost-bar and table-header rules (the table header's duplicate first-column background was dropped), moved the bar animation timing into one `--bar-anim` variable, and replaced repeated inline `margin` styles with `.m0` and `.mt10` classes.

## [2.18.2] - 2026-10-27

### Fixed
- The Annual cost table and the Line-item detail table can now be scrolled to their last row with the column headers still visible. Before, the table frame was a fixed share of the window height and ignored the sticky blue pane, so scrolling to the bottom pushed the table, headers included, behind the pane.

### Changed
- Table frames are sized to the space left below the blue pane (its height is measured and follows the number of result bars; never less than 220 px). Scrolling a table into view stops just below the pane.

## [2.18.1] - 2026-10-27

### Changed
- The Annual cost table (Evaluator tab) and the Line-item detail table scroll vertically inside their own frame, and the column headers stay visible while you scroll.

## [2.18.0] - 2026-10-27

### Changed
- Medicare Advantage plans now have separate deductibles for medical care and medications. The medical deductible (often $0) applies only to medical services, and the Part D drug deductible (per person) applies only to drug tiers marked "deductible applies". Before, one deductible was shared by both, so a $0 medical deductible let the drug deductible be used up by medical services, and a nonzero medical deductible hid the drug deductible.
- Line-item detail, the header summary and the tooltips show the medical and drug deductibles and how much of each is used.
- Marketplace (non-Medicare) plans are unchanged: one deductible shared by medical and drugs.
- The out-of-pocket maximum is still one combined cap; the separate Part D drug out-of-pocket cap is still recorded but not costed.

## [2.17.1] - 2026-10-27

### Changed
- Cost bar names: the first word of a shared name that is not a known term (the organization, such as "Ambetter") is kept in full; the words after it become initials ("Ambetter CS Vital Gold").

## [2.17.0] - 2026-10-27

### Changed
- Cost bars: the leading words a plan name shares with another plan (the health organization and program, such as "Kaiser Permanente Medicare Advantage" or "Ambetter Cascade Select") are abbreviated, so the distinguishing part of the name fits on the two lines. Hover shows the full name. Plan names elsewhere are unchanged.

## [2.16.1] - 2026-10-27

### Changed
- Cost bar x axis now shows 5 to 10 labelled positions. The step is $10k divided by 1, 2, 4 or 5 (so $10k, $5k, $2.5k or $2k; scaled by powers of 10 for very small or large totals), chosen as the finest step that fits within 10 positions.

## [2.16.0] - 2026-10-27

### Added
- Save and Save as… give visible feedback: the button turns green and reads "Saved ✓" for two seconds (red "Save failed" on an error, "Downloaded ✓" in browsers that download instead), and the current file name flashes.

## [2.15.1] - 2026-10-27

### Changed
- Cost bars: plan names wrap onto two lines instead of being cut off after one, so the plan type is visible, not only the organization name. Hover still shows the full name.

## [2.15.0] - 2026-10-27

### Changed
- Cost bars: the paid-out-of-pocket section is renamed **Other out of pocket** and no longer includes medications.
- Medication cost is its own striped segment with a tooltip showing what you pay for each medication tier.
- Premium, other out of pocket and medications each use a different shade (darkest, lightest, and a striped mid-tone), in both the normal-year and stress bars. The legend shows all three.

## [2.14.0] - 2026-10-27

### Changed
- Evaluator and Line-item detail tab selection moved from below the header into the sticky blue top pane, so you can change tabs at any scroll position without scrolling back up to find the tab handles.
- Leaving and returning to a tab keeps its scrolled position (Evaluator and Line-item detail each remember their own). A tab you have not visited yet opens at the top.
- The plan and scenario checkboxes in the blue pane's bars still choose what Line-item detail shows; they work the same as before.

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
