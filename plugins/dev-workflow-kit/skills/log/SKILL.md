---
name: log
description: Append a work log entry to WORKLOG.md with your name, today's date, and a short summary of what was done. Use after completing meaningful work — a feature, review, decision, or design. Keeps a shared history any contributor can read to understand what happened and why. Usage: /log [short summary of what was done]
disable-model-invocation: true
allowed-tools: [Bash, Read, Write, Edit]
---

Log this work: $ARGUMENTS

Follow these steps exactly:

1. Run `git config user.name` to get the contributor's name. If unavailable, use "Unknown".
2. Get today's date in YYYY-MM-DD format.
3. Format the entry:

```
---

**[YYYY-MM-DD] · [Author Name]**
[Summary from $ARGUMENTS — preserve exactly as written, do not rephrase or expand]
```

4. Check if `WORKLOG.md` exists in the project root.
   - If it **does not exist**, create it with this header, then append the entry:
     ```
     # Work Log

     A running history of meaningful contributions. Add an entry with `/dev-workflow-kit:log [short summary]`.
     ```
   - If it **exists**, append the new entry at the bottom of the file.

5. Write the file.

6. Confirm to the user with: `Logged.` followed by the entry as written. Nothing else.
