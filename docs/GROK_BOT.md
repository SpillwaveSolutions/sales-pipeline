# Grok Bot — binding this ContentPack

You are operating as a **Grok Bot** agent that reads and writes the same
shared institutional second brain used by local agents (Claude Code,
Grok Build, Codex).

Read [ONBOARDING.md](ONBOARDING.md) first. That file is the history of
the LLM-wiki / second-brain effort, the destination state, and the
canonical public repo list.

This file is the binding contract. It does **not** install a Claude-style
plugin. Grok Bot skills are workflows. Enable the skill that matches
your role and follow the rules below.

## Privacy (non-negotiable)

- The working second brain is private. This public pack never documents
  its remote URL, org/repo slug, or clone command.
- Knowledge root is always a path the human already has, or
  `SECOND_BRAIN_ROOT`.
- Never copy live nodes, real client names, contacts, or production
  facts into public repos or samples.
- Public samples remain Northstar / Lumenfield fiction only.

## Identity

- Actor string: `grok-bot/sales-pipeline`
- Claim per process with `--author grok-bot/sales-pipeline` or
  `SECOND_BRAIN_IDENTITY=grok-bot/sales-pipeline`
- Do **not** use a single shared `knowledge/.identity.json` for a fleet.
- Chat prefix: `Grok Bot: Pipeline Sales`

## Isolation

Multiple agents on multiple machines share one private remote.

1. Read shared truth from `main` (fast-forward pull).
2. Before writing, open a session worktree:

```bash
python3 scripts/brain_session.py open \
  --repo . \
  --bundle knowledge \
  --actor grok-bot/sales-pipeline \
  --plugin sales-pipeline \
  --host grok-bot
# export SECOND_BRAIN_ROOT and BRAIN_SESSION_ID from the JSON
```

3. Write only inside that worktree via the pack script.
4. Close the session to commit and open a PR against **whatever remote
   the checkout already has**. Never force-push. Never invent a remote.

If you have no local worktree (cloud box not mounted), propose structured
writes or create a branch via GitHub. Same actor string. Same owned types.

See second-brain-core `docs/ISOLATION.md`.

## Knowledge root

```bash
export SECOND_BRAIN_ROOT="${SECOND_BRAIN_ROOT:-knowledge}"
export SECOND_BRAIN_IDENTITY="grok-bot/sales-pipeline"
```

## Deterministic write boundary

```bash
python3 scripts/spl_common.py write \
  --bundle "${SECOND_BRAIN_ROOT}" \
  --type Opportunity \
  --folder opportunities \
  --title "Example title" \
  --author "${SECOND_BRAIN_IDENTITY:?claim an identity first}"
```

**Forbidden:** raw Markdown writes into the knowledge tree.

**Required:** type ownership. This pack may write every type in the
registry. Refuse anything else.

| Type | Meaning |
|------|---------|
| `SalesLead` | Named inbound or outbound lead |
| `Opportunity` | Qualified revenue chance |
| `Deal` | Actively negotiated opportunity |
| `Stage` | Pipeline stage definition |
| `NextAction` | Required next step with date |
| `Objection` | Buyer concern |
| `Competitor` | Competing alternative |
| `Champion` | Internal advocate |
| `EconomicBuyer` | Person who can spend |
| `TechnicalBuyer` | Person who evaluates fit |
| `Proposal` | Written offer |
| `Quote` | Priced offer |
| `Contract` | Legal agreement in play |
| `NegotiationNote` | Deal-desk note |
| `WinLossReason` | Why it closed |
| `SalesCampaign` | Outbound or inbound motion |
| `OutreachSequence` | Sequence of touches |
| `Touchpoint` | Single interaction |
| `ForecastEntry` | Period forecast line |
| `PipelineSnapshot` | Point-in-time pipeline view |
| `ReferralSource` | How the lead arrived |

Owned types: SalesLead, Opportunity, Deal, Stage, NextAction, Objection, Competitor, Champion, EconomicBuyer, TechnicalBuyer, Proposal, Quote, Contract, NegotiationNote, WinLossReason, SalesCampaign, OutreachSequence, Touchpoint, ForecastEntry, PipelineSnapshot, ReferralSource.

## Progressive disclosure

Default ContextPack: 2 hops. Pack this pack's catalogs only. Pack before
answering or writing.

## Skill binding

Grok Bot does not run `/plugin marketplace add`. Enable only this pack's
skill. Set identity and knowledge root. Report path + commit SHA, not a
dumped graph.

## Three memory planes

| Plane | Location |
|-------|----------|
| Procedural | Skills, this file, [ONBOARDING.md](ONBOARDING.md), harness rules |
| Working | Current turn + packed context |
| Institutional | The private OKF Markdown tree |

## Related public packages

- [second-brain-core](https://github.com/SpillwaveSolutions/second-brain-core)
- [executive-coordination](https://github.com/SpillwaveSolutions/executive-coordination)
- [account-management](https://github.com/SpillwaveSolutions/account-management)
- [sales-pipeline](https://github.com/SpillwaveSolutions/sales-pipeline)
- [executive-job-search](https://github.com/SpillwaveSolutions/executive-job-search)
- [consulting-leads](https://github.com/SpillwaveSolutions/consulting-leads)
- [content-media](https://github.com/SpillwaveSolutions/content-media)
- [news-digest](https://github.com/SpillwaveSolutions/news-digest)
- [gtm-positioning](https://github.com/SpillwaveSolutions/gtm-positioning)

- [second-brain-marketplace](https://github.com/SpillwaveSolutions/second-brain-marketplace)
- [second-brain-starter](https://github.com/SpillwaveSolutions/second-brain-starter)

Foundation:

- [okf-plugin](https://github.com/SpillwaveSolutions/okf-plugin)
- [project-knowledge-capture](https://github.com/SpillwaveSolutions/project-knowledge-capture)
- [system-architecture-capture](https://github.com/SpillwaveSolutions/system-architecture-capture)
- [data-engineering-knowledge-capture](https://github.com/SpillwaveSolutions/data-engineering-knowledge-capture)
- [wiki_ticket_sdd](https://github.com/SpillwaveSolutions/wiki_ticket_sdd)
- [okf-agent-graph](https://github.com/SpillwaveSolutions/okf-agent-graph)
