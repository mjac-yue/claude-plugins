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

6. **Present the recommendation** and ask:
   > "Does this stack work for you? Reply **'approve'** to scaffold the project, or share any changes before proceeding."

7. **Scaffold the code structure** — once the stack is approved:

   **Step 7a — Detect project context**

   Check if a `CLAUDE.md` exists in the current directory. If yes, this is an initialised project — scaffold code at the current directory root. If no, ask where to scaffold (default: current directory).

   **Step 7b — Run the framework scaffold command**

   Use the Bash tool to run the appropriate scaffold command for the approved stack. Use `--yes` or equivalent flags to avoid interactive prompts. Common commands:

   | Stack | Scaffold command |
   |-------|----------------|
   | Next.js (TypeScript) | `npx create-next-app@latest . --typescript --tailwind --eslint --app --src-dir --import-alias "@/*" --yes` |
   | Next.js (JavaScript) | `npx create-next-app@latest . --javascript --tailwind --eslint --app --src-dir --yes` |
   | Vite + React (TypeScript) | `npm create vite@latest . -- --template react-ts && npm install` |
   | Vite + React (JavaScript) | `npm create vite@latest . -- --template react && npm install` |
   | Express + Node | Create manually — see Step 7c |
   | FastAPI (Python) | Create manually — see Step 7c |
   | SvelteKit | `npx sv create . --template minimal --types ts --yes && npm install` |

   If the stack doesn't have a standard CLI scaffold, proceed to Step 7c manually.

   **Step 7c — Create standard additional directories**

   After the framework scaffold, use Bash to create any additional standard directories the project will need. Adapt to the framework — examples:

   For Next.js (`src/` layout):
   ```bash
   mkdir -p src/components src/lib src/hooks src/types src/styles
   ```

   For Express/Node:
   ```bash
   mkdir -p src/routes src/controllers src/middleware src/models src/lib src/types
   touch src/index.js src/routes/index.js
   ```

   For FastAPI (Python):
   ```bash
   mkdir -p app/routers app/models app/schemas app/services app/core
   touch app/main.py app/routers/__init__.py app/models/__init__.py
   ```

   **Step 7d — Create a `.gitignore`**

   If the scaffold didn't create one, use the Write tool to create a `.gitignore` appropriate for the stack. Always include:
   ```
   # Environment
   .env
   .env.local
   .env.*.local

   # Dependencies
   node_modules/

   # Build output
   .next/
   dist/
   build/
   out/

   # OS
   .DS_Store

   # IDE
   .vscode/
   .idea/
   ```

   **Step 7e — Update the project CLAUDE.md**

   If a `CLAUDE.md` exists in the current directory, append the following section to it using the Edit tool:

   ```markdown
   ## Code structure

   Application code lives at the project root alongside the doc folders.

   | What | Path |
   |------|------|
   | Application source | `src/` |
   | Components | `src/components/` |
   | Utilities / helpers | `src/lib/` |
   | Custom hooks | `src/hooks/` |
   | Type definitions | `src/types/` |
   | API routes | `src/app/api/` |
   | Configuration files | `/` (root) |

   *Adapt these paths if the framework uses a different convention.*

   ### Agent code paths

   When agents need to read or review code, look here:

   | Agent | Code paths |
   |-------|-----------|
   | `code-reviewer` | `src/` |
   | `security-reviewer` | `src/`, `src/app/api/` |
   | `arch-reviewer` | `src/`, root config files |
   | `solution-analyst` | `src/`, `package.json` (or equivalent) |
   | `test-case-generator` | `src/` |
   ```

   **Step 7f — Confirm and summarise**

   After scaffolding, output:

   ```
   ## Code scaffold complete

   Stack: [Framework + Language]

   📁 [project-name]/
   ├── CLAUDE.md           ← updated with code paths
   ├── pm/                 ← PM docs
   ├── design/             ← design docs
   ├── dev/                ← dev docs
   ├── src/                ← application code
   │   ├── app/            ← pages and API routes
   │   ├── components/     ← reusable UI components
   │   ├── lib/            ← utilities and helpers
   │   ├── hooks/          ← custom React hooks
   │   └── types/          ← TypeScript type definitions
   ├── package.json
   └── .gitignore

   **Next step**: Save the tech stack document to dev/tech-stack.md, then run `/arch-design` or `/tech-spec` to begin the technical design.
   ```
