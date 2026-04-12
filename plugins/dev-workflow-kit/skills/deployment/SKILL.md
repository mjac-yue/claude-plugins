---
name: deployment
description: Produce a deployment guide for a completed feature or product — covering platform setup, environment configuration, database provisioning, domain and DNS, first deploy steps, smoke testing, and rollback. Written for a PM-led, AI-assisted build. Use when the code is ready to ship and you need a step-by-step plan to get it live.
disable-model-invocation: true
---

Produce a deployment guide for: $ARGUMENTS

Use the template in [deployment-template.md](deployment-template.md) as the structure.

Follow this process:

1. **Clarify the deployment context** — ask if not provided:
   - What tech stack is being deployed? (language, framework, database)
   - Where is it being deployed? (if not yet decided, recommend a platform based on the stack)
   - Is this a first deploy (new product) or an update to something already live?
   - Is there an existing domain, or does one need to be set up?
   - Does it need CI/CD, or is a manual first deploy acceptable?

2. **Recommend a deployment platform** if not specified. Default priorities for a PM-led build:
   - **Web app (Next.js, Remix, SvelteKit)**: Vercel — simplest deploy path, git-connected, built-in preview environments
   - **Full-stack / backend API**: Railway or Render — managed hosting with database add-ons, simple config
   - **Python / FastAPI / Flask**: Render or Railway — both support Python natively with minimal config
   - **Mobile**: not covered here — flag and recommend platform-specific guides
   - Avoid recommending AWS/GCP/Azure raw infrastructure unless the user has DevOps support

3. **Build the pre-deployment checklist** — the steps that must be done before the first deploy:
   - Environment variables: list every env var the app needs and where to set them
   - Secrets: API keys, database connection strings, auth secrets — where they come from and how to store them safely
   - Database: provisioning steps, migration commands, seed data if needed
   - Third-party services: any API accounts that must be set up first (auth provider, email service, payment processor, etc.)

4. **Write the deploy steps** — numbered, specific, command-by-command where possible. Assume the reader knows basic terminal commands but not platform-specific CLIs.

5. **Build the smoke test checklist** — 5-10 specific things to verify immediately after deploy that confirm the product is working. Each item should be a concrete action with an expected outcome, not a vague category.

6. **Cover domain and DNS** if the product needs a custom domain:
   - Where to buy a domain (if needed)
   - DNS records to add (A record, CNAME, etc.)
   - SSL certificate (most platforms handle this automatically — note if any action is needed)
   - Expected propagation time

7. **Define the rollback plan** — what to do if the deploy breaks something. Keep it simple:
   - How to revert to the previous version on the chosen platform
   - Whether a database migration needs to be reversed (and if so, how)
   - Who to notify and when

8. **Set up basic monitoring** — minimum viable observability for a solo builder:
   - Error tracking (recommend a free tier tool)
   - Uptime monitoring (recommend a free tier tool)
   - Where to find logs on the chosen platform

Be specific about commands and platform UI steps. If the stack is not specified clearly enough to give concrete steps, ask before producing a generic guide.

## Save output

After presenting the deployment guide to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/deployment` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. Confirm the file was written to the user
5. If no project `CLAUDE.md` exists, present the output for manual copying
