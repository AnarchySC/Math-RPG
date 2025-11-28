# Phase 4: Build One Complete Battle

## Overview

You have a prototype. You have your numbers. Now it's time to build one COMPLETE battle with every mechanic working together. This is your vertical slice — a tiny but fully-featured version of the final game.

By the end of this phase, you'll fight one enemy with all four math types, buffs, healing, potions, and proper UI feedback.

---

## What "Complete" Means

A complete battle includes:

- All 4 math problem types (not just addition)
- Each type triggers its correct effect (heal, mana, attack buff, defense buff)
- Buffs have duration and expire
- Mana exists as a resource (even if you're not using it yet)
- Potions can be used and affect problem distribution
- UI shows all relevant information clearly
- Visual and audio feedback for actions
- Penalty for wrong answers implemented

---

## Implementation Checklist

### Step 1: Implement All Four Math Types

**What to do:**
1. Create generators for addition, subtraction, multiplication, and division
2. Ensure division always produces clean results (no remainders)
3. Randomly select which type appears (25% each for now)
4. Display the problem with the operation symbol clearly visible

**Code structure suggestion:**
```
function generateProblem(type):
    if type == "addition":
        return generateAddition()
    elif type == "subtraction":
        return generateSubtraction()
    elif type == "multiplication":
        return generateMultiplication()
    elif type == "division":
        return generateDivision()

function getRandomProblemType():
    return random.choice(["addition", "subtraction", "multiplication", "division"])
```

**Testing:** Generate 100 problems and verify each type appears roughly 25 times.

---

### Step 2: Implement Addition → Healing

**What to do:**
1. When player correctly answers an addition problem, heal them
2. Apply time multiplier to heal amount
3. Cap healing at max HP (don't overheal)
4. Show healing feedback ("+22 HP!")

**Edge case:** Player at full health still gets addition problem. Options:
- Let them "waste" the heal (realistic)
- Overheal into temporary bonus HP (interesting but complex)
- Show "Already at full health!" message

**Recommendation:** Allow wasted heals — it teaches players to manage their problem types strategically.

---

### Step 3: Implement Subtraction → Mana Restoration

**What to do:**
1. Correct subtraction answer restores mana
2. Apply time multiplier
3. Cap at max mana
4. Show feedback ("+15 Mana!")

**Question:** What does mana DO in your game?

Options for mana usage:
- **Special attacks:** Spend mana for powerful moves (not implemented yet)
- **Potion usage:** Potions cost mana to activate
- **Nothing yet:** Just track it, make it useful in Phase 5

**Recommendation:** For now, just track mana. Add special attacks in Phase 5 or later.

---

### Step 4: Implement Multiplication → Attack Buff

**What to do:**
1. Correct multiplication applies an Attack buff
2. Store buff amount and remaining duration
3. Apply buff to damage calculations
4. Show buff icon or text on UI ("ATK +15 [3 turns]")
5. Decrement duration each turn
6. Remove buff when duration hits 0

**Buff stacking decision:**
- **Stack additively:** Multiple buffs add together (simple)
- **Refresh duration:** New buff replaces old, resets timer (simpler)
- **Stack with diminishing returns:** Each additional buff is less effective (complex)

**Recommendation:** Refresh duration — it's simplest and prevents buff hoarding.

**Implementation:**
```
function applyAttackBuff(amount, duration):
    player.attackBuff = amount  # Replace, don't add
    player.attackBuffDuration = duration

function onTurnEnd():
    if player.attackBuffDuration > 0:
        player.attackBuffDuration -= 1
    if player.attackBuffDuration == 0:
        player.attackBuff = 0
```

---

### Step 5: Implement Division → Defense Buff

**What to do:**
1. Same pattern as attack buff
2. Store defense buff amount and duration
3. Apply buff to damage received
4. Show on UI
5. Expire after duration

**Damage received formula:**
```
damageTaken = enemyAttack - (player.baseDefense + player.defenseBuff)
damageTaken = max(damageTaken, 1)  # Always take at least 1 damage
```

---

### Step 6: Add Mana as a Resource

**What to do:**
1. Display mana bar/number on UI
2. Mana changes when subtraction is solved correctly
3. (Optional) Mana costs for abilities

**Even if mana does nothing yet**, showing it teaches players it exists and primes them for future mechanics.

---

### Step 7: Create Basic Battle UI

**Required UI elements:**
- Player HP (current / max)
- Player Mana (current / max)
- Active buffs with remaining duration
- Enemy HP (current / max)
- Current math problem
- Input field or answer buttons
- Timer display
- Feedback message area

**Layout suggestion:**
```
+----------------------------------+
|  PLAYER          |        ENEMY  |
|  HP: 85/100      |    HP: 35/50  |
|  MP: 40/50       |               |
|  [ATK+15 2 turns]|               |
+----------------------------------+
|                                  |
|         24 + 17 = ?              |
|                                  |
|        [ INPUT BOX ]             |
|        [ SUBMIT ]                |
|                                  |
|        Timer: 3.2s               |
|                                  |
|      "Great! +18 damage!"        |
+----------------------------------+
|  [Use Potion ▼]                  |
+----------------------------------+
```

---

### Step 8: Add Affinity Potions to Inventory

**What to do:**
1. Create an inventory system (even if just 4 potion slots)
2. Start the battle with some potions for testing
3. Add UI to see inventory during battle

**Inventory structure:**
```
inventory = {
    "addition_potion": 3,
    "subtraction_potion": 2,
    "multiplication_potion": 2,
    "division_potion": 1
}
```

---

### Step 9: Implement Potion Usage

**What to do:**
1. Allow player to use a potion (button or menu)
2. Decrement potion count
3. Set active affinity effect
4. Track remaining duration (number of problems or turns)

**Using a potion should:**
- Happen instead of OR before answering a problem (your choice)
- Show feedback ("Used Addition Potion! Addition problems more likely.")
- Visually indicate active affinity (color glow, icon)

**Recommendation:** Allow potion use BEFORE the problem appears each turn, so player can strategically choose.

---

### Step 10: Make Potions Affect Probability

**What to do:**
1. When generating a problem, check for active affinity
2. If affinity active, use weighted random selection
3. Affinity expires after set duration

**Weighted selection implementation:**
```
function getRandomProblemType():
    if activeAffinity == null:
        weights = [25, 25, 25, 25]  # Equal chance
    elif activeAffinity == "addition":
        weights = [55, 15, 15, 15]  # 55% addition
    elif activeAffinity == "subtraction":
        weights = [15, 55, 15, 15]
    # ... etc
    
    return weightedRandomChoice(types, weights)
```

---

### Step 11: Add Feedback for Correct Answers

**Visual feedback ideas:**
- Screen flash (green tint)
- Number popup showing damage/healing (+18!)
- Enemy shake or blink when hit
- Sound effect (satisfying ding)

**Text feedback by result:**
- Perfect: "PERFECT! ⚡" (big, flashy)
- Great: "Great!" 
- Good: "Good"
- OK: (no special message)
- Slow: "Slow..."

**Make correct answers feel GOOD.** This is where dopamine comes from.

---

### Step 12: Add Feedback for Wrong Answers

**Visual feedback:**
- Screen flash (red tint)
- "X" or "Wrong!" display
- Buzz or error sound
- Show the correct answer

**Mechanical consequence:**
- Enemy gets free attack (recommended)
- Player loses a turn
- Or nothing (for easy mode)

**Show the correct answer!** This is educational. Player should learn from mistakes.

---

### Step 13: Balance the Complete Fight

Now that everything works, fight your test enemy 20+ times:

**Questions to answer:**
1. How many turns does a typical fight take? (Target: 5-10)
2. How often do you die? (Target: rarely at first enemy)
3. Are buffs worth using? Do they feel impactful?
4. Is any math type too hard or too easy?
5. Do potions feel useful?

**Adjust until it feels right:**
- Too easy? Raise enemy attack, lower time multipliers
- Too hard? Lower enemy stats, increase healing
- Buffs useless? Increase buff amounts or durations
- One math type ignored? Rebalance its effect

---

## Testing Protocol

### Test 1: Basic Functionality
- [ ] Can generate and solve addition problems
- [ ] Can generate and solve subtraction problems
- [ ] Can generate and solve multiplication problems
- [ ] Can generate and solve division problems
- [ ] All operations appear roughly equally

### Test 2: Effects Working
- [ ] Addition heals player
- [ ] Subtraction restores mana
- [ ] Multiplication applies attack buff
- [ ] Division applies defense buff
- [ ] Buffs expire after correct duration

### Test 3: Time Multipliers
- [ ] Fast answers deal more damage/healing
- [ ] Slow answers deal less
- [ ] Perfect threshold feels achievable but challenging

### Test 4: Combat Flow
- [ ] Player and enemy take turns
- [ ] HP updates correctly
- [ ] Battle ends on win
- [ ] Battle ends on loss

### Test 5: Potions
- [ ] Can use potions during battle
- [ ] Potion count decreases
- [ ] Affinity effect activates
- [ ] Problem distribution changes
- [ ] Effect expires correctly

### Test 6: UI/UX
- [ ] All information visible
- [ ] Feedback is clear
- [ ] No confusion about what's happening

---

## Time Estimate for Phase 4

| Task | Time |
|------|------|
| All math type generators | 1-2 hours |
| Implement healing (addition) | 1 hour |
| Implement mana restore (subtraction) | 30 min |
| Implement attack buff (multiplication) | 1-2 hours |
| Implement defense buff (division) | 1 hour |
| Create battle UI | 2-3 hours |
| Inventory and potions | 2-3 hours |
| Potion probability effects | 1-2 hours |
| Feedback polish | 1-2 hours |
| Balance testing | 3-5 hours |
| **Total** | **14-22 hours** |

---

## Phase 4 Checklist

- [ ] All 4 math problem types generate correctly
- [ ] Problem type is randomly selected
- [ ] Addition → Healing implemented
- [ ] Subtraction → Mana restoration implemented
- [ ] Multiplication → Attack buff with duration
- [ ] Division → Defense buff with duration
- [ ] Buffs display on UI
- [ ] Buffs expire correctly
- [ ] Mana displays (even if unused)
- [ ] Inventory system exists
- [ ] Player starts with test potions
- [ ] Can use potions during battle
- [ ] Potions affect problem probability
- [ ] Affinity effect has duration
- [ ] Correct answers show satisfying feedback
- [ ] Wrong answers show feedback and consequence
- [ ] Correct answer revealed on wrong answer
- [ ] Battle balanced and fun
- [ ] Playtested 20+ times

---

## What You Should Have Now

One enemy. One complete fight. Every mechanic working. It's still ugly (rectangles and programmer art), but it's a real game now.

If you showed this to someone, they could play it and understand it.

---

## Next Up

**Phase 5: Add Progression** — Stats that persist, leveling up, and a reason to keep fighting.
