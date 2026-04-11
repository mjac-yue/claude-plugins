# Deployment Guide: [Product / Feature Name]

**Date**: [Date]
**Stack**: [Framework + Language + Database]
**Deployment target**: [Platform name]
**Deploy type**: First deploy / Update to existing

---

## Pre-Deployment Checklist

Complete all items before running the deploy command.

### Accounts & Services

- [ ] [Hosting platform] account created and project initialized
- [ ] [Database service] instance provisioned
- [ ] [Auth service] configured (application created, redirect URIs set)
- [ ] [Email service] account set up, sending domain verified
- [ ] [Other third-party service] — [what needs to be done]

### Environment Variables

Set the following environment variables in your hosting platform's dashboard:

| Variable | Where to get it | Example / Notes |
|----------|----------------|-----------------|
| `DATABASE_URL` | [Database service] dashboard → Connection string | `postgresql://user:pass@host/db` |
| `SECRET_KEY` | Generate with: `openssl rand -hex 32` | Keep secret — never commit to git |
| `[AUTH_PROVIDER]_CLIENT_ID` | [Auth service] dashboard | |
| `[AUTH_PROVIDER]_CLIENT_SECRET` | [Auth service] dashboard | |
| `[EMAIL_SERVICE]_API_KEY` | [Email service] dashboard | |
| `NEXT_PUBLIC_APP_URL` | Your domain (or platform URL before custom domain) | `https://your-app.vercel.app` |

**Never put secrets in your code or commit them to git.** Use your platform's environment variable UI or a `.env` file that is listed in `.gitignore`.

### Database Setup

```bash
# 1. Run migrations to create tables
[migration command — e.g., npx prisma migrate deploy]

# 2. Seed initial data (if required)
[seed command — e.g., npx prisma db seed]

# 3. Verify connection
[verification command or manual check]
```

---

## Deploy Steps

### First-Time Setup

```bash
# Step 1: [Description]
[command]

# Step 2: [Description]
[command]

# Step 3: [Description]
[command]
```

### Connecting to Git (for continuous deployment)

1. [Platform] → [Navigation path] → Connect Repository
2. Select [repository name]
3. Set root directory to: `[path if monorepo, otherwise leave default]`
4. Set build command to: `[build command]`
5. Set output directory to: `[output dir]`
6. Add all environment variables from the table above
7. Click Deploy

**After this setup, every push to `main` will trigger an automatic deploy.**

---

## Domain & DNS

*Skip this section if using the platform's default URL.*

### Buy a Domain (if needed)
Recommended registrars: Namecheap, Google Domains, Cloudflare Registrar

### DNS Records to Add

Add these records at your domain registrar or DNS provider:

| Type | Name | Value | TTL |
|------|------|-------|-----|
| A | @ | [IP address from platform] | 3600 |
| CNAME | www | [platform URL] | 3600 |

**SSL certificate**: [Platform] handles this automatically once DNS propagates. No action needed.

**Propagation time**: 15 minutes to 48 hours. Check status at: [tool, e.g., whatsmydns.net]

---

## Smoke Test Checklist

Run these immediately after deploy to confirm the product is working. Each test is pass/fail.

- [ ] **Home page loads**: Navigate to `[URL]` — page loads without error, no console errors
- [ ] **Sign up works**: Create a new account with a test email — confirmation email received, can log in
- [ ] **Core user flow**: [Describe the primary action] — completes successfully, data saved correctly
- [ ] **Database reads**: [Navigate to a page that shows data] — data displays correctly
- [ ] **Database writes**: [Perform an action that saves data] — data persists after page refresh
- [ ] **Auth protected routes**: Navigate to `[protected URL]` without being logged in — redirected to login
- [ ] **Error handling**: Navigate to `[invalid URL]` — 404 page shown (not a stack trace)
- [ ] **Environment variables**: Check that [key feature that depends on env var] works correctly
- [ ] **[Third-party service]**: [Action that triggers the integration] — works as expected
- [ ] **Mobile/responsive**: Load on a mobile device or browser dev tools — layout renders correctly

**If any item fails**: Do not announce the launch. See Rollback section.

---

## Monitoring Setup

Set up these two things before announcing the launch:

### Error Tracking
**Recommended**: [Sentry](https://sentry.io) — free tier covers solo projects

```bash
# Install
[install command]

# Add to your app
[integration snippet or config step]
```

### Uptime Monitoring
**Recommended**: [Better Uptime](https://betterstack.com) or [UptimeRobot](https://uptimerobot.com) — free tier available

1. Create account → Add new monitor
2. Monitor type: HTTP(S)
3. URL: `[your app URL]`
4. Check interval: 5 minutes
5. Alert: email to `[your email]`

### Viewing Logs
On [platform]: [Navigation path to logs — e.g., Project → Functions → Logs]

---

## Rollback Plan

### If the deploy breaks something immediately:

**On [platform]**: Go to Deployments → Previous deployment → Redeploy

This takes approximately [X] minutes and returns to the last known working version.

### If a database migration needs to be reversed:

```bash
# Roll back the last migration
[rollback command — e.g., npx prisma migrate reset --skip-seed]
```

**Warning**: Rolling back a migration that dropped columns or tables may result in data loss. Only do this if the deploy has not yet had real user data written to the new schema.

### When to rollback vs. hotfix:
- **Rollback**: the site is down or a core flow is broken
- **Hotfix**: the issue is minor and a fix can be deployed quickly without data risk

---

## Post-Deploy Notes

- [ ] Update `[status page / internal doc]` with new deploy version
- [ ] Fill in any `[screenshot placeholder]` in user-facing documentation
- [ ] Notify `[team / users]` that the feature is live
- [ ] Set a reminder to check error tracking and uptime monitor in 24 hours
