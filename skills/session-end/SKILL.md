---
name: session-end
description: "Run when the user signals they are done ('that's it', 'thanks', 'gotta go', end of conversation). Writes session notes, commits and pushes any uncommitted memory updates."
---

# session-end

Closes out a peer session cleanly.

## Steps

1. Write or append session notes to `<memory-dir>/sessions/YYYY-MM-DD.md`:
   - What the user brought up
   - What was resolved, confirmed, or left open
   - Any new facts worth keeping (these should already be in memory files, this is a recap)
2. If the memory directory is a git repo:
   ```
   cd <memory-dir> && git add -A && git commit -m "session: YYYY-MM-DD" && git push
   ```
3. Confirm the push succeeded. If it failed, tell the user and give them the command to retry.
4. Close briefly. Do not summarize the whole session back at them.

## Do not

- Do not offer unsolicited advice on the way out.
- Do not pad the goodbye. "You're good" or "Go be with your family" is enough.
