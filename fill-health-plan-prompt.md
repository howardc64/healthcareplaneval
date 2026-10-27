# Prompt: fill a health plan file (schema 2.1)

Give an LLM that reads PDFs: `health-plan.schema.json`, the plan's documents, and this prompt. Save its JSON answer as `<name>.plan.json` and load it with **Load health plan**.

---

You fill one JSON file that follows `health-plan.schema.json` (schema_version "2.1").

Documents: for a marketplace plan, the Summary of Benefits and Coverage plus the marketplace plan-details page (premium). For a Medicare Advantage plan, the carrier's plan-details page and, if provided, the Summary of Benefits and Evidence of Coverage.

Rules:
1. Facts only. Copy what the documents say. If a value is not stated, use null (or omit it). Never guess a price.
2. Every cost share has a `structure` (copay, coinsurance, no_charge, not_covered, not_applicable, unknown). Use `coinsurance_pct` for YOUR share, `deductible_applies` true/false/null, and a short `source_text` quote (max 300 characters).
3. Marketplace plans: leave `plan_category` out (or "marketplace"). Medicare Advantage plans: set `plan_category` to "medicare_advantage", `medicare_coverage_type` ("MA" or "MAPD"), `plan_id` (contract-plan id), `service_area`, and fill the required `plan.medicare` block.
4. Medicare amounts are per person: put them in `deductible_individual` and `oop_max_individual`, set `limits.individual_only` true and leave family amounts null. `premium.per_person` is true.
5. Put in-network amounts in `services` and out-of-network amounts in `out_of_network_services`. Put dental, vision, hearing, fitness, transportation and meals in `supplemental_benefits`.
6. Drugs: `tier1_generic` .. `tier5` are positional (Tier 1..5). Put the plan's best everyday channel there (for Medicare, preferred retail, 30 days), list every channel in `drugs.pharmacy_channels`, and record the tier names in `drugs.tier_labels`. Put a separate Part D deductible in `limits.drug_deductible` and the prescription cap in `limits.drug_oop_max`.
7. Hospital copays per day with a day limit: unit "day" and `max_units` (for example 5). Put anything the structure cannot hold (such as free first days) in `limits`.
8. Put your own dollar estimates only in `evaluator_inputs.prices`, never in `services`.
9. Fill `extraction`: confidence (high, medium, low), assumptions (what you inferred or took from a different line), and notes.
10. Answer with the JSON only.
