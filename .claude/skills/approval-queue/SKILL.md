---
name: approval-queue
description: Convention for drafting an action into the approvals queue for Austin's sign-off before it becomes real - publishing, spending, launching, uploading, or acting on a trade idea. Use whenever an agent finishes work that crosses a hard constraint (money, external send/publish, new integration) rather than acting on it directly.
---

# Approval Queue

See `approvals/README.md` for the full convention. Summary for agents invoking this skill:

1. Confirm the action actually needs approval — routine/reversible/internal work (drafts sitting
   in an `inbox/`, research, backtests) does NOT need this; only external-facing, financial, or
   hard-to-reverse actions do.
2. Write `approvals/queue/YYYY-MM-DD-<business>-<short-slug>.md` with sections: **What**, **Why**,
   **Preview** (the actual content/numbers — not a paraphrase), **Risk/reversibility**.
3. Tell Austin in chat that something is waiting in the queue, in one sentence, and stop —
   don't take further action on it.
4. Never mark your own queue entry as approved. Only Austin's explicit reply in chat does that,
   and even then, follow the specific action category's rules (e.g. sending an email is still
   something Austin does himself from the Gmail draft, not something the agent triggers).
