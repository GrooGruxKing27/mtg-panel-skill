# mtg-panel

A Claude Skill: a panel of Magic: The Gathering experts (personas) for serious deck and gameplay work. Use whenever you want to evaluate a card, set, deck, or play; build, update, or grade the power level of a Commander deck; identify combos in a card pool; resolve a rules or stack interaction; or get a structured second opinion on an MTG decision. Defaults to Commander/EDH but can advise on other formats.

The skill routes questions to the right specialist instead of summoning the whole panel for every prompt, then formats output in one of a few structured shapes (single-persona answer, multi-persona panel, full deck review).

> [!IMPORTANT]
> **This skill is non-functional without the [`mtg-commander`](https://github.com/GrooGruxKing27/mtg-commander-MCP) MCP server.** That server is what gives the personas their data — EDHREC recommendations/combos/themes/top cards, Scryfall card lookups and queries, MTG comprehensive rules and card rulings, Archidekt/Moxfield deck import and analysis, and TCGPlayer/Card Kingdom pricing. Install it first, then this skill.

## The Panel

- **The Optimizer** — efficiency, win rate, low CMC, fast clocks. cEDH and high-bracket lens.
- **The Brewer** — combos, jank, off-meta commanders, weird interactions.
- **The Theme Architect** — flavor, tribes, lore, archetype identity.
- **The Judge** — Comprehensive Rules, rulings, stack, layers, edge cases.
- **The Meta Analyst** — EDHREC inclusion percentages, popular cards, what's actually played.
- **The Table Captain** — bracket framework fit, social contract, pod dynamics.
- **The Mana Base Specialist** — lands, fixing, ramp curve, MDFCs, color requirements.

Full persona profiles live in [`references/personas.md`](references/personas.md). The EDHREC bracket framework reference is in [`references/bracket-framework.md`](references/bracket-framework.md), and a Scryfall-query cookbook in [`references/scryfall-queries.md`](references/scryfall-queries.md).

## Installation

### Step 1 — install the MCP server (required)

Follow the install instructions at [`GrooGruxKing27/mtg-commander-MCP`](https://github.com/GrooGruxKing27/mtg-commander-MCP) and make sure the `mtg-commander` MCP server is registered with your Claude client. Without it, the personas have no data to reach for and the skill won't work.

### Step 2 — install the skill

**Option A — download the release zip**

1. Grab `mtg-panel-v1.3.zip` from the [Releases page](../../releases/latest).
2. Unzip it into your Claude skills directory:
   - User-wide: `~/.claude/skills/`
   - Project-scoped: `.claude/skills/` inside the project root

   The zip unpacks to a `mtg-panel/` folder containing `SKILL.md` and `references/`.

**Option B — clone the repo**

```sh
git clone https://github.com/GrooGruxKing27/mtg-panel-skill ~/.claude/skills/mtg-panel
```

Either way, restart your Claude Code session so the skill is picked up.

## Versioning

Tagged releases mark stable versions of the skill. Release notes describe what changed; the in-repo `SKILL.md` always reflects the current `main`.

## License

MIT — see [`LICENSE`](LICENSE).
