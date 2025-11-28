# Phase 5: Add Progression

## Overview

A single battle is fun once. Progression is what makes players come back. This phase adds persistent stats, leveling, and rewards — the RPG loop that keeps players engaged.

By the end of this phase, your game will remember what happened between battles.

---

## What Progression Means for Your Game

Players need to feel growth over time:

1. **Stats increase** — Numbers go up (always satisfying)
2. **New challenges unlock** — Harder enemies become beatable
3. **Resources accumulate** — Gold, items, equipment
4. **Skills improve** — Better at specific math types

Your Math RPG has a unique hook: **math practice directly improves character strength**. The player who's good at multiplication will have high Attack. The player who needs healing a lot will have high HP.

---

## Core Systems to Implement

### System 1: Persistent Player Data

**What to store between battles:**
```
playerData = {
    // Character level and XP
    level: 1,
    currentXP: 0,
    xpToNextLevel: 50,
    
    // Base stats
    maxHP: 100,
    maxMana: 50,
    attack: 10,
    defense: 5,
    
    // Stat-specific XP (from math types)
    hpXP: 0,        // From addition
    manaXP: 0,      // From subtraction
    attackXP: 0,    // From multiplication
    defenseXP: 0,   // From division
    
    // Stat levels
    hpLevel: 1,
    manaLevel: 1,
    attackLevel: 1,
    defenseLevel: 1,
    
    // Resources
    gold: 0,
    
    // Inventory
    inventory: {
        additionPotion: 3,
        subtractionPotion: 2,
        multiplicationPotion: 2,
        divisionPotion: 1
    },
    
    // Stats tracking
    battlesWon: 0,
    totalProblemsAnswered: 0,
    perfectAnswers: 0
}
```

---

### System 2: XP Gain After Battle

**When a battle ends in victory:**

1. Calculate battle XP (from Phase 3 formula)
2. Add to player's currentXP
3. Check if currentXP >= xpToNextLevel
4. If yes, level up

**Battle XP formula reminder:**
```
battleXP = baseXP × enemyLevelModifier × performanceBonus

baseXP = 20
enemyLevelModifier = enemyLevel / playerLevel (clamped 0.5 to 2.0)
performanceBonus = averageTimeMultiplier (e.g., 1.3)
```

**Victory screen should show:**
```
+---------------------------+
|        VICTORY!           |
+---------------------------+
| XP Earned: +45            |
| [████████░░] 78/100 XP    |
|                           |
| Gold Earned: +15          |
| Total Gold: 230           |
|                           |
| Problems Solved: 7        |
| Perfect Answers: 3        |
| Accuracy: 85%             |
+---------------------------+
|      [Continue]           |
+---------------------------+
```

---

### System 3: Level Up System

**When player levels up:**

1. Reset currentXP (carry over excess)
2. Increase xpToNextLevel
3. Boost all base stats slightly

**Stat gains per level:**
| Stat | Increase per Level |
|------|-------------------|
| Max HP | +10 |
| Max Mana | +5 |
| Attack | +2 |
| Defense | +1 |

**Level up flow:**
```
function checkLevelUp():
    while currentXP >= xpToNextLevel:
        currentXP -= xpToNextLevel
        level += 1
        xpToNextLevel = calculateXPNeeded(level)
        applyLevelUpBonuses()
        showLevelUpScreen()
```

**Level up screen:**
```
+---------------------------+
|      LEVEL UP!            |
|      Level 4 → 5          |
+---------------------------+
| Max HP: 130 → 140 (+10)   |
| Max Mana: 65 → 70 (+5)    |
| Attack: 16 → 18 (+2)      |
| Defense: 8 → 9 (+1)       |
+---------------------------+
|      [Continue]           |
+---------------------------+
```

---

### System 4: Math-Type Stat Leveling

This is your game's unique twist: **each math type levels its own stat**.

**After each correct answer:**
```
function onCorrectAnswer(mathType, timeMultiplier):
    xpGained = 10 × timeMultiplier
    
    if mathType == "addition":
        hpXP += xpGained
        checkStatLevelUp("hp")
    elif mathType == "subtraction":
        manaXP += xpGained
        checkStatLevelUp("mana")
    elif mathType == "multiplication":
        attackXP += xpGained
        checkStatLevelUp("attack")
    elif mathType == "division":
        defenseXP += xpGained
        checkStatLevelUp("defense")
```

**Stat level XP requirements:**
| Stat Level | XP Required |
|------------|-------------|
| 1 → 2 | 50 |
| 2 → 3 | 100 |
| 3 → 4 | 175 |
| 4 → 5 | 275 |
| 5 → 6 | 400 |

**Stat bonuses per stat level:**
| Stat | Bonus per Stat Level |
|------|---------------------|
| HP Level | +5 Max HP |
| Mana Level | +3 Max Mana |
| Attack Level | +1 Attack |
| Defense Level | +1 Defense |

**This creates emergent player builds:**
- Good at multiplication? High attack, glass cannon build
- Always healing? Tank build with high HP
- Balanced player? Balanced stats
- Struggling with division? Weak defense, motivation to practice

---

### System 5: Track Individual Stat Progress

**Show stat XP in a character screen:**
```
+----------------------------------+
|         CHARACTER STATS          |
+----------------------------------+
| Level 5        XP: 45/200        |
+----------------------------------+
| HP: 145    [████████░░] Lv.3     |
| Mana: 65   [██████░░░░] Lv.2     |
| Attack: 21 [██████████] Lv.5     |
| Defense: 9 [████░░░░░░] Lv.2     |
+----------------------------------+
| Battles Won: 23                  |
| Problems Solved: 187             |
| Perfect Answers: 42 (22%)        |
+----------------------------------+
```

This motivates players to work on weak stats.

---

### System 6: Inventory System

**Basic inventory structure:**
```
inventory = {
    // Potions
    additionPotion: 5,
    subtractionPotion: 3,
    multiplicationPotion: 4,
    divisionPotion: 2,
    
    // Healing items (optional)
    smallHealthPotion: 10,  // Heal 25 HP instantly
    largeHealthPotion: 3,   // Heal 75 HP instantly
    
    // Maybe later: equipment slots
    // weapon: null,
    // armor: null,
    // accessory: null
}
```

**Inventory UI:**
- Show during battle (potion section)
- Show in menu between battles (full inventory)
- Update after shop purchases
- Persist between sessions

---

### System 7: Gold and Economy

**Gold sources:**
- Battle victory: 10-30 gold based on enemy
- Perfect answers: +2 gold each
- Found in treasure (later phases)

**Gold sinks:**
- Shop purchases
- Maybe: Inn to restore HP between battles

**Keep economy simple at first.** You can add complexity later.

---

### System 8: Simple Shop

**Shop items:**
| Item | Price | Effect |
|------|-------|--------|
| Addition Potion | 20g | +30% addition chance for battle |
| Subtraction Potion | 20g | +30% subtraction chance for battle |
| Multiplication Potion | 20g | +30% multiplication chance for battle |
| Division Potion | 20g | +30% division chance for battle |
| Small Health Potion | 15g | Heal 25 HP instantly in battle |
| Large Health Potion | 40g | Heal 75 HP instantly in battle |

**Shop UI:**
```
+----------------------------------+
|            SHOP                  |
+----------------------------------+
| Your Gold: 145                   |
+----------------------------------+
| Addition Potion     20g   [Buy]  |
| Subtraction Potion  20g   [Buy]  |
| Multiplication Pot. 20g   [Buy]  |
| Division Potion     20g   [Buy]  |
| Small Health Pot.   15g   [Buy]  |
| Large Health Pot.   40g   [Buy]  |
+----------------------------------+
|           [Exit]                 |
+----------------------------------+
```

---

### System 9: Save and Load

**Critical:** Players will quit and come back. Their progress MUST persist.

**What to save:**
- All playerData (stats, XP, level, inventory, gold)
- Current location in game (later phases)
- Settings preferences

**When to save:**
- After every battle
- After shop purchases
- When quitting game
- Periodically (every few minutes)

**Save format options:**
- **JSON file** — Simple, human-readable, easy to debug
- **Binary** — Smaller, harder to cheat
- **Cloud save** — Complex, requires backend

**Recommendation:** Start with local JSON. Add cloud saves way later.

**Save implementation:**
```
function saveGame():
    data = {
        version: "1.0",
        timestamp: getCurrentTime(),
        player: playerData
    }
    writeToFile("savegame.json", JSON.stringify(data))

function loadGame():
    if fileExists("savegame.json"):
        data = JSON.parse(readFile("savegame.json"))
        playerData = data.player
        return true
    return false  // No save found
```

**Handle missing saves gracefully:**
- New players start fresh
- Corrupted saves show error, offer to start over
- Version mismatch? Migrate or warn

---

## Game Loop With Progression

```
MAIN MENU
    ↓
[New Game] or [Continue]
    ↓
HUB SCREEN (Phase 6 will expand this)
    ↓
[Fight] → BATTLE → Victory/Defeat
    ↓              ↓
    ↓         [XP + Gold + Stat XP]
    ↓              ↓
    ←──────────────┘
    ↓
[Shop] → Buy items
    ↓
[Stats] → View progress
    ↓
[Save & Quit]
```

---

## Testing Your Progression

### Test 1: XP and Leveling
- [ ] XP earned after battle
- [ ] Level up triggers at correct threshold
- [ ] Stats increase on level up
- [ ] XP carries over past level threshold

### Test 2: Stat-Specific XP
- [ ] Addition answers give HP XP
- [ ] Subtraction answers give Mana XP
- [ ] Multiplication answers give Attack XP
- [ ] Division answers give Defense XP
- [ ] Stat levels increase stats correctly

### Test 3: Persistence
- [ ] Save game works
- [ ] Load game restores all data
- [ ] Progress survives closing the game

### Test 4: Economy
- [ ] Gold earned from battles
- [ ] Shop allows purchases
- [ ] Inventory updates correctly
- [ ] Items usable in battle

---

## Time Estimate for Phase 5

| Task | Time |
|------|------|
| Persistent player data structure | 1 hour |
| XP gain after battle | 1-2 hours |
| Level up system | 2-3 hours |
| Stat-specific XP system | 2-3 hours |
| Inventory system | 2-3 hours |
| Gold and economy | 1-2 hours |
| Shop implementation | 2-3 hours |
| Save/load system | 3-5 hours |
| Testing and balancing | 2-4 hours |
| **Total** | **16-26 hours** |

---

## Phase 5 Checklist

- [ ] Player data structure defined
- [ ] Data persists between battles
- [ ] XP awarded after victories
- [ ] Level up system works
- [ ] Stats increase on level up
- [ ] Stat-specific XP (HP, Mana, Attack, Defense)
- [ ] Stat levels visible to player
- [ ] Inventory system holds items
- [ ] Gold tracked and earned
- [ ] Shop allows purchases
- [ ] Save game works
- [ ] Load game works
- [ ] Progress survives quit and relaunch
- [ ] Character stats screen shows all info
- [ ] Victory screen shows rewards
- [ ] 10+ battles tested with progression intact

---

## What You Should Have Now

A game you can play for multiple sessions. Your character gets stronger. Your resources accumulate. There's a reason to fight another battle.

It's still one enemy and one battle arena, but the RPG loop is complete.

---

## Next Up

**Phase 6: Create the World** — Movement, maps, NPCs, and multiple enemies to fight.
