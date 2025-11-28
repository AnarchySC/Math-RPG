# Phase 2: Make It Playable Ugly First

## Overview

This is the most important phase of development. You're going to build the core battle system using ugly rectangles and placeholder everything. No sprites, no polish, no distractions.

**Why ugly first?** Because if the core loop isn't fun with rectangles, pretty graphics won't save it. You need to know if your math-combat idea actually works before investing weeks in art and polish.

---

## What You're Building

By the end of this phase, you'll have:

- A battle screen with a player and enemy
- Math problems that appear when you attack
- A timer tracking how fast you answer
- Damage dealt based on correct/incorrect answers
- Win/lose conditions

It will look terrible. That's the point.

---

## Step-by-Step Implementation

### Step 1: Create a Battle Scene

**What to do:**
1. Create a new scene called "Battle" (or similar)
2. Add two rectangles: one for the player (left side), one for the enemy (right side)
3. Use different colors so you can tell them apart (blue = player, red = enemy)
4. Add labels showing each character's name and HP

**Technical notes:**
- In Godot: Use ColorRect nodes for rectangles, Label nodes for text
- In Unity: Use UI Image components or simple sprites
- In RPG Maker: Use the built-in battle system as a starting point, then customize

**Your goal:** A static screen showing "Player HP: 100" on one side and "Enemy HP: 50" on the other.

---

### Step 2: Display a Math Problem

**What to do:**
1. Add a text label in the center of the screen (this will show the math problem)
2. Write code that generates a random math problem
3. Store the correct answer somewhere your code can check later

**Generating problems by type:**

```
ADDITION:
- Pick two random numbers (e.g., 1-20)
- Problem: "7 + 13 = ?"
- Answer: 20

SUBTRACTION:
- Pick two random numbers, make sure first is larger
- Problem: "18 - 5 = ?"
- Answer: 13

MULTIPLICATION:
- Pick two random numbers (keep them small at first, e.g., 1-10)
- Problem: "6 × 8 = ?"
- Answer: 48

DIVISION:
- Pick the answer first, then multiply to get the dividend
- Example: answer = 7, multiplier = 4, so problem is "28 ÷ 4 = ?"
- This ensures clean division with no remainders
```

**Your goal:** Pressing a button shows a random math problem on screen.

---

### Step 3: Accept Player Input

**What to do:**
1. Add an input field where the player types their answer (or use multiple choice buttons)
2. Add a "Submit" button (or accept Enter key)
3. When submitted, compare player's answer to correct answer

**Design decision — Text input vs. Multiple choice:**

| Text Input | Multiple Choice |
|------------|-----------------|
| Harder (requires typing) | Easier (can guess) |
| More authentic math practice | Faster gameplay |
| Risk of typos frustrating players | Less educational value |
| Better for older players | Better for younger players |

**Recommendation:** Start with text input. You can always add multiple choice later as an "easy mode."

**Your goal:** Player can type an answer and submit it.

---

### Step 4: Check Answers and Give Feedback

**What to do:**
1. Compare submitted answer to stored correct answer
2. Show "Correct!" or "Wrong!" feedback
3. Make it obvious (color the text green or red)

**Handling edge cases:**
- Trim whitespace from input (player might type " 42 " instead of "42")
- Handle empty submissions (don't let blank answers count)
- Consider case sensitivity if using text (shouldn't matter for numbers)

**Your goal:** Player sees immediate feedback on whether they got it right.

---

### Step 5: Add a Timer

**What to do:**
1. Start a timer when the math problem appears
2. Display the timer on screen (counting up or down, your choice)
3. Stop the timer when the player submits
4. Store the elapsed time for damage calculation

**Timer display options:**
- Count up from 0 (shows how long they took)
- Count down from 10 (adds pressure, auto-fails if time runs out)
- Hidden timer (less stressful, calculate damage secretly)

**Recommendation:** Start with a visible count-up timer. Add countdown/pressure mechanics later if desired.

**Your goal:** You know exactly how many seconds it took the player to answer.

---

### Step 6: Deal Damage on Correct Answer

**What to do:**
1. When player answers correctly, reduce enemy HP
2. Base damage = some fixed amount (e.g., 10)
3. Faster answers = more damage (implement your time-to-damage formula)

**Simple time-to-damage formula:**
```
If answered in under 2 seconds: damage = base × 2.0 (Perfect!)
If answered in under 4 seconds: damage = base × 1.5 (Great!)  
If answered in under 6 seconds: damage = base × 1.0 (Good)
If answered in under 10 seconds: damage = base × 0.75 (Slow)
If answered in 10+ seconds: damage = base × 0.5 (Very slow)
```

**Your goal:** Enemy HP goes down when you answer correctly. Faster = more damage.

---

### Step 7: Handle Wrong Answers

**What to do:**
1. Decide the penalty for wrong answers
2. Options: enemy gets free attack, lose your turn, take direct damage, or no penalty (just try again)

**Penalty options and their effects:**

| Penalty | Feels Like | Best For |
|---------|-----------|----------|
| Enemy attacks back | Punishing but fair | Older players, hard mode |
| Lose turn (no damage dealt) | Frustrating | Not recommended |
| Take direct damage | Very punishing | Expert mode only |
| No penalty, try again | Forgiving | Young players, learning mode |
| Show correct answer, move on | Educational | Tutoring focus |

**Recommendation:** Start with "enemy gets a free attack" — it's punishing enough to matter but doesn't feel unfair.

**Your goal:** Wrong answers have consequences.

---

### Step 8: Let the Enemy Fight Back

**What to do:**
1. After the player's turn, the enemy attacks
2. Reduce player HP by enemy's attack value
3. Show feedback ("Enemy attacks! You take 8 damage!")

**Turn structure options:**
- **Turn-based:** Player attacks → Enemy attacks → Repeat
- **Real-time:** Enemy attacks on a timer regardless of player actions
- **Conditional:** Enemy only attacks if player gets answer wrong

**Recommendation:** Start with simple turn-based. Add real-time pressure later if desired.

**Your goal:** Player HP goes down when enemy attacks.

---

### Step 9: Add Win Condition

**What to do:**
1. Check if enemy HP ≤ 0 after each attack
2. If yes, show "Victory!" screen
3. Stop the battle (disable input, show results)

**Victory screen should show:**
- "You Win!"
- Total time taken
- Number of problems solved
- Accuracy percentage (correct / total attempts)

**Your goal:** Battle ends when enemy dies.

---

### Step 10: Add Lose Condition

**What to do:**
1. Check if player HP ≤ 0 after enemy attacks
2. If yes, show "Defeat!" screen
3. Stop the battle

**Defeat screen should show:**
- "Game Over" (or less harsh: "Try Again?")
- Option to retry the battle
- Stats from the attempt (optional)

**Your goal:** Battle ends when player dies.

---

## Testing Your Prototype

Once all 10 steps are done, playtest it yourself:

**Questions to ask:**
1. Is it fun? Or tedious?
2. Is the difficulty right? (Too easy = boring, too hard = frustrating)
3. Does the timer add excitement or stress?
4. Is the feedback clear? Do I always know what's happening?
5. Would I want to play this again?

**Red flags that need fixing:**
- You're bored before the battle ends
- You can win without thinking
- You feel cheated when you lose
- You're confused about what to do next
- The math problems are too easy or too hard

---

## Common Pitfalls

**Pitfall 1: Making it too pretty too soon**
You'll want to add sprites. Resist. The ugly prototype tells you if the idea works.

**Pitfall 2: Overcomplicating the math generation**
Start with addition only. Add other operations once that works.

**Pitfall 3: Not playtesting enough**
Play your prototype 20+ times before moving on. You'll find issues.

**Pitfall 4: Hardcoding everything**
Use variables for damage, HP, timer thresholds. You'll be tweaking these constantly.

**Pitfall 5: Ignoring wrong answer handling**
Wrong answers are where frustration lives. Get this right early.

---

## Time Estimate for Phase 2

| Task | Time |
|------|------|
| Create battle scene with rectangles | 30-60 min |
| Display math problems | 1-2 hours |
| Add input and answer checking | 1-2 hours |
| Implement timer | 30-60 min |
| Damage calculation | 1-2 hours |
| Enemy attacks | 30-60 min |
| Win/lose conditions | 1-2 hours |
| Testing and bug fixing | 2-4 hours |
| **Total** | **8-15 hours** |

---

## Phase 2 Checklist

- [ ] Battle scene exists with player and enemy rectangles
- [ ] HP displays for both player and enemy
- [ ] Random math problems appear on screen
- [ ] Player can input answers (text field or buttons)
- [ ] Correct/incorrect feedback is shown
- [ ] Timer tracks how long player takes
- [ ] Correct answers deal damage (faster = more damage)
- [ ] Wrong answers have consequences
- [ ] Enemy attacks the player
- [ ] Battle ends when enemy HP hits 0 (victory)
- [ ] Battle ends when player HP hits 0 (defeat)
- [ ] Playtested at least 20 times
- [ ] Core loop feels fun (or at least not broken)

---

## What You Should Have Now

A hideous but functional battle prototype. You press a button, a math problem appears, you answer it, and either you or the enemy takes damage. Eventually someone wins.

If this is fun with rectangles, it'll be amazing with polish.

---

## Next Up

**Phase 3: Design Your Numbers** — You'll figure out all the formulas, balance the difficulty curve, and create a spreadsheet so you can tweak values without changing code.
