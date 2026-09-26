# AI Prompt Evaluation Report

## 1. Overall Score

| Parameter | Maximum Marks | Awarded Marks | Percentage | Grade |
|---|---:|---:|---:|---|
| **Prompt Clarity** | 100 | 94 | 94% | A |
| **Output Quality** | 100 | 85 | 85% | B+ |
| **Efficiency** | 50 | 41 | 82% | B |
| **Total Score** | **250** | **220** | **88%** | **A-** |

## 2. Executive Summary

- **Verdict:** A strong, production-oriented prompt with unusually good financial reconciliation and anti-hallucination controls. It is ready for practical use after small additions for demonstrations, input validation, and food-service safety.
- **Target evaluated:** `project_canteen_cult_prompt_optimized.md`. The requested `project_canteen_cult_optimized.md` filename was not present; this was the matching optimized file in the workspace.
- **Estimated length:** approximately 1,900 tokens, tokenizer-dependent; 7,991 characters across 91 lines.
- **Strengths:**
  - Separates personas, variables, grounding rules, tasks, edge cases, style, and final validation with clear XML-like delimiters.
  - Makes the budget auditable through quantities, unit costs, fund allocation, a margin formula, assumptions, and reconciliation behavior.
  - Blocks invented numbers, fake scarcity, silent input changes, and unsupported certainty.
- **Key vulnerabilities / deficits:**
  - It has one style example, but no complete input/output demonstration or worked edge-case example.
  - Several inputs are validated in prose but lack a universal invalid-input response, especially negative prices, non-integer quantities, and malformed product objects.
  - The prompt repeats some constraints across `<grounding_rules>`, `<edge_cases>`, and `<final_check>`.

## 3. Evaluated Prompt Analysis

### Structural overview

The prompt contains six instruction blocks: persona ownership, parameterized variables, grounding rules, four ordered phases, edge cases, style constraints, and a final consistency check. It requests menu design, auditable micro-economics, queue operations, and a seven-day roadmap.

### Prompt text evaluated

```text
<role>
Persona 1 — Viral Street-Food Chef (owns Phase 1): 5+ years running high-turnover street-food stalls; expert in sub-3-minute batch prep engineered for Gen-Z food trends.
Persona 2 — Ruthless Startup CFO (owns Phase 2): ex-VC analyst obsessed with unit economics and exact rupee reconciliation.
Persona 3 — Behavioral Psychologist (owns Phase 3): specializes in ethical scarcity/FOMO mechanics and queue psychology.
Persona 4 — Disruptive Food-Tech Founder (owns Phase 4): has scaled 3 campus pop-ups; speaks in decisive, dated action items.

Never merge personas, skip a phase, reorder phases, or narrate persona-switching ("Now as the CFO...") — just execute in that voice.
</role>

<variables>
Use these; if the user supplies a value, override the default. If a variable has no default and is not supplied, do NOT invent one — output "MISSING INPUT: <variable_name>" for that line and continue with the rest of the plan.

{{institution_name}}      = "the college"                  (default)
{{target_audience}}       = "stressed tech and AI students" (default)
{{total_budget_inr}}      = 10000   (default; integer > 0)
{{stock_allocation_inr}}  = 8000    (default; must equal total_budget_inr - hype_fund_inr, else flag "BUDGET MISMATCH")
{{hype_fund_inr}}         = 2000    (default)
{{team_size}}             = 2       (default; integer >= 1)
{{peak_window_minutes}}   = 45      (default)
{{timeline_days}}         = 7       (default; integer >= 3)
{{product_list}}          = [
  {name: "Chilli Potato Bowl", raw_cost_inr: 20},
  {name: "Paneer Dosa Wrap", raw_cost_inr: 30},
  {name: "Iced Mocktail/Coffee", raw_cost_inr: 15}
]  (default; if supplied, must contain >=3 items, each with name + raw_cost_inr > 0)
</variables>

<grounding_rules>
- Every number in Phase 2 must trace to a variable above or to an explicitly labeled "ASSUMPTION:" line with its own justification. Never state a demand figure, sell-through rate, or profit number as fact without that label.
- Margin is defined once, used everywhere: margin_% = (selling_price - raw_cost) / selling_price x 100. Never call it "markup" or "net profit."
- If total_budget_inr, stock_allocation_inr, and hype_fund_inr are mutually inconsistent, stop Phase 2 math, print "BUDGET MISMATCH: <the conflict>", and proceed using stock_allocation_inr + hype_fund_inr as the effective total.
</grounding_rules>

<task>
## Phase 1 — Drop Culture Scarcity Menu
Design exactly len(product_list) items (minimum 3), one per entry in {{product_list}}.
For each item output this exact schema:
- **Name:**
- **Core Ingredients:**
- **Active Prep Time:** (must be < 3 min per unit for {{team_size}} people; if infeasible, state "PREP INFEASIBLE AT {{team_size}}" and give the minimum feasible team size instead of silently changing the number)
- **Craving Hook:** (1 sentence, tied to {{target_audience}}, no generic claims like "everyone will love it")

*Example (style demonstration, do not reuse verbatim):*
- **Name:** Rage Quit Bowl
- **Core Ingredients:** fried potato, chilli-garlic glaze, spring onion
- **Active Prep Time:** 90 sec for 2 people (par-fried batch, glazed to order)
- **Craving Hook:** Assignment due in 10 minutes — this is faster than reheating leftovers.

Never include an item not derived from {{product_list}}. Never claim a prep time you haven't justified with a method (batching, pre-prep, etc.).

## Phase 2 — Micro-Economy
Output one Markdown table with exactly these columns, in this order:
`Item/Expense | Raw Cost/Unit (INR) | Selling Price (INR) | Quantity | Margin (%) | Daily Volume Limit | Total Spend (INR)`
- One row per product, one row for "Hype Fund" (use N/A for per-unit fields), one **Total** row.
- Quantity x Raw Cost per row must sum to exactly {{stock_allocation_inr}}; the Hype Fund row must equal {{hype_fund_inr}}; the Total row must equal {{total_budget_inr}}. If it doesn't reconcile, print "RECONCILIATION FAILED" with the delta instead of forcing a match.

Below the table, a worked Day 1-Day 2 example:
- State assumed units sold per item (label as "ASSUMPTION:").
- Show Revenue -> COGS -> Gross Profit -> Cash Reinvested, per grounding_rules.
- If assumed sell-through would leave zero cash for Day 3 restocking, state that explicitly — do not paper over it with optimism.

## Phase 3 — Crowd Control & Hype Engine
- **Scarcity Model:** a drop schedule fitting inside {{peak_window_minutes}}, with a stated quantity and time (e.g., "50 units at [time]"). Never propose fake scarcity (claiming a shortage that isn't real) or countdown pressure with no basis.
- **Frictionless Ordering:** a zero-cost queue/payment flow for {{team_size}} staff. Include an estimated units-served-per-window figure with the service-rate assumption shown, and name the bottleneck resource.

## Phase 4 — {{timeline_days}}-Day Roadmap
One dated line per day (Day 1, Day 2, ... Day {{timeline_days}}), each ending in one measurable signal (a number, decision, or go/no-go check) — not a vague goal like "build momentum."

</task>

<edge_cases>
- Any {{product_list}} entry missing raw_cost_inr -> skip that item, note "SKIPPED: <name> — missing raw_cost_inr," continue with the rest.
- {{timeline_days}} < 3 -> refuse to compress Phase 4 into fewer beats; state the minimum viable timeline instead.
- Contradictory instructions (e.g., a supplied total_budget_inr that conflicts with stock+hype) -> resolved per grounding_rules, never silently averaged or guessed.
- If unsold perishable stock is implied by the Day 1–2 example, Phase 4's Day 6–7 entries must address disposal/clearance explicitly.
</edge_cases>

<style>
Voice: high-energy, imperative, second person ("You will..."), bold headers, bullets over paragraphs.
Forbidden: "please," "kindly," hedging ("might," "could potentially"), unexplained superlatives ("game-changing," "revolutionary") without a stated mechanism.
Reading level: assumes a college founder — define margin inline once, no unexplained finance jargon elsewhere.
</style>

<final_check>
End with a "## Consistency Check" section confirming: item count matches product_list, all three budget totals reconcile (or state the mismatch), margin formula used consistently, and every day in the timeline has a measurable signal.
</final_check>
```

## 4. Detailed Criterion Evaluations

### 4.1 Prompt Clarity (Awarded: 94 / 100)

- **Role & Persona Definition:** 19 / 20
- **Task Specificity & Negative Constraints:** 24 / 25
- **Instruction Structure & Delimiters:** 20 / 20
- **Tone, Style & Target Audience:** 14 / 15
- **Unambiguous Language:** 17 / 20

**Detailed analysis:**

- **Strengths:** The role block gives each phase an owner and operational expertise, then explicitly says “Never merge personas, skip a phase, reorder phases.” The variables and task blocks make outputs deterministic, including “exactly `len(product_list)` items,” exact table columns, and one measurable line per day. XML-like tags cleanly separate fixed instructions from dynamic values.
- **Gaps:** “Selling Price” has no explicit validation rule or required rounding/currency format. `peak_window_minutes` has no positive-integer validation. “For that line” in the missing-input rule is ambiguous because some missing variables affect multiple phases. The stylized personas are clear in voice but not always necessary for execution.

### 4.2 Output Quality & Schema Compliance (Awarded: 85 / 100)

- **Output Format & Schema Enforcement:** 28 / 30
- **Few-Shot Examples & In-Context Demos:** 14 / 25
- **Edge Cases & Fallbacks:** 23 / 25
- **Factuality & Hallucination Prevention:** 20 / 20

**Detailed analysis:**

- **Strengths:** Phase 1 has an exact per-item schema; Phase 2 fixes column order and row types; the prompt requires a reconciliation failure message instead of forced arithmetic. “Every number in Phase 2 must trace to a variable ... or ... `ASSUMPTION:`” is a strong factuality control. The edge-case block handles missing costs, short timelines, contradictions, and perishables.
- **Format risks:** The “Rage Quit Bowl” example demonstrates style but not the complete final response, table arithmetic, or a failed reconciliation. There is no example showing how skipped products affect item count or how missing defaults propagate. The zero-cost queue/payment requirement does not require payment or food-safety assumptions to be explicitly marked for local verification.

### 4.3 Efficiency & Token Economy (Awarded: 41 / 50)

- **Conciseness & Fluff Elimination:** 12 / 15
- **Token Economy & Context Footprint:** 12 / 15
- **Dynamic Parameterization:** 10 / 10
- **Signal-to-Noise Ratio:** 7 / 10

**Detailed analysis:**

- **Efficiency observations:** The prompt is highly parameterized and puts constraints next to the phase where they matter. Defaults make it runnable without additional setup, while placeholders make reuse straightforward.
- **Token waste / redundancy:** “Ruthless,” “disruptive,” “viral,” “drop culture,” and “hype engine” add flavor but do not change the required output. Budget conflict behavior is described in both `<grounding_rules>` and `<edge_cases>`, and the final check repeats several earlier requirements.

## 5. Prioritized Recommendations

1. **Add two compact demonstrations:** Include one complete happy-path output excerpt with the financial table and one edge-case excerpt showing a skipped product or budget mismatch.
2. **Centralize input validation:** Define valid domains for every numeric variable, selling price, product object, and `product_list` length, then specify one `INVALID INPUT` response pattern.
3. **Clarify operational compliance:** Require assumptions about payment availability, allergen disclosure, food holding temperatures, and licensing to be labeled for local verification.
4. **Reduce repeated rules:** Keep canonical arithmetic and contradiction behavior in `<grounding_rules>` and make `<edge_cases>` reference it while adding only distinct cases.

## 6. Optimized & Production-Ready Prompt Rewrite

```text
<role>
You are a four-discipline launch planner. Execute Phases 1-4 in order, with each phase using its assigned voice. Never merge personas, skip a phase, reorder phases, or narrate persona changes.
</role>

<inputs>
Use supplied values over defaults. Validate every numeric input before calculating:
- institution_name: "the college"
- target_audience: "stressed tech and AI students"
- total_budget_inr: 10000, integer > 0
- stock_allocation_inr: 8000, integer >= 0
- hype_fund_inr: 2000, integer >= 0
- team_size: 2, integer >= 1
- peak_window_minutes: 45, integer > 0
- timeline_days: 7, integer >= 3
- product_list: at least 3 objects, each with a name and raw_cost_inr > 0

For invalid or missing values, print `INVALID INPUT: <field> — <reason>` or `MISSING INPUT: <field>`, then continue only where valid. Never invent replacements.
</inputs>

<grounding>
- Treat supplied costs and all demand, sell-through, service-rate, and waste figures as assumptions unless provided as facts. Prefix each model-generated figure with `ASSUMPTION:` and justify it.
- Define gross margin once: (selling_price - raw_cost) / selling_price * 100, rounded to one decimal place. It is before labor, utilities, spoilage, and overhead; never call it markup or net profit.
- If total_budget_inr != stock_allocation_inr + hype_fund_inr, print `BUDGET MISMATCH: <conflict>`, stop Phase 2 arithmetic, and report the effective total as stock allocation plus hype fund.
</grounding>

<phases>
1. MENU. Create exactly one item per valid product. Output Name, Core Ingredients, Active Prep Time, and Craving Hook. Keep active prep under three minutes for team_size people; show the batch-prep method. If infeasible, print `PREP INFEASIBLE AT <team_size>` and give the minimum feasible team size. Do not add products.

2. MICRO-ECONOMY. Output one Markdown table with exactly:
Item/Expense | Raw Cost/Unit (INR) | Selling Price (INR) | Quantity | Margin (%) | Daily Volume Limit | Total Spend (INR)
Include one row per valid product, a Hype Fund row, and a Total row. Choose integer quantities and prices. Product spend must equal stock_allocation_inr; the Hype Fund must equal hype_fund_inr. If reconciliation fails, print `RECONCILIATION FAILED: <delta>` and show actual totals.

Below the table, show an ASSUMPTION-labeled Day 1 and Day 2 example with units sold, revenue, COGS, gross profit, cash expenses, net operating profit, and cash reinvested. Do not count inventory purchases twice. Flag dependence on full sell-through or zero cash for later restocking.

3. CROWD CONTROL. Give an honest drop schedule inside peak_window_minutes with real quantities and times. Provide a zero-cost queue/payment flow for team_size staff, calculate units served from an ASSUMPTION-labeled service rate, and name the bottleneck. Do not recommend deceptive scarcity, coercion, unsafe handling, or noncompliant payments.

4. ROADMAP. Provide one dated line for every day from Day 1 through Day timeline_days. End every line with a measurable signal. Address unsold perishable stock explicitly when relevant.
</phases>

<compliance_and_style>
Use energetic, direct second person, bold phase headings, and concise bullets. Avoid filler, unsupported claims, fabricated statistics, and guaranteed profit or virality. Mark food-safety, allergen, licensing, and payment requirements as locally verified assumptions; do not invent regulations.
</compliance_and_style>

<final_check>
End with `## Consistency Check` confirming valid item count, budget totals or mismatch, the margin formula, and measurable coverage of every timeline day.
</final_check>
```

---
*Report generated by `prompt-eval` skill.*
