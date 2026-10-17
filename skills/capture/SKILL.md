---
name: capture
description: "Save a lesson, decision, or pattern the user just named. Routes to lessons.md, decisions.md, or patterns.md in the peer-mind memory directory and commits to git. Use when the user says 'I learned', 'lesson learned', 'I decided', 'that's a pattern', 'note this', or 'capture that', whether or not they are in a peer session."
---

# capture

Records durable self-knowledge the moment it surfaces. Works standalone (after a hard debug session, a tough conversation, a project retrospective) and inside a peer session.

## When to use

- "I learned that X"
- "Lesson learned: Y"
- "I decided to Z because..."
- "I noticed a pattern: when I..."
- "Note this", "capture that", "save that"
- "Add this to my memory"

Do not use it for transient context. If it will be stale next week, it belongs in `current-context.md`, not here.

## Routing

Pick the file based on what the user is recording:

| What they said | Where it goes |
|---|---|
| Something they learned the hard way | `lessons.md` |
| A decision they made, with reasoning | `decisions.md` |
| A behavioral pattern they noticed or named | `patterns.md` |

If the thing spans two categories, pick the one that will be more useful later. Do not write the same entry to two files.

## Steps

1. Locate the memory directory. Default: `~/peer-mind/`. If the user has configured a different path, use that.
2. If it is a git repo, pull first:
   ```
   cd <memory-dir> && git fetch && git pull
   ```
   If the pull fails with a conflict, abort the merge and ask the user which version to keep. Do not guess.
3. Append to the correct file. Follow the format the file already uses:
   - `lessons.md`: `- YYYY-MM-DD — <lesson, one or two lines, plain>`
   - `decisions.md`: use the `### <Decision>` block format with Date, Decision, Reasoning, Status fields
   - `patterns.md`: append under the most relevant section (Strengths, Traps, Tells, What works)
4. If it is a git repo:
   ```
   cd <memory-dir> && git add -A && git commit -m "capture: <short description>" && git push
   ```
5. Confirm to the user in one short sentence. Do not recap the entry back at them.

## Examples

User: "Lesson learned: never run a migration on a Friday."
→ Append to `lessons.md`:
`- 2026-10-17 — Never run a migration on a Friday.`

User: "I decided to take the PPL role because the pay bump and scope beat the alternative."
→ Append to `decisions.md` as a `### Take the PPL role` block with date, decision, reasoning, status: active.

User: "I've noticed I avoid hard conversations until I'm forced into them."
→ Append to `patterns.md` under `## Traps`.

## Do not

- Do not ask the user to confirm before writing. They said to capture it, so capture it.
- Do not editorialize. Write what they said, in their words where possible.
- Do not commit if the pull at step 2 failed. Flag it instead.
- Do not use this for session notes. Those belong in `sessions/YYYY-MM-DD.md`.
