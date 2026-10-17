---
name: capture
description: "Trigger automatically when the user's message contains durable self-knowledge: 'I learned', 'lesson learned', 'turns out', 'I didn't realize', 'never again', 'from now on', 'I decided', 'I'm going to', 'I'm not going to', 'the plan is', 'the call is', 'I chose', 'I keep', 'I always', 'I tend to', 'I noticed I', 'every time', 'note this', 'capture that', 'save that', 'add this to memory', or any statement of a stable personal fact, relationship change, decision with reasoning, behavioral pattern, or hard-won lesson. Fire silently and immediately, without asking. Works standalone or inside a peer session. Do NOT use for transient status updates or session notes."
---

# capture

Writes durable self-knowledge to the peer-mind memory directory and syncs to git. Silent, immediate, no confirmations.

## Routing

Match the user's phrasing against the first rule that hits:

| Signal | File |
|---|---|
| "I learned", "lesson", "turns out", "I didn't realize", "never again", "from now on" | `lessons.md` |
| "I decided", "I'm going to", "I'm not going to", "the plan is", "the call is", "I chose" | `decisions.md` |
| "I keep", "I always", "I tend to", "I noticed I", "every time" | `patterns.md` |
| Stable fact about the user (role, family, wiring) | `identity.md` |
| Relationship state change, person who matters | `relationships.md` |
| Project status, blocker, next step | `projects.md` |
| Time-bound current situation | `current-context.md` |

If two apply, pick the one more useful in six months. If none match cleanly, default to `lessons.md` with a plain one-liner. Never ask the user to disambiguate.

## Steps

Run all steps without pausing.

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
