---
name: capture
description: "Persist durable self-knowledge to peer-mind memory. Load this skill when the user reveals something about themselves that will still be true in six months: a hard-won lesson, a decision with reasoning, a recurring behavioral pattern, a stable fact about their identity or relationships. Do not load for transient status, session notes, or task-specific context."
---

# capture

Persists durable self-knowledge to the peer-mind memory directory and syncs to git. Silent, immediate, no confirmations.

## When this applies

The user just told you something about themselves that is durable. Not what they are doing, but what they learned, decided, or keep doing. Not a status update. Not a task. Something that, if you forget it, they will have to explain again next session.

Signals:

- They are reflecting on something that already happened and drawing a conclusion from it
- They have made a decision and are explaining why
- They are describing their own behavior as if observing it from outside ("I keep", "I always", "every time")
- They are correcting your model of them ("no, I'm actually...", "that's not how I work")
- They are naming a person who matters and giving you context you did not have

If you are unsure whether it is durable, ask yourself: will this still matter in six months? If yes, capture it. If no, it belongs in `current-context.md` or nowhere.

## Routing

Pick the file by what kind of durable thing it is:

| What it is | File |
|---|---|
| A lesson drawn from experience | `lessons.md` |
| A decision, with reasoning | `decisions.md` |
| A behavioral pattern they noticed or you both named | `patterns.md` |
| A stable fact about who they are | `identity.md` |
| A relationship state change, or a person who matters | `relationships.md` |
| A project status, blocker, or next step that is unlikely to change this week | `projects.md` |
| Time-bound current situation | `current-context.md` |

If two apply, pick the one more useful in six months. If none apply cleanly, `lessons.md` with a plain one-liner. Never ask the user to disambiguate.

## Steps

Run all steps without pausing. Do not narrate what you are doing.

1. Memory directory: default `~/peer-mind/`. Honor user-configured overrides.
2. If git repo: `cd <memory-dir> && git fetch && git pull`. On conflict, `git merge --abort`, tell the user, stop.
3. Append to the routed file using its existing format:
   - `lessons.md`: `- YYYY-MM-DD — <lesson>`
   - `decisions.md`: `### <Title>` block with Date / Decision / Reasoning / Status
   - `patterns.md`: under the most relevant section
   - others: match existing section structure
4. If git repo: `cd <memory-dir> && git add -A && git commit -m "capture: <short description>" && git push`
5. Confirm in one short sentence naming only the file. Example: "Saved to lessons.md." Do not read the entry back.

## Hard rules

- No confirmations before writing
- No editorializing, write their words
- No duplicate captures of the same fact in one session
- No session notes here (those go in `sessions/YYYY-MM-DD.md`)
- No commits if the pull failed
