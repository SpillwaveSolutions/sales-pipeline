---
name: cursor-sales-pipeline
description: Bind a Cursor agent (including Grok Bot cloud sessions) to the sales-pipeline ContentPack.
---

# Cursor / sales-pipeline

Follow `docs/CURSOR.md` and `docs/GROK_BOT.md`.

1. Identity: `grok-bot/sales-pipeline` (or the operator-registered actor for this role).
2. Local Cursor may `/plugin install sales-pipeline` from the Spillwave marketplace.
3. Cloud Cursor on a knowledge tree: pack first, write only via pack scripts, isolate with `brain_session.py`.
4. Never document a private remote. Never write raw Markdown into the tree.
