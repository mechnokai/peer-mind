---
name: remember
description: "Save a new fact, decision, pattern, or lesson about the user into the peer-mind memory directory and commit it to git. Use when the user says 'remember this', 'save that', or reveals durable personal context."
---

# remember

Writes durable user context to the peer-mind memory directory.

## When to use

- User says "remember this", "save that", "add this to memory", "note that"
- User reveals a stable fact, a decision and its reasoning, a relationship detail, a behavioral pattern, or a hard-won lesson

## Steps

1. Identify which memory file the fact belongs in:
   - `identity.md` — stable facts (name, role, family, traits)
   - `current-context.md` — what is happening right now, time-bound
   - `relationships.md` — people who matter
   - `projects.md` — active projects
   - `patterns.md` — behavioral patterns
   - `decisions.md` — decisions and the reasoning behind them
   - `lessons.md` — hard-won lessons
2. Append or edit the relevant section. Keep the existing structure and tone.
3. If the memory directory is a git repo:
   ```
   cd <memory-dir> && git add -A && git commit -m "memory: <short description>" && git push
   ```
4. Confirm to the user in one short sentence. Do not recap the whole entry back at them.

## Do not

- Do not ask the user to confirm before writing. They said to remember, so remember.
- Do not write the same fact to multiple files.
- Do not commit if the git pull at session start failed; flag it instead.
