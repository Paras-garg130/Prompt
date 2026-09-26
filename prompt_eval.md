# Prompt Evaluation Report

## Overall Score

| Parameter | Score |
|---|---:|
| Prompt Clarity | 80 / 100 |
| Output Quality | 39 / 100 |
| Efficiency | 30 / 50 |
| **Total** | **149 / 250** |

## Executive Summary

The prompt has a memorable business scenario, clear phase boundaries, concrete product cost anchors, and a useful set of requested deliverables. It should reliably produce an energetic, structured business plan. Its weakest point is financial reproducibility: selling prices and inventory quantities are unconstrained, “margin” is undefined, and profit-based reinvestment is requested without specifying sales, expenses, or accounting assumptions. It also omits food-safety and local-compliance guardrails and provides no fallback for infeasible timing or throughput assumptions. The rewrite below retains the concept while requiring auditable calculations and explicitly labeled assumptions.

## Evaluated Prompt Analysis

**Source:** `project_canteen_cult_prompt(1).md`  
**Estimated length:** approximately 400 tokens (rough estimate; tokenizer-dependent).  
**Structure:** A scenario-setting directive, four persona-led phases, embedded product and cost assumptions, phase-specific deliverables, and a final style rule. It contains no variable placeholders or example outputs.

### Prompt Text Evaluated

> **System Directive:** Activate "Project Canteen Cult." You will execute a comprehensive 4-phase strategy to flip the standard college canteen into a high-profit, viral sensation within exactly 7 days, using a strict ₹10,000 micro-budget.
>
> Follow the strict phase-by-phase persona mapping and constraints below.
>
> ### PHASE 1: The "Drop Culture" Scarcity Menu (Adopt Persona: Viral Street-Food Chef)
> Design an ultra-fast prep menu limited to exactly 3 killer items targeted at stressed tech and AI students.
> * **Item 1:** A signature loaded Chilli Potato bowl. (Assume ₹20 raw cost)
> * **Item 2:** A handheld Paneer Dosa fusion wrap. (Assume ₹30 raw cost)
> * **Item 3:** An artisanal iced mocktail/coffee. (Assume ₹15 raw cost)
> * **Deliverable:** For each item, provide a Catchy Name, Core Ingredients, Prep Time (must be under 3 minutes assuming a 2-person prep team), and the psychological hook (why students will crave it).
>
> ### PHASE 2: The ₹10,000 Micro-Economy (Adopt Persona: Ruthless Startup CFO)
> * **The Day 1 Budget (Markdown Table):** Allocate exactly ₹8,000 to initial stock and ₹2,000 for a "Hype Fund." Use the anchor raw costs provided in Phase 1.
> * **Required Columns:** Item/Expense | Raw Cost per Unit (₹) | Selling Price (₹) | Margin (%) | Daily Volume Limit | Total Initial Spend (₹).
> * **The Reinvestment Loop:** In a separate bulleted section strictly *below* the table, mathematically explain how Day 1 and Day 2 profits are dynamically reinvested to scale inventory for the Day 5-7 peak.
>
> ### PHASE 3: Crowd Control & The Hype Engine (Adopt Persona: Behavioral Psychologist)
> Weaponize the 45-minute peak lunch rush bottleneck. Assume a single service window.
> * **Scarcity Model:** Outline a psychological FOMO strategy (e.g., limited daily "drops" where only 50 wraps are available at exactly 1:15 PM).
> * **Frictionless Ordering:** Design a high-speed, zero-cost queuing system (e.g., color-coded tokens for exact UPI payments or a WhatsApp fast-lane) that eliminates line fatigue.
>
> ### PHASE 4: The 7-Day Escalation Protocol (Adopt Persona: Disruptive Food-Tech Founder)
> Provide a high-energy, authoritative day-by-day roadmap.
> * **Day 1-2:** The Hook (Taste-testing and aggressive word-of-mouth).
> * **Day 3-5:** The Scale (Optimizing the prep-line to handle maximum throughput).
> * **Day 6-7:** The Cash Out (Profit maximization and aggressive inventory clearance for zero waste).
>
> **Output Rules:** Use high-energy, authoritative language. Employ bold headers, concise bullet points, and absolutely zero generic cafeteria advice. Think like a founder executing a hostile takeover.

## Detailed Parameter Breakdown

### 1. Prompt Clarity: 80 / 100

| Criterion | Score | Assessment |
|---|---:|---|
| Role & Persona Definition | 17 / 20 | Four phases assign distinct perspectives: “Viral Street-Food Chef,” “Ruthless Startup CFO,” “Behavioral Psychologist,” and “Disruptive Food-Tech Founder.” Their expertise is evocative but not operationally defined. |
| Task Specificity & Negative Constraints | 20 / 25 | Exact product count, product concepts, unit costs, prep-time ceiling, budget split, and seven-day timeline are specified. Negative boundaries beyond “zero generic cafeteria advice” are limited. |
| Instruction Structure & Delimiters | 18 / 20 | Four labeled phases and bullets make deliverables easy to locate. The budget table has required columns, but no dedicated assumptions or calculation definitions are requested. |
| Tone, Style & Target Audience | 13 / 15 | “High-energy, authoritative” and “stressed tech and AI students” establish a strong voice and audience. Reader expertise and acceptable level of hype are not bounded. |
| Unambiguous Language | 12 / 20 | “Exactly ₹10,000,” “high-profit,” “maximum throughput,” and “zero waste” sound precise but lack measurable definitions. “Margin (%)” has multiple common definitions, and “under 3 minutes” does not say whether it means active assembly or order-to-handoff time. |

**Strengths:** “limited to exactly 3” and “using a strict ₹10,000 micro-budget” are crisp constraints. Phase headings make the required sequence explicit.

**Gaps:** “Allocate exactly ₹8,000 to initial stock” does not state how to express inventory quantities or reconcile each row to that sum. “Maximum throughput” has no numerical service capacity target.

### 2. Output Quality & Schema Compliance: 39 / 100

| Criterion | Score | Assessment |
|---|---:|---|
| Output Format & Schema Enforcement | 22 / 30 | A Markdown budget table with named columns, separate reinvestment bullets, bold headers, and concise bullets are required. No required day-by-day fields, calculation notation, or final consistency check is defined. |
| Few-Shot Examples & In-Context Demonstrations | 0 / 25 | The prompt gives illustrative tactics, such as a 1:15 PM wrap drop, but no input/output example that demonstrates the desired full answer or calculation style. |
| Edge Cases & Fallback Instructions | 9 / 25 | It includes scenario assumptions (two-person team and single service window), but no instruction for infeasible prep or rush targets, missing data, weak demand, unsold perishables, or payment-channel limitations. |
| Factuality & Hallucination Prevention | 8 / 20 | The three raw costs are explicitly labeled assumptions. There is no broader rule to distinguish assumptions from facts, avoid unsupported demand claims, or flag that real costs and local requirements need verification. |

**Strengths:** Product costs and operating assumptions are supplied instead of leaving the entire plan unconstrained. Specific output elements (name, ingredients, prep time, hook) help drive useful menu descriptions.

**Gaps:** The requested “Day 1 and Day 2 profits” cannot be calculated uniquely without selling prices, units sold, and treatment of the ₹2,000 hype spend. The prompt also does not distinguish revenue, gross profit, and cash available for restocking.

### 3. Efficiency & Token Economy: 30 / 50

| Criterion | Score | Assessment |
|---|---:|---|
| Conciseness & Fluff Elimination | 10 / 15 | Most text sets a task or constraint, but repeated persona labels and phrases such as “killer,” “weaponize,” and “hostile takeover” spend tokens on voice rather than execution detail. |
| Token Economy & Context Footprint | 11 / 15 | The four-phase structure is information-dense. Some evocative instructions duplicate the final tone directive, while essential finance definitions are missing. |
| Dynamic Parameterization | 1 / 10 | Costs and timeline are embedded as fixed values; no reusable fields are marked for location, opening days, existing equipment, or available staff. |
| Signal-to-Noise Ratio | 8 / 10 | Required products, costs, phases, and deliverables are visible and prioritized. High-energy wording competes slightly with the exact operational requirements. |

## Actionable Recommendations

1. Define margin as `(selling price - raw cost) / selling price × 100` and state whether the result is gross margin before overhead.
2. Require a quantity per product and show unit cost × quantity = initial stock spend; verify the three product totals equal ₹8,000 and the hype fund equals ₹2,000.
3. Specify an auditable sales scenario for Day 1 and Day 2. Separate revenue, cost of goods sold, operating expenses, profit, and cash reinvested; label any demand or sell-through figures as assumptions.
4. Clarify whether the three-minute prep target is active preparation or order-to-handoff time, and request a realistic capacity calculation for a 45-minute rush and one service window.
5. Add fallback and risk instructions for infeasible throughput, low demand, unsold perishables, and assumptions that need local validation.
6. Keep the requested energetic voice, but prohibit coercive, deceptive, or unsafe tactics and require local food-safety, allergen, and payment-process compliance to be verified rather than invented.

## Optimized Prompt Rewrite (Production-Ready)

```text
<role>
You are a practical food-service launch planner combining menu development, small-business finance, queue operations, and marketing. Build an energetic but feasible seven-day plan for a college canteen serving tech and AI students.
</role>

<fixed_context>
Budget: ₹10,000 total.
Initial stock allocation: exactly ₹8,000.
Promotion allocation: exactly ₹2,000 (the "Hype Fund").
Team: two people. Service: one window. Peak lunch period: 45 minutes.
Product raw costs per sellable unit, treated as supplied assumptions:
- Chilli Potato bowl: ₹20
- Paneer Dosa fusion wrap: ₹30
- Iced mocktail or coffee: ₹15
Timeline: seven days.
</fixed_context>

<task>
Create the plan in four numbered phases and in this order.

1. MENU: Propose exactly three items, one based on each supplied product. For each, give a catchy name, core ingredients, estimated active prep time, and a brief appeal to students. Keep active prep under three minutes per item for a two-person team; state any batch-prep assumption. Do not imply that the three-minute target is order-to-handoff time unless the workflow supports it.

2. BUDGET AND REINVESTMENT: Provide a Markdown table with these columns: Item/Expense, Raw Cost per Unit (₹), Selling Price (₹), Gross Margin (%), Initial Quantity, Daily Volume Limit, Initial Spend (₹). Include all three stock items and a Hype Fund row. For the fund row, use N/A for per-unit fields. Include a total row. Choose integer quantities and selling prices so product inventory totals exactly ₹8,000, the Hype Fund is exactly ₹2,000, and the full budget is exactly ₹10,000. Show the arithmetic or a brief reconciliation beneath the table.

Define gross margin as (selling price - raw cost) / selling price × 100, rounded to one decimal place. This is before labor, utilities, spoilage, and other overhead. Do not call it markup or net profit.

Then show a separate Day 1 and Day 2 worked example. State assumed units sold and any additional cash expenses; label them as assumptions, not facts. For each day show revenue, cost of units sold, gross profit, cash expenses, net operating profit, and amount available/reinvested in stock. Do not count inventory purchases twice. Explain how the resulting cash supports Days 3-7, and flag if the plan depends on selling all available stock.

3. RUSH AND ORDERING: Give a scarcity/drop schedule that is honest about actual quantities and availability. Design a zero-cost queue and payment flow for one service window. Estimate orders served in 45 minutes from the proposed workflow; show the assumed service rate and identify the bottleneck. Do not promise a throughput level the two-person team cannot support.

4. SEVEN-DAY ROADMAP: Give one concise entry for each day. Cover taste testing and feedback (Days 1-2), measured workflow adjustments and scaling (Days 3-5), then demand-led inventory and waste control (Days 6-7). Include a measurable action or decision signal each day.
</task>

<constraints>
- Keep the tone energetic, direct, and founder-minded; use bold phase headings and concise bullets.
- Avoid generic cafeteria advice, fabricated market statistics, and guaranteed profit or virality claims.
- Distinguish supplied facts from assumptions. If a calculation needs unavailable information, state the assumption and show its effect.
- Do not recommend deceptive scarcity, coercive marketing, unsafe food handling, or noncompliant payment practices. Note that local food-safety, allergen, licensing, and payment requirements must be checked; do not invent rules.
- Minimize waste: use conservative replenishment and a clear response to unsold perishable stock.
- Finish with a compact consistency check confirming the item count, budget totals, margin formula, and seven-day coverage.
</constraints>
```