# Phase 3: Design Your Numbers

## Overview

Game design is math. Before you balance by feel, you need to understand the numbers driving your system. This phase is about spreadsheets, formulas, and making conscious decisions about difficulty curves.

**Why this matters:** If you wing it, you'll spend forever tweaking random values trying to make things "feel right." A spreadsheet lets you see the whole system at once and make informed changes.

---

## Core Stats to Define

### Player Base Stats

These are the starting values for a new player:

| Stat | What It Does | Suggested Starting Value |
|------|--------------|--------------------------|
| HP | How much damage you can take | 100 |
| Attack | Base damage dealt (before time bonus) | 10 |
| Defense | Reduces incoming damage | 5 |
| Mana | Resource for special abilities | 50 |

**Why these values?** 
- HP at 100 makes percentages intuitive (50 HP = 50% health)
- Attack at 10 makes mental math easy (2x bonus = 20 damage)
- Defense at 5 is low enough to matter but not dominant
- Mana at 50 gives room to grow

---

### Enemy Base Stats (Test Enemy)

Your first enemy should be beatable but not trivial:

| Stat | Value | Reasoning |
|------|-------|-----------|
| HP | 50 | Dies in ~5-7 correct answers |
| Attack | 8 | Takes ~12 hits to kill player |
| Defense | 2 | Player damage still feels impactful |

**Design philosophy:** Early enemies should teach mechanics, not punish players. Make them easy enough that players feel powerful while learning.

---

## Time-to-Damage Formula

This is the heart of your game. Fast answers = strong attacks.

### Basic Formula

```
Final Damage = Base Attack × Time Multiplier × Buff Multiplier - Enemy Defense
```

### Time Multiplier Table

| Answer Time | Multiplier | Label | Feedback |
|-------------|------------|-------|----------|
| 0-2 seconds | 2.0 | Perfect | "PERFECT! ⚡" |
| 2-4 seconds | 1.5 | Great | "Great!" |
| 4-6 seconds | 1.2 | Good | "Good" |
| 6-10 seconds | 1.0 | OK | "OK" |
| 10-15 seconds | 0.75 | Slow | "Slow..." |
| 15+ seconds | 0.5 | Very Slow | "Too slow!" |

### Example Calculation

```
Player Attack: 10
Time to answer: 3 seconds (Great = 1.5x)
No buffs active (Buff Multiplier = 1.0)
Enemy Defense: 2

Final Damage = 10 × 1.5 × 1.0 - 2 = 13 damage
```

---

## Math Problem Difficulty Scaling

As players level up, problems should get harder. Here's how to scale each operation:

### Addition Difficulty Tiers

| Player Level | Number Range | Example |
|--------------|--------------|---------|
| 1-5 | 1-10 | 3 + 7 = ? |
| 6-10 | 1-20 | 14 + 18 = ? |
| 11-15 | 10-50 | 23 + 47 = ? |
| 16-20 | 20-100 | 67 + 84 = ? |
| 21+ | 50-200 | 143 + 89 = ? |

### Subtraction Difficulty Tiers

| Player Level | Number Range | Example |
|--------------|--------------|---------|
| 1-5 | Result 1-10 | 9 - 4 = ? |
| 6-10 | Result 1-20 | 25 - 8 = ? |
| 11-15 | Result 10-50 | 73 - 29 = ? |
| 16-20 | Result 20-100 | 156 - 78 = ? |
| 21+ | Result 50-200 | 234 - 167 = ? |

**Important:** Always ensure the first number is larger to avoid negative results.

### Multiplication Difficulty Tiers

| Player Level | Number Range | Example |
|--------------|--------------|---------|
| 1-5 | 1-5 × 1-5 | 3 × 4 = ? |
| 6-10 | 1-10 × 1-10 | 7 × 8 = ? |
| 11-15 | 5-12 × 2-10 | 9 × 11 = ? |
| 16-20 | 10-15 × 5-12 | 12 × 13 = ? |
| 21+ | 10-20 × 10-15 | 14 × 17 = ? |

### Division Difficulty Tiers

| Player Level | Divisor Range | Example |
|--------------|---------------|---------|
| 1-5 | 1-5 | 15 ÷ 3 = ? |
| 6-10 | 2-10 | 48 ÷ 6 = ? |
| 11-15 | 5-12 | 84 ÷ 7 = ? |
| 16-20 | 6-15 | 143 ÷ 11 = ? |
| 21+ | 8-20 | 288 ÷ 16 = ? |

**Important:** Generate division problems by picking the answer first, then multiplying. This ensures clean results.

```
To generate "? ÷ 8 = ?"
1. Pick divisor: 8
2. Pick answer: 7 (from appropriate range)
3. Calculate dividend: 8 × 7 = 56
4. Problem: "56 ÷ 8 = ?" Answer: 7
```

---

## Stat Effect Formulas

Each math type affects a different stat:

### Addition → Healing

```
Heal Amount = Base Heal × Time Multiplier

Base Heal = 15 (at level 1)
Scale: +2 per player level
```

| Time | Multiplier | Heal at Level 1 |
|------|------------|-----------------|
| Perfect | 2.0 | 30 HP |
| Great | 1.5 | 22 HP |
| Good | 1.2 | 18 HP |
| OK | 1.0 | 15 HP |

### Subtraction → Mana Restoration

```
Mana Restored = Base Mana × Time Multiplier

Base Mana = 10 (at level 1)
Scale: +1 per player level
```

### Multiplication → Attack Buff

```
Attack Bonus = Base Buff × Time Multiplier
Duration = 3 turns (doesn't scale)

Base Buff = +5 Attack (at level 1)
Scale: +1 per player level
```

**Example:** At level 5, a "Great" multiplication gives +10 × 1.5 = +15 Attack for 3 turns.

### Division → Defense Buff

```
Defense Bonus = Base Buff × Time Multiplier  
Duration = 3 turns (doesn't scale)

Base Buff = +3 Defense (at level 1)
Scale: +1 per player level
```

---

## XP and Leveling Curve

### XP Per Battle

```
XP Gained = Base XP × Enemy Level Modifier × Performance Bonus

Base XP = 20
Enemy Level Modifier = Enemy Level / Player Level (min 0.5, max 2.0)
Performance Bonus = Average Time Multiplier across battle
```

**Example:**
- Beat a level 3 enemy as a level 2 player
- Average time multiplier was 1.3
- XP = 20 × 1.5 × 1.3 = 39 XP

### XP Required Per Level

Use an exponential curve so early levels feel fast:

| Level | XP Required | Total XP |
|-------|-------------|----------|
| 1→2 | 50 | 50 |
| 2→3 | 75 | 125 |
| 3→4 | 100 | 225 |
| 4→5 | 150 | 375 |
| 5→6 | 200 | 575 |
| 6→7 | 275 | 850 |
| 7→8 | 350 | 1200 |
| 8→9 | 450 | 1650 |
| 9→10 | 550 | 2200 |

**Formula:** `XP for next level = 50 × (1.3 ^ (current level - 1))`

---

## Stat Leveling (The Math-Type XP System)

Each math operation levels its associated stat independently:

| Math Type | Stat Leveled | XP Per Correct Answer |
|-----------|--------------|----------------------|
| Addition | Max HP (+5 per level) | 10 |
| Subtraction | Max Mana (+3 per level) | 10 |
| Multiplication | Attack (+1 per level) | 10 |
| Division | Defense (+1 per level) | 10 |

**Stat Level Curve:**

| Stat Level | XP Required |
|------------|-------------|
| 1→2 | 50 |
| 2→3 | 100 |
| 3→4 | 175 |
| 4→5 | 275 |
| 5→6 | 400 |

This means players naturally level up the stats for math they're good at. If you're great at multiplication, your Attack will outpace your other stats.

---

## Affinity Potion Effects

Potions shift the probability of getting certain problem types:

### Default Problem Distribution

| Type | Base Chance |
|------|-------------|
| Addition | 25% |
| Subtraction | 25% |
| Multiplication | 25% |
| Division | 25% |

### After Using a Potion

**Addition Potion:**
| Type | Chance |
|------|--------|
| Addition | 55% (+30%) |
| Subtraction | 15% |
| Multiplication | 15% |
| Division | 15% |

Apply same pattern for other potions. Duration: Entire battle or 10 problems, whichever comes first.

---

## Your Spreadsheet Setup

Create a spreadsheet with these tabs:

### Tab 1: Base Stats
All starting values for player and test enemy.

### Tab 2: Time Multipliers
The speed bonuses table — you'll tweak this a lot.

### Tab 3: Problem Difficulty
Number ranges for each operation at each level.

### Tab 4: XP Curves
Level requirements and stat growth.

### Tab 5: Enemy Roster
Stats for each enemy type you'll create.

### Tab 6: Balance Testing
Record your playtests: "Level 3, Enemy 2, Won/Lost, Time, Notes"

---

## Balance Testing Process

1. **Play through with the numbers as designed**
2. **Note anything that feels off:**
   - Too easy? Raise enemy stats or lower time bonuses
   - Too hard? Lower enemy stats or increase player healing
   - Boring? Make time thresholds tighter for more pressure
   - Math too easy/hard? Adjust difficulty tiers

3. **Change ONE variable at a time**
4. **Playtest again**
5. **Repeat until it feels right**

**Golden rule:** If you change three things at once and it feels better, you won't know which change helped.

---

## Time Estimate for Phase 3

| Task | Time |
|------|------|
| Define base stats | 30 min |
| Create time-to-damage formula | 1 hour |
| Design math difficulty tiers | 1-2 hours |
| Create XP/leveling curve | 1 hour |
| Design potion effects | 30 min |
| Set up spreadsheet | 1-2 hours |
| Initial balance testing | 2-4 hours |
| **Total** | **7-11 hours** |

---

## Phase 3 Checklist

- [ ] Player base stats defined (HP, Attack, Defense, Mana)
- [ ] Test enemy stats defined
- [ ] Time-to-damage formula created
- [ ] Time thresholds set (Perfect, Great, Good, etc.)
- [ ] Math difficulty tiers for all 4 operations
- [ ] Healing formula (Addition)
- [ ] Mana restoration formula (Subtraction)
- [ ] Attack buff formula (Multiplication)
- [ ] Defense buff formula (Division)
- [ ] XP per battle formula
- [ ] Level-up XP requirements
- [ ] Stat-specific leveling system
- [ ] Potion probability effects
- [ ] Spreadsheet created with all values
- [ ] Playtested and adjusted at least 5 times

---

## Next Up

**Phase 4: Build One Complete Battle** — Take your formulas and implement ALL mechanics in a single, fully-featured fight.
