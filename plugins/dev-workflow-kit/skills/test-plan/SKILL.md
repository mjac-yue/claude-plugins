---
name: test-plan
description: Create a QA test plan covering test types, key test cases, coverage targets, and acceptance criteria. Use before development begins or during QA handoff to define what "done" looks like.
disable-model-invocation: true
---

Create a QA test plan for: $ARGUMENTS

> **Learning note — QA Test Plan**
> A test plan defines what "working" means before the feature ships. It documents the happy path, edge cases, error states, and acceptance criteria so that QA, engineering, and PM have an objective standard to test against. Features shipped without a test plan tend to have well-tested obvious paths and untested edge cases that become post-launch bugs. Writing the test plan before development also surfaces ambiguities in the requirements — if you can't write a test for something, the requirement isn't specific enough yet.

Display the learning note above verbatim to the user before proceeding.

**Output standard — tables**: All documents are read in Obsidian. Always include a blank line before any Markdown table — Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [test-plan-template.md](test-plan-template.md) as the structure.

Follow this process:
1. **Scope and objectives** — what is being tested? What is explicitly out of scope? What quality risks are we most concerned about?
2. **Test types and coverage targets**:
   - **Unit tests**: which modules/functions need unit coverage? Target coverage %?
   - **Integration tests**: which service boundaries or data flows need integration coverage?
   - **End-to-end tests**: which critical user journeys must have e2e coverage?
   - **Manual / exploratory**: which areas require human judgment (edge cases, visual correctness, UX feel)?
   - **Performance tests**: any latency, load, or throughput requirements to verify?
   - **Security tests**: any auth, input validation, or data exposure vectors to test?
   - **AI evaluation tests** (if AI/ML components are in scope — skip if not):
     > **Learning note — Testing AI Components**
     > Traditional tests assume deterministic outputs — the same input always produces the same output, and you verify it exactly. AI components break this assumption: the same prompt can produce different completions. Testing AI requires a different approach: an evaluation dataset (representative input/expected output pairs) and a scoring mechanism (human judgment, LLM-as-judge, or reference-based metrics). Without an eval dataset established before launch, you have no baseline to detect quality degradation in production.
     >
     > Display this learning note verbatim before AI evaluation test planning.
     - **Evaluation dataset**: define a representative set of 20–50 input/expected output pairs covering the core use cases, edge cases, and known failure modes. This is your regression test suite for AI quality.
     - **Scoring mechanism**: how will outputs be judged — human eval rubric (1–5 scale with defined criteria), LLM-as-judge (another model scores the output against the rubric), or reference-based (output compared to a gold-standard answer)?
     - **Quality threshold**: what minimum score constitutes a passing eval? Define this before running evals, not after seeing the results.
     - **Adversarial prompt testing**: test inputs designed to trigger failure modes — prompt injection attempts, boundary-pushing content, empty inputs, extremely long inputs, inputs in unexpected languages.
     - **Latency benchmarking**: measure p50/p95 AI call latency under representative load. Establish the acceptable ceiling and confirm the implementation is within it.
     - **Cost benchmarking**: measure token consumption per representative request. Confirm the cost-per-request is within the target established in the PRD.
     - **Fallback path testing**: deliberately trigger AI API failures (mock the API returning 500, timeout, rate limit) and confirm the fallback behaves as designed.
     - **Content filter testing**: test inputs that should trigger the content policy and confirm the fallback message and UX behave correctly.
3. **Key test cases**. For each test case:
   - Test case name
   - Preconditions / test data setup
   - Steps to execute
   - Expected result
   - Pass/fail criteria
   - Test type (unit / integration / e2e / manual)
   
   Cover: happy path, edge cases, error states, boundary conditions, and concurrent/race scenarios.
4. **Test environment requirements** — what environments, data fixtures, mocks, or feature flags are needed?
5. **Acceptance criteria** — the specific, verifiable conditions that define QA sign-off. These should map directly to the PRD requirements.
6. **Regression considerations** — what existing functionality could this change break? Which regression tests must be re-run?
7. **Sign-off process** — who approves QA completion? What is the escalation path for blocking bugs?

Output a test plan engineering and QA can execute without additional clarification.

## Save output

After presenting the QA test plan to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/test-plan` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no project `CLAUDE.md` exists, present the output for manual copying
