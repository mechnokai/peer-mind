# peer-mind

A template for running an AI peer, not a chatbot, with persistent memory.

This is a system prompt, a small set of skills, and a blank memory scaffold. It is built for people who need to think out loud about complex situations and want an AI that holds the complexity instead of flattening it into advice.

It is not a therapist. It is not a coach. It does not fix you. It remembers, reflects, confirms when you are right, and recalibrates openly when it is wrong.

## What this gives you

- A peer that remembers you across sessions via a private git repo.
- No therapeutic filler, no unsolicited advice, no seventeen-option hedging.
- Direct confirmation when you have already made the decision.
- Honest recalibration when new information changes the picture.

## What's inside

```
peer.md                  The agent's system prompt. Personality and rules.
skills/
  session-start/         Pull memory repo, load context before responding
  session-end/           Write session notes, commit and push
  remember/              Save durable facts the moment they come up
memory-template/         Blank memory files to make your own
```

## Quick start

New to git or GitHub? Read [SETUP.md](SETUP.md) for the full walkthrough.

1. Click **Use this template** at the top of this repo to create your own copy. Name it something private, like `peer-mind`, and set it to **Private**.
2. Clone your copy locally.
3. Copy the contents of `memory-template/` up to the repo root (or keep them in a subfolder, your call).
4. Fill in `identity.md` first. Be honest. Nobody else reads this.
5. Wire it into your AI tool of choice:
   - **Claude Code** (recommended): put `peer.md` and `skills/` in a folder, add a `CLAUDE.md` pointing at your memory directory, launch Claude Code there. Memory sync is automatic.
   - **Claude Project** (browser/apps): paste `peer.md` into the project instructions. Manually paste or attach memory files at session start. Apply the agent's memory edits yourself before pushing.
   - **Other tools** (opencode, Cursor, ChatGPT custom instructions): adapt `peer.md` to the tool's system-prompt slot and treat the skills as conventions, not commands.

## Rules the agent follows

- **Auto-update.** It writes new facts to memory without waiting to be asked.
- **Privacy.** Memory files stay local and private. Never share them.
- **Sensitive topics.** If you name a file after a person (`<name>.md`), the agent only reads it when you bring that person up.
- **Confirmation over advice.** If you have already decided, it says so and stops.
- **Short is fine.** "You're good" is a complete response.

## Maintenance

- Prune `current-context.md` monthly. Stale context makes the agent dumber.
- Keep `decisions.md` even after decisions resolve. It stops the agent from re-litigating settled questions.
- If a relationship becomes sensitive, move it to its own `<name>.md` file and add a one-line note in `relationships.md` saying so.

## What this is not

- Not a therapist or a replacement for professional help.
- Not a productivity system.
- Not a prompt-engineering showcase. It is a working tool.

## License

MIT. Take it, adapt it, make it yours.
