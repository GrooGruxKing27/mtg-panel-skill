# Scryfall Query Patterns

Scryfall's search syntax is the workhorse tool for combo hunting, archetype searches, and mana base construction. This reference is a working library of useful query patterns for the personas — especially the **Brewer** (combo hunting) and **Mana Base Specialist** (fixing). Pass these queries to `scryfall_search`.

Full Scryfall syntax reference: https://scryfall.com/docs/syntax

---

## Core syntax cheat sheet

| Operator | Meaning | Example |
|---|---|---|
| `c:` / `color:` | Card colors | `c:wu` (white and blue) |
| `ci:` / `id:` | Color identity (use this for Commander) | `ci:bant` |
| `t:` / `type:` | Type or subtype | `t:dragon`, `t:legendary t:creature` |
| `o:` / `oracle:` | Oracle text | `o:"draw a card"` |
| `cmc:` / `mv:` | Mana value (numeric) | `cmc<=3`, `mv=0` |
| `pow:` / `tou:` | Power / toughness | `pow>=4 tou>=4` |
| `r:` / `rarity:` | Rarity | `r:m` (mythic) |
| `is:` | Boolean tags | `is:commander`, `is:permanent`, `is:game-changer` |
| `usd<=` / `usd>=` | TCGPlayer USD price filter | `usd<=2` |
| `legal:commander` | Format legality | `legal:commander` |
| `f:` | Format shorthand | `f:edh` |
| `-` (minus) | Exclude | `-t:land` |
| `()` | Group / OR with `or` | `(t:elf or t:knight)` |

Color identity is the operator to use for Commander; `c:` checks just the casting cost colors.

---

## Combo hunting patterns

The Brewer's bread and butter. The trick is to identify the *function* a combo piece needs, then find every card that performs it.

### Untap-based combos
```
o:"untap" t:creature ci:[colors]
o:"untap target" t:permanent
o:"untap all" ci:[colors]
```

### Mana doublers / triplers
```
o:"add" o:"twice that much"
o:"adds an additional"
o:"that much mana" t:creature
```

### Damage / life-gain doublers
```
o:"would deal" o:"deals that much"
o:"would gain" o:"gains twice"
o:"if you would gain"
```

### Ways to copy a spell or trigger
```
o:"copy target spell"
o:"copy target instant or sorcery"
o:"create a token that's a copy"
o:"whenever" o:"trigger" o:"additional"
```

### Recursion (dies / sacrifice / graveyard return)
```
o:"return" o:"from your graveyard" t:creature
o:"whenever a creature dies"
o:"persist" or o:"undying"
```

### Wincons that close combo loops
```
o:"loses the game" -t:land
o:"each opponent" o:"life"
o:"infinite" -t:land   (rarely literal but worth checking)
o:"each player" o:"deck"   (mill wins)
```

### Recur a single card on demand
```
o:"return" o:"to your hand" cmc<=2
o:"to the battlefield" o:"target" cmc<=3
```

---

## Archetype / theme searches

### Tribal pools
```
t:[creature_type] ci:[colors] f:edh        (full tribal pool)
t:[creature_type] ci:[colors] cmc<=3 f:edh (low-curve tribal)
```

### Theme: tokens
```
o:"create" o:"token" ci:[colors]
o:"populate" ci:gw
```

### Theme: +1/+1 counters
```
o:"+1/+1 counter" ci:[colors]
o:"proliferate"
```

### Theme: sacrifice / aristocrats
```
(o:"sacrifice a creature" or o:"whenever a creature dies") ci:[colors]
```

### Theme: blink / flicker
```
o:"exile target" o:"return it to the battlefield"
o:"return it to the battlefield" -t:instant -t:sorcery
```

### Theme: storm / spellslinger
```
o:"whenever you cast" o:"instant or sorcery"
o:"storm" -is:storm   (cards that grant or use storm count)
```

### Theme: lifegain
```
(o:"whenever you gain life" or o:"if you gained life this turn") ci:[colors]
```

---

## Mana base patterns

### Color fixing for [color identity]
```
t:land ci:[colors] -t:basic
t:land produces:[colors]   (for specific color combos)
```

### Untapped duals at common rarity (budget)
```
t:land ci:[colors] o:"enters the battlefield" -o:"tapped" r<=u
```

### Fetchlands (canonical 10)
```
t:land o:"search your library" o:"forest or" -is:reprint
```
(narrower: `t:fetchland` is not a real Scryfall tag — use the oracle text)

### Triomes / tri-lands
```
t:land o:"basic land types"
```

### MDFCs (modal double-faced lands / land-back spells)
```
is:dfc t:land
```

### Utility lands by function
```
t:land o:"draw a card"          (card-draw lands)
t:land o:"target creature gets"  (combat-trick lands)
t:land o:"sacrifice"             (sac outlets in lands)
```

---

## Constraint-stacking patterns

### Cheap [function] in [colors] for Commander
```
o:"[function]" ci:[colors] cmc<=2 f:edh
```

### Budget alternative for an effect
```
o:"[oracle phrase]" usd<=2 -is:reprint   (sort by oracle relevance, then price)
```

### Find redundancy for a key card
1. Read the card's oracle text via `scryfall_card`.
2. Pull the most distinctive 4–6 words.
3. Search `o:"that distinctive phrase" ci:[colors]` to find similar effects.
4. Filter by CMC, format, and price as needed.

Example: Looking for redundancy for *Smothering Tithe*?
```
o:"create a treasure token" o:"whenever an opponent" ci:w
```

### Finding "X but cheaper / colorshifted"
The pattern: take the original card's oracle text, generalize it slightly, and search.
- *Cyclonic Rift* alternatives: `o:"return" o:"all" o:"nonland" t:instant ci:u`
- *Counterspell* alternatives: `t:instant o:"counter target spell" ci:u cmc<=2`

---

## Antipatterns

- **Don't search by power level.** Scryfall has no "power" tag. The Brewer/Optimizer's job is to interpret search results, not delegate the judgment.
- **Don't use `c:` for Commander color identity.** Use `ci:`. `c:` is too restrictive — it excludes cards whose casting cost is a different color than their identity.
- **Don't return huge result sets uncritically.** Cap with `limit` and narrow the query. 200 results is unhelpful; 20 well-filtered results are.
- **Don't trust the first match for fuzzy card-name lookups.** When using `scryfall_card` with a possibly-misspelled name, verify the returned card is the intended one before continuing analysis.

---

## Working with `is:game-changer`

For the Table Captain and Optimizer when bracket-counting:
```
is:game-changer ci:[colors]   (Game Changers in this color identity)
is:game-changer t:[type]      (e.g., is:game-changer t:land for land GCs)
```

The `is:game-changer` tag is the live, authoritative answer to "is this a Game Changer?" — Scryfall keeps it current with the WotC list.
