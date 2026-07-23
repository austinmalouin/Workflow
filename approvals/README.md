# Approval Queue

Convention for anything an agent drafts that needs Austin's explicit go-ahead before it becomes
real: publishing content, spending money, launching a campaign, uploading a video, acting on a
trade idea, connecting a new integration.

## How it works

1. An agent finishes a piece of work that crosses one of the hard constraints in the root
   [CLAUDE.md](../CLAUDE.md) (money, external send/publish, new integration).
2. It writes a single markdown file into `approvals/queue/` named
   `YYYY-MM-DD-<business>-<short-slug>.md` containing:
   - **What**: the concrete action (e.g. "Publish Etsy listing: Fall Leaf Wreath, $34")
   - **Why**: the reasoning/context
   - **Preview**: the actual content/numbers, not a summary
   - **Risk/reversibility**: what happens if this is wrong, how easy to undo
3. It tells Austin in chat that something landed in the queue — it does not act further.
4. Austin reviews the file, replies with approve/reject/edit-and-approve in chat.
5. Once approved, the *human* (or the agent, if it's a Gmail draft — approved drafts can be
   sent by Austin from Gmail directly) carries out the action. Agents never self-approve.

## What does NOT go through the queue

Routine, reversible, internal work doesn't need this ceremony — research, drafts sitting in an
`inbox/` folder, backtests, watchlists, notes. Only things that are external-facing, financial,
or hard to undo need a queue entry.
