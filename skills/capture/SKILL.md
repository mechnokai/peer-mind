---
name: capture
description: "Persist durable knowledge to peer-mind memory. Load this skill when (a) the user reveals something about themselves that will still be true in six months, or (b) you discover something about how to work with this user that would change your default behavior next session: an approach that failed, a workflow that worked better than expected, a correction the user issued twice. Do not load for transient status, session notes, or task-specific context."
---

# capture

Persists two kinds of durable knowledge to the peer-mind memory directory:

1. **User knowledge** — things the user learned, decided, or revealed about themselves
2. **Agent lessons** — things you (the LLM) learned about how to work with this user

Both matter. The first keeps the user from re-explaining themselves. The second keeps you from repeating failed approaches.

## When this applies

### User knowledge

The user just told you something durable about themselves. Signals:

- Reflecting on the past and drawing a conclusion
- Explaining a decision with reasoning
- Observing their own behavior from outside ("I keep", "I always", "every time")
- Correcting your model of them ("no, I'm actually...", "that's not how I work")
- Naming a person who matters with context you did not have

### Agent lessons

You just discovered something about how to work with this user that would change your default behavior. Signals:

- You tried an approach and it failed or got pushback
- The user corrected the same behavior twice in one session
- You found a better workflow through trial and error
- The user explicitly told you to do something differently next time
- You wasted effort on something that should have been obvious

Ask yourself: would knowing this at the start of the session have changed what I did? If yes, capture it.

## Routing

| What it is | File |
|---|---|
| User lesson from experience | `lessons.md` |
| Agent lesson about workflow | `agent-lessons.md` |
| User decision with reasoning | `decisions.md` |
| User behavioral pattern | `patterns.md` |
| Stable fact about the user | `identity.md` |
| Relationship state change | `relationships.md` |
| Project status unlikely to change this week | `projects.md` |
| Time-bound current situation | `current-context.md` |

If two apply, pick the one more useful in six months. If none apply cleanly, default to `lessons.md`. Never ask the user to disambiguate.

## Agent lesson format

`agent-lessons.md` uses this structure:

```markdown
## <topic>

- **YYYY-MM-DD** — <trigger>: <what happened>
  - Wrong approach: <what you did>
  - Better approach: <what to do instead>
  - Why: <reason>
```

Group by topic (for example: `git-workflow`, `communication-style`, `code-review`). Create a new topic section if none exists. Append; do not rewrite existing entries.

If the same lesson appears twice across sessions (you made the same mistake again), flag it to the user: "I've made this mistake before. Promoting this to a standing rule."

## Steps

Run all steps without pausing. Do not narrate.

1. Memory directory: default `~/peer-mind/`. Honor user-configured overrides.
2. If git repo: `cd <memory-dir> && git fetch && git pull`. On conflict, `git merge --abort`, tell the user, stop.
3. Append to the routed file using its existing format:
   - `lessons.md`: `- YYYY-MM-DD — <lesson>`
   - `agent-lessons.md`: topic-grouped block as shown above
   - `decisions.md`: `### <Title>` block with Date / Decision / Reasoning / Status
   - `patterns.md`: under the most relevant section
   - others: match existing section structure
4. If git repo: `cd <memory-dir> && git add -A && git commit -m "capture: <short description>" && git push`
5. Confirm in one short sentence naming only the file. Example: "Saved to lessons.md." Do not read the entry back.

## Hard rules

- No confirmations before writing
- No editorializing, write their words (or for agent lessons, write what actually happened)
- No duplicate captures of the same fact in one session
- No session notes here (those go in `sessions/YYYY-MM-DD.md`)
- No commits if the pull failed
