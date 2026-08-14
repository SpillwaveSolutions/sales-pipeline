# Sales Pipeline

Sales pipeline ContentPack: leads, opportunities, stages, next actions, objections, proposals, and forecast entries.

MIT. Dual-host: **Claude Code**, **Grok Build**, and **Codex** (Agent Skill Standard). Writes OKF Markdown + YAML into a shared second-brain bundle so other agents and local jobs can read the same graph.

## Install

```bash
# Claude Code
/plugin marketplace add SpillwaveSolutions/sales-pipeline
/plugin install sales-pipeline@SpillwaveSolutions

# Skilz CLI
skilz install SpillwaveSolutions/sales-pipeline
```

Point the plugin at a shared knowledge root (default `knowledge/`). All sibling ContentPack plugins write into the same tree.

## Skills

| Skill | What it does |
|-------|----------------|
| `/spl-init` | Scaffold the catalogs this plugin owns |
| `/spl-capture` | Capture a noun into the shared second brain (deterministic write) |
| `/spl-pack` | Build a bounded ContextPack from a root concept |
| `/spl-validate` | Validate frontmatter, types, and links |
| `/spl-doctor` | Health check of the bundle this plugin owns |

## Nouns this plugin may write

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

## Relationships

| `rel` | Meaning |
|-------|---------|
| `belongs_to` | Lead belongs to client or campaign |
| `owned_by` | Pipeline owner identity |
| `originates_from` | Came from campaign or referral |
| `advances_to` | Moved to a stage |
| `blocked_by` | Stuck on objection or missing buyer |
| `competes_with` | Against a competitor |
| `proposed_as` | Has a proposal or quote |
| `related_to` | Soft association |
| `closed_as` | Won or lost with reason |

## Catalogs

- `sales-leads/`
- `opportunities/`
- `deals/`
- `proposals/`
- `quotes/`
- `campaigns/`
- `touchpoints/`
- `objections/`
- `forecasts/`

## Deterministic write boundary

The model proposes. Schema-enforced scripts commit:

```bash
python3 scripts/spl_common.py write \
  --bundle knowledge \
  --type SalesLead \
  --folder sales-leads \
  --title "Example" \
  --author "Grok Bot: Sales Pipeline"
```

Never invent `rel` values. Never write types owned by another plugin.



## Related plugins

- [second-brain-core](https://github.com/SpillwaveSolutions/second-brain-core) — shared pack engine and typed-edge conventions
- [project-knowledge-capture](https://github.com/SpillwaveSolutions/project-knowledge-capture) — the “why” second brain
- [system-architecture-capture](https://github.com/SpillwaveSolutions/system-architecture-capture) — the “what is running” second brain
- [wiki_ticket_sdd](https://github.com/SpillwaveSolutions/wiki_ticket_sdd) — visible work log

## License

MIT. Copyright 2026 Rick Hightower / contributors.
