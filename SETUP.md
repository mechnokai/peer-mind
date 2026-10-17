# Detailed setup

This walks through setup from zero, including the GitHub parts. If you already know git, the main README is enough.

## Step 1: Get your own copy

1. Go to the template repo on GitHub.
2. Click the green **Use this template** button at the top, then **Create a new repository**.
3. Name it `peer-mind` (or anything you like).
4. Set it to **Private**. This is not optional. These files will contain personal information.
5. Click **Create repository**.

## Step 2: Clone it to your machine

Open a terminal.

```bash
cd ~
git clone https://github.com/<your-username>/peer-mind.git
cd peer-mind
```

Replace `<your-username>` with your GitHub username.

If this is your first time using git with GitHub, you will be prompted to authenticate. Follow the prompts.

## Step 3: Fill in your memory files

The template ships with blank files inside `memory-template/`. Move them up to the repo root and delete the now-empty template folder:

```bash
mv memory-template/* .
mv memory-template/sessions ./sessions
rm -rf memory-template
```

Now edit the files. Start with `identity.md`, then `current-context.md`, then `relationships.md`. The more honest you are, the better the agent works. Nobody else will read these. The repo is private.

Commit your baseline:

```bash
git add -A
git commit -m "initial: my peer-mind baseline"
git push
```

## Step 4: Wire it into Claude

Pick one.

### Option A: Claude Code (recommended, memory sync is automatic)

1. Install Claude Code: https://claude.com/claude-code
2. Sign in with your Claude account.
3. Make a folder for the agent somewhere, for example `~/peer-agent/`.
4. Put `peer.md` and the `skills/` folder in it.
5. Create a `CLAUDE.md` in the same folder with contents like:

   ```markdown
   # Peer agent

   System prompt: see peer.md in this folder. Follow it exactly.

   Memory directory: ~/peer-mind/

   At the start of every session, run the session-start skill.
   ```

6. Launch Claude Code in `~/peer-agent/`. The agent will pull your memory repo, read it, and commit changes as you talk.

### Option B: Claude Project (browser and apps, manual memory loop)

1. Go to https://claude.ai and log in.
2. Create a new Project. Name it "Peer".
3. In Project settings, paste the full contents of `peer.md` into the custom instructions field.
4. At the start of each session, paste the contents of `identity.md`, `current-context.md`, and `relationships.md` into the first message, or attach the files.
5. When the agent says it updated memory, apply those edits to your local files and push. Claude Projects cannot write to your filesystem, so you are the sync layer.

Option B works but the memory loop is manual. Option A is better once you are comfortable in a terminal.

## Step 5: Use it

Start a session. The agent reads your memory files first. Talk. When you tell it something new, it updates memory on its own. When you are done, say so and it writes a session note and pushes.

The agent gets better the longer you use it. Memory compounds.

## Maintenance

- Prune `current-context.md` monthly. Stale context makes the agent dumber.
- Keep `decisions.md` even after decisions resolve. It stops the agent from re-litigating settled questions.
- If a relationship becomes sensitive enough that you only want it discussed when you bring it up, move it to its own `<name>.md` file and add a one-line note in `relationships.md` saying so.
