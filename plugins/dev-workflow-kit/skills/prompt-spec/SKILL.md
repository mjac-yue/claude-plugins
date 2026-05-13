---
name: prompt-spec
description: Design and document a prompt pipeline for an AI feature — covering system prompt design, context assembly, token budget, versioning, retrieval strategy (if RAG), evaluation criteria, and fallback behavior. Use after the tech spec is approved and before the dev plan, when the feature includes LLM, embedding, or RAG components. Output is a prompt specification that engineers can implement and the team can evaluate against.
disable-model-invocation: true
---

Design a prompt specification for: $ARGUMENTS

> **Learning note — Prompt Pipeline Design**
> A prompt is not just text — it is the interface between your system and the AI model. Like an API, a prompt has a contract: given these inputs, in this format, the model produces outputs within these boundaries. Unlike an API, prompts are non-deterministic, sensitive to wording, and can degrade silently as inputs vary in production. Designing a prompt pipeline means specifying the full contract: what the system prompt says and why, what data is injected and how, what the token budget is, how quality is measured, and what happens when things go wrong. A prompt specification written before implementation catches design issues when they're cheap to fix — not after you've built a product around a prompt that doesn't hold up at scale.

Display the learning note above verbatim to the user before proceeding.

**Output standard — tables**: All documents are read in Obsidian. Always include a blank line before any Markdown table. Obsidian requires this to render `|` syntax as a table rather than plain text.

---

## Step 0: Read inputs

Before designing the prompt pipeline, read:
- **Tech spec** (`dev/tech-spec.md`) — for the decided AI stack: model provider, model tier, embedding model, evaluation framework
- **PRD** (`pm/prd.md`) — for AI requirements: quality thresholds, latency SLA, cost constraint, human override requirements, transparency requirements
- **User stories** (`pm/user-stories.md`) — for the specific tasks the AI must perform and the acceptance criteria it must meet
- **Design handoff** (`design/design-handoff.md`) — for the interaction model: streaming vs. batch, loading states, error states

If any of these are missing, note what's absent and proceed with what's available.

---

## Step 1: AI component inventory

Identify all distinct AI calls this feature makes. Each call is a separate prompt — do not treat them as one specification.

| AI call | Purpose | Model tier | Execution model | Frequency |
|---------|---------|-----------|----------------|-----------|
| [e.g., "Generation"] | [What this call produces for the user] | [e.g., Claude Sonnet] | Sync / Async / Background | [Per request / Batch] |

If there are multiple AI calls, produce a separate prompt spec (Steps 2–7) for each.

---

## Step 2: System prompt design

For each AI call, design the system prompt:

### Purpose statement
One sentence: what must this prompt make the model do? State it as a behavioral constraint, not a feature description.

*Example: "Generate a concise summary of the user's uploaded document that accurately represents the main argument without adding interpretation."*

### System prompt structure
Document each section of the system prompt and its purpose:

| Section | Purpose | Key content |
|---------|---------|-------------|
| **Role** | Establish model persona and scope | [e.g., "You are a financial document summarizer..."] |
| **Task** | Define exactly what the model must do | [Specific instructions] |
| **Constraints** | What the model must never do | [e.g., "Never add information not present in the document"] |
| **Output format** | Format, length, and structure of the response | [e.g., "Respond in 3–5 bullet points, each under 20 words"] |
| **Tone** | Voice and register | [e.g., "Professional, neutral, no hedging language"] |
| **Safety** | Content boundaries | [What content to refuse or redirect] |

### System prompt draft
Write the full system prompt text. Be explicit — vague instructions produce vague outputs.

```
[System prompt text here]
```

### Design rationale
For each non-obvious instruction in the system prompt, note why it's there. Instructions without rationale get deleted when prompts are iterated, causing regressions.

| Instruction | Why it's there |
|-------------|----------------|
| | |

---

## Step 3: Context assembly

Define exactly what is injected into each prompt call, from where, and in what format.

| Context element | Source | Format | Required / Optional | Notes |
|----------------|--------|--------|---------------------|-------|
| [e.g., "User message"] | User input | Raw text | Required | |
| [e.g., "Document content"] | Database / file store | Truncated to [X] chars | Required | |
| [e.g., "User history"] | Session / DB query | Last [N] items as JSON | Optional | |
| [e.g., "Current date"] | Server time | ISO 8601 string | Required | Prevents stale reasoning |

**PII handling**: For each context element, note whether it contains PII and confirm whether sending it to the AI API is compliant with the data processing agreements in place.

| Context element | Contains PII? | PII type | Compliant to send? | Mitigation if not |
|----------------|--------------|----------|--------------------|-------------------|
| | Yes / No | | Yes / No / Check required | |

---

## Step 4: Token budget

Define the token budget for each AI call.

| Budget element | Allocation | Rationale |
|---------------|------------|-----------|
| **System prompt** | ~[X] tokens | |
| **Context injection** | ~[X] tokens (max) | |
| **User message** | ~[X] tokens (max) | |
| **Total input budget** | ~[X] tokens | Must be below model context window |
| **Output budget** | ~[X] tokens (max) | Set via `max_tokens` parameter |
| **Context window** | [Model's limit] tokens | [e.g., Claude Sonnet: 200K] |
| **Buffer** | [X]% headroom | For prompt iteration without hitting limit |

**Overflow handling**: What happens when input exceeds the budget?
- [ ] Truncate oldest context (specify which element and from which end)
- [ ] Summarize context before injection
- [ ] Return an error to the user
- [ ] Split into multiple calls

---

## Step 5: RAG pipeline *(complete if retrieval is involved; delete if not)*

### Retrieval strategy

| RAG element | Decision | Rationale |
|-------------|---------|-----------|
| **Embedding model** | [e.g., text-embedding-3-small] | |
| **Vector store** | [e.g., pgvector, Pinecone] | |
| **Chunk size** | [X] tokens | [Why this size for this content type] |
| **Chunk overlap** | [X] tokens | [Why this overlap] |
| **Retrieval strategy** | Dense / Sparse / Hybrid | |
| **Top-K** | [N] chunks retrieved | |
| **Reranking** | Yes / No — [tool if yes] | |
| **Similarity threshold** | [X] minimum score | [Chunks below this are discarded] |

### Retrieved content injection
How are retrieved chunks inserted into the prompt?

```
[Template showing how retrieved content is formatted and positioned in the prompt]
```

### Retrieval failure handling
What happens when retrieval returns no results above the similarity threshold?
- [ ] Proceed without context (with explicit instruction to say "I don't know")
- [ ] Return a user-facing message and do not call the model
- [ ] Fall back to a non-RAG response path

---

## Step 6: Versioning and rollback

| Versioning element | Decision |
|-------------------|---------|
| **Prompt storage** | Inline in code / External config file / Prompt management service: [tool] |
| **Version identifier** | [How versions are named — e.g., `v1.2`, git commit hash, timestamp] |
| **Deployment process** | [How a new prompt version is deployed — code deploy / config update / tool push] |
| **Rollback process** | [How to revert to the previous version without a full redeploy — specify exact steps] |
| **Change log** | [Where prompt change history is recorded and who can review it] |

**Rollback trigger**: under what conditions should a prompt version be rolled back? (e.g., quality score drops more than X%, error rate exceeds Y%, user complaints spike)

---

## Step 7: Evaluation criteria

### Quality rubric
Define the scoring rubric used to evaluate model outputs. This is the ground truth for all evals.

| Criterion | Definition | Weight | Scoring scale |
|-----------|-----------|--------|---------------|
| [e.g., Accuracy] | Output correctly reflects source material | 40% | 1–5 |
| [e.g., Conciseness] | Output is within the specified length | 20% | 1–5 |
| [e.g., Tone] | Output matches the required register | 20% | 1–5 |
| [e.g., Completeness] | Output addresses the full user intent | 20% | 1–5 |

**Composite score formula**: [e.g., weighted average of criteria scores]
**Minimum passing score**: [X/5 composite] — outputs below this threshold trigger the fallback path

### Evaluation method
- [ ] Human eval — who reviews, how often, what's the review process?
- [ ] LLM-as-judge — which model, what prompt, what's the judge's rubric?
- [ ] Reference-based — what is the gold-standard reference and how is similarity measured?
- [ ] Hybrid — specify which method applies to which criteria

### Evaluation dataset
Describe the evaluation dataset:
- **Size**: [N] representative input/output pairs at launch; target [N] at steady state
- **Coverage**: [Which use cases, edge cases, and failure modes are represented]
- **Source**: [How were examples selected — real user inputs, synthetic, expert-curated?]
- **Update cadence**: [When and how the dataset is expanded]

### Production quality monitoring
| Signal | How measured | Alert threshold | Cadence |
|--------|-------------|-----------------|---------|
| Quality score | [LLM-as-judge / user feedback / human sample] | < [X] | Daily / Weekly |
| Error rate | AI call failures / total calls | > [X]% | Real-time |
| Latency | p95 AI call latency | > [X]ms | Real-time |
| Cost | Token spend / request | > $[X] | Daily |

---

## Step 8: Fallback behavior

| Failure mode | Trigger condition | Fallback behavior | User-facing message |
|-------------|------------------|-------------------|---------------------|
| API unavailable | HTTP 5xx or timeout | [Non-AI path / retry / queue] | [Exact copy] |
| Rate limit hit | HTTP 429 | [Queue / degrade / error] | [Exact copy] |
| Content filter | HTTP 400 / safety block | [Redirect / log / error] | [Exact copy] |
| Output below quality threshold | Score < [X] on judge | [Retry with temperature change / surface for human review / return generic response] | [Exact copy] |
| Token budget exceeded | Input > [X] tokens | [Truncate / summarize / error] | [Exact copy] |

---

## Step 9: Open questions

| Question | Impact on prompt design | Owner | Due |
|----------|------------------------|-------|-----|
| | | | |

---

## Save output

After presenting the prompt specification to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, save to the path listed for `/prompt-spec`; if no row exists, save to `dev/prompt-spec.md`
3. Update the **Status** field to **Done** and **Last updated** to today's date
4. Confirm the file was written to the user
5. If no project `CLAUDE.md` exists, present the output for manual copying
6. Prompt the user: *"Run `/dev-workflow-kit:log [one-line summary]` to record this in the work log — e.g. `/dev-workflow-kit:log Completed prompt spec for [feature name]`"*
