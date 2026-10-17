---
name: capture
description: "Automatically save a lesson, decision, or pattern the user just surfaced. Detects the type, routes to the right memory file, commits, and pushes without asking. Use when the user says 'I learned', 'lesson learned', 'I decided', 'that's a pattern', 'note this', 'capture that', or any phrasing that signals durable self-knowledge, whether or not they are in a peer session."
---

# capture

Records durable self-knowledge the moment it surfaces. Detects what kind of thing the user said, writes it to the right file, syncs to git. No prompts, no confirmations, no routing questions.

Works standalone (after a hard debug session, a tough conversation, a project retrospective) and inside a peer session.

## When to fire

Fire automatically on phrasing like:

- "I learned that X"
- "Lesson learned: Y"
- "I decided to Z because..."
- "I noticed a pattern: when I..."
- "Note this", "capture that", "save that"
- "Add this to my memory"
- "I keep doing X when Y" (pattern)
- "I'm going to start / stop doing X" (decision)
- "Turns out X" (lesson)

Do not fire on transient context. If it will be stale next week, it belongs in `current-context.md`, not here.

## Auto-routing

Classify by the shape of what the user said, not by asking them. Use the first rule that matches:

| Signal in their phrasing | Where it goes |
|---|---|
| "I learned", "lesson", "turns out", "I didn't realize", "never again", "from now on" (reflective) | `lessons.md` |
| "I decided", "I'm going to", "I'm not going to", "the plan is", "the call is", "I chose" | `decisions.md` |
| "I keep", "I always", "I tend to", "I noticed I", "when I'm X I do Y", "every time" | `patterns.md` |
| Stable fact about them (role, family, wiring) | `identity.md` |
| Person they care about, relationship state change | `relationships.md` |
| Project status, blocker, next step | `projects.md` |
| Time-bound, current situation | `current-context.md` |

If two categories genuinely apply, pick the one that will be more useful in six months. Do not write the same entry to two files. If none of the rules match cleanly, default to `lessons.md` with a plain one-liner rather than asking the user to disambiguate.

## Steps

Run these in order. Do not pause for confirmation between them.

1. Locate the memory directory. Default: `~/peer-mind/`. If the user has configured a different path, use that.
2. If it is a git repo, pull first:
   ```
   cd <memory-dir> && git fetch && git pull
   ```
   If the pull fails with a conflict, abort the merge, tell the user, and stop. Do not guess which side to keep.
3. Append to the routed file. Match the format already in use:
   - `lessons.md`: `- YYYY-MM-DD — <lesson, one or two lines, plain>`
   - `decisions.md`: `### <Decision>` block with Date, Decision, Reasoning, Status fields
   - `patterns.md`: append under the most relevant section (Strengths, Traps, Tells, What works)
   - `identity.md`, `relationships.md`, `projects.md`, `current-context.md`: match existing section structure
4. If it is a git repo, commit and push:
   ```
   cd <memory-dir> && git add -A && git commit -m "capture: <short description>" && git push
   ```
5. Confirm in one short sentence. Name the file, not the whole entry. Example: "Saved to lessons.md." Do not read the entry back.

## Examples

User: "Lesson learned: never run a migration on a Friday."
→ Append to `lessons.md`: `- 2026-10-17 — Never run a migration on a Friday.`

User: "I decided to take the new role because the pay bump and scope beat staying."
→ Append to `decisions.md` as a `### Take the new role` block with date, decision, reasoning, status: active.

User: "I've noticed I avoid hard conversations until I'm forced into them."
→ Append to `patterns.md` under `## Traps`.

User: "I keep rewriting the same function three times before I'm happy with it."
→ Append to `patterns.md` under `## Tells` or `## Traps`, whichever fits the existing tone.

User: "My sister just had her baby."
→ Append to `relationships.md` under the sister's entry, or add one if she is not there yet.

## Do not

- Do not ask which file it belongs in. Route it yourself.
- Do not ask the user to confirm before writing. They surfaced it; capture it.
- Do not editorialize or expand. Write what they said, in their words where possible.
- Do not commit if the pull at step 2 failed. Flag it and stop.
- Do not use this for session notes. Those belong in `sessions/YYYY-MM-DD.md`.
- Do not fire on the same fact twice in one session.
