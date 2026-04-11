---
name: prioritization
description: Prioritize a list of features, requests, or initiatives using RICE, MoSCoW, or impact/effort frameworks. Use when the user needs help ranking or triaging product work.
disable-model-invocation: true
---

Help prioritize: $ARGUMENTS

Use the template in [rice-template.md](rice-template.md) as the structure.

Follow this process:
1. **Identify the framework** — default to RICE unless the user specifies MoSCoW or impact/effort matrix.
2. For **RICE scoring**, score each item on:
   - **Reach**: How many users affected per quarter? (number)
   - **Impact**: How much does it move the needle per user? (3=massive, 2=high, 1=medium, 0.5=low, 0.25=minimal)
   - **Confidence**: How confident are you in your estimates? (100%/80%/50%)
   - **Effort**: Person-weeks of work (lower = better)
   - **RICE Score** = (Reach × Impact × Confidence) / Effort
3. For **MoSCoW**, categorize each item as Must Have / Should Have / Could Have / Won't Have with a one-line rationale.
4. For **Impact/Effort Matrix**, place items in four quadrants: Quick Wins / Big Bets / Fill-ins / Time Sinks.
5. Produce a ranked table with scores and a brief recommendation section explaining the top priorities and any notable trade-offs.

Ask the user which framework they prefer if not specified. Output a table suitable for sharing in a planning doc.
