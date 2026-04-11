---
name: tech-stack
description: Choose the right tech stack for your product — language, framework, database, auth, hosting, and key services. Prioritizes simplicity and maintainability for a PM-led, AI-assisted build. Use before design or development begins on any new product or major feature.
disable-model-invocation: true
---

Choose a tech stack for: $ARGUMENTS

Use the template in [tech-stack-template.md](tech-stack-template.md) as the structure.

Follow this process:

1. **Clarify what's being built** — ask if not clear:
   - Product type: web app, mobile app, API/backend only, browser extension, CLI tool, or hybrid?
   - Primary users: internal tool, consumer-facing, or developer-facing?
   - Expected scale at launch vs. 12 months out (rough order of magnitude is enough)
   - Any hard constraints: must use a specific language, existing codebase to extend, budget ceiling, compliance requirements?

2. **Establish the builder context** — assume the builder is a PM with some coding skills using AI assistance. Default to:
   - **Managed services over self-hosted** — less operational burden, easier to debug
   - **Monolith over microservices** — simpler to build, deploy, and reason about at early stage
   - **Convention over configuration** — opinionated frameworks reduce decision fatigue
   - **Proven libraries over custom** — don't build what you can install
   - **Hosted databases over self-managed** — avoid database ops complexity
   - Override these defaults only if there's a specific, stated reason

3. **Select each layer of the stack**. For each layer, recommend one primary option and note one alternative. Layers to cover:
   - **Frontend** (if applicable): framework, component library, styling approach
   - **Backend**: language, framework, API style (REST, GraphQL, tRPC, etc.)
   - **Database**: type (relational vs. document), specific service, ORM/query layer
   - **Authentication**: managed auth service vs. DIY — strongly prefer managed for a PM-builder
   - **File storage** (if applicable): where uploads and assets live
   - **Hosting & deployment**: where it runs and how it gets deployed
   - **Key third-party services**: payments, email, notifications, analytics — prefer best-in-class APIs over building

4. **Estimate monthly cost** at two tiers:
   - Launch (0–500 users): what it costs to start
   - Growth (500–5,000 users): when things start to cost real money

5. **Flag what to avoid** — specific technologies or patterns that would add complexity a PM-builder shouldn't take on without dedicated engineering support

6. **Suggest a starter setup** — the first 3 commands or steps to get a skeleton running locally

Ask clarifying questions if the product type or constraints are unclear. Do not recommend a stack without understanding what's being built.
