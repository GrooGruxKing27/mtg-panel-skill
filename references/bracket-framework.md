# EDH Bracket Framework

The Commander Format Panel's bracket system (introduced Feb 11, 2025; in beta since). Five brackets that classify decks by power and intent rather than the old vague 1–10 power-level scale. This reference is the working tool for the **Table Captain** persona and is also used by the **Optimizer** and **Meta Analyst** when discussing power level.

The framework is *intent-first*: a deck that technically fits Bracket 2's deck-building rules but plays at Bracket 4 power should be self-classified at Bracket 4. The rules below are guardrails, not a checklist.

For the live, authoritative card list, search Scryfall with `is:game-changer`. The list is updated periodically (most recently Feb 9, 2026, with 53 cards). Don't try to maintain a hardcoded list in this skill — call Scryfall.

---

## The brackets

### Bracket 1 — Exhibition
**Intent:** Ultra-casual. Winning is not the point. Showcase decks: tribal jank, theme constraints (every card has the number 4, all art has horses, etc.), gimmicks.

**Rules:**
- No Game Changers
- No intentional two-card infinite combos
- No mass land denial / mass land destruction (MLD)
- No extra-turn cards
- Tutors should be sparse

**Game length expectation:** Long; ends slowly.

### Bracket 2 — Core
**Intent:** Modern precon level. The reference point is "an unmodified preconstructed deck." Where most newer or casual players land.

**Rules:**
- No Game Changers
- No intentional two-card infinite combos
- No MLD
- Extra-turn cards only in low quantities; not chained or looped
- Tutors should be sparse

**Game length expectation:** Roughly six turns or more before a winner is decided.

### Bracket 3 — Upgraded
**Intent:** Souped-up beyond a precon. Carefully curated card slots, intentional engines, faster than a precon by a turn or two.

**Rules:**
- Up to 3 Game Changers allowed
- No early-game two-card infinite combos (early = ~first six turns)
- No MLD
- Extra-turn cards only in low quantities
- Tutors should be sparse but allowed

**Game length expectation:** Six turns or so. A bit faster than Core.

### Bracket 4 — Optimized
**Intent:** "Bring your best deck, but not one tournament-tuned for a metagame." Explosive starts, strong tutors, cheap combos OK if not tier-zero, free disruption all on the table.

**Rules:**
- Unrestricted Game Changers
- No intentional early-game two-card infinite combos (still — this is what separates 4 from 5)
- Low quantities of extra-turn cards
- No MLD

**Game length expectation:** ~4 turns. Games can end fast.

### Bracket 5 — cEDH
**Intent:** Tournament metagame. Decks built using cEDH knowledge, tools, decklists. Everything legal under the Commander banlist is fair game.

**Rules:**
- All restrictions off (within the format banlist)
- Two-card infinite combos welcome
- MLD welcome
- Extra-turn loops welcome
- Whatever wins

**Game length expectation:** Variable — turn 2 wins possible, sometimes longer grinds when the table interacts heavily.

---

## Working with the framework

### How to estimate a deck's bracket

1. **Count Game Changers** (`is:game-changer` on Scryfall). Zero → eligible for B1/B2. 1–3 → B3 minimum. 4+ → B4 minimum.
2. **Check for two-card infinite combos.** If present and assemble-able cheaply (≤6 turns) → B5 territory; otherwise it's a B3+ tell at minimum.
3. **Check for MLD.** Any mass land denial (Armageddon, Jokulhaups, Ravages of War effects) → B5 only.
4. **Check tutor density.** "Sparse" is loose, but five-plus efficient tutors signals B3+ at minimum, B4 at typical density.
5. **Check the curve and ramp speed.** A turn-2 ramp suite into turn-4 game-ending threats says B4 regardless of what the deckbuilder calls it.
6. **Check extra-turn density.** 3+ extra turn cards or any loop intent → B4+.
7. **Read intent.** What is this deck *trying* to do? A deck of 99 efficient pieces and a finisher that wins on turn 5 is B4 even if the deck list "looks casual."

The Table Captain should always state both what the deck *technically* qualifies for (rule-wise) and what it *plays* at (functionally), and recommend the higher of the two.

### Common mis-bracketings

- **"It's a precon" ≠ Bracket 2 if it's been heavily upgraded.** Even modest upgrades push toward Bracket 3.
- **"It has no Game Changers, so it's Bracket 2."** A no-GC deck full of optimized synergy and a fast clock is Bracket 3 at minimum.
- **"It has Rhystic Study, so it's Bracket 5."** No — one Game Changer puts a deck at Bracket 3, not 5. Game Changers ≠ cEDH-only.
- **Tribal decks are not automatically low-bracket.** A tuned tribal deck with strong synergy and ramp can easily be B3 or B4.

### When a deck violates its target bracket

When recommending changes to bring a deck to a target bracket, the priority order is:
1. Remove illegal cards (Game Changers in B1/B2; MLD in B1–4; etc.).
2. Remove combos that violate the bracket's combo timing rules.
3. Reduce extra-turn count if too high.
4. Adjust speed (curve, ramp density) if the deck plays too fast for its target.

When recommending cards to *raise* a deck toward a higher bracket, the priority order is:
1. Add Game Changers strategically (within the deck's strategy, not just for power).
2. Tighten the curve and ramp.
3. Improve interaction density.
4. Add a faster, more reliable win condition.

---

## Notes on Game Changers

The Game Changers list is curated by the Commander Format Panel. Cards on the list are legal but bracket-restricted. The list updates roughly every 3–4 months. Notable changes:

- **Feb 2025:** Initial list (40 cards).
- **April 2025:** Significant expansion in response to community feedback that the list was too small.
- **Oct 2025:** Some cards removed (delisted) to refine the list's signal.
- **Feb 2026:** Farewell added (deemed too punishing for casual play); Biorhythm added after coming off the banlist.

Three categorical rules of thumb for what tends to be on the list:
1. **Snowballing resource engines** (Rhystic Study, Smothering Tithe, Mystic Remora at the high end).
2. **Free disruption** (Force of Will, Fierce Guardianship, Deflecting Swat).
3. **Efficient tutors** (Demonic Tutor, Vampiric Tutor, Imperial Seal).

Cards on the list typically warp games in ways that "feel bad" for opponents who didn't know they were in the deck — that's the framework's central intuition.

The formal banlist is separate from Game Changers. Cards like Dockside Extortionist, Mana Crypt, Jeweled Lotus, and Nadu (Winged Wisdom) were *banned* in September 2024, not added to Game Changers. When a card is unbanned, it commonly lands on the Game Changers list as a half-step (this happened with Biorhythm, Braids, Coalition Victory, Gifts Ungiven, and Panoptic Mirror).

Sol Ring is famously *not* on the Game Changers list despite being one of the most powerful cards in the format — WotC's reasoning is that Sol Ring is so ubiquitous (every precon has one) that restricting it would be impractical.
