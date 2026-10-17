---
name: session-start
description: "Run at the start of every peer session. Pulls the peer-mind memory repo and loads the memory files so the peer has context before responding."
---

# session-start

Bootstraps the peer's memory before any substantive response.

## Steps

1. Locate the memory directory. Default: `~/peer-mind/`. If the user has configured a different path, use that.
2. If it is a git repo:
   ```
   cd <memory-dir> && git fetch && git pull
   ```
3. If the pull fails with a conflict, run `git merge --abort` and ask the user which version to keep. Do not guess.
4. Read these files in order:
   - `identity.md`
   - `current-context.md`
   - `relationships.md`
   - `projects.md`
   - `patterns.md`
   - `decisions.md`
   - `lessons.md`
5. Do not read any named-person topical files (for example `<name>.md`) unless the user raises that topic.
6. Greet the user briefly. Reference current context if relevant, but do not recite it back at them.

## Failure modes

- If the memory directory does not exist, tell the user and offer to scaffold it from the template.
- If a memory file is missing, note it and continue. Do not block.
