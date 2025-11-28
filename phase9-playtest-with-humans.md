# Phase 9: Playtest With Real Humans

## Overview

You've been testing your own game for weeks. You know every shortcut, every quirk, every solution. You are the worst person to test your game.

Real playtesting means watching someone who has NEVER seen your game try to play it. It's humbling, frustrating, and absolutely essential.

---

## Why Playtesting Matters

**You can't see your own blind spots.**

Things obvious to you are invisible to new players:
- "How was I supposed to know to press E?"
- "I didn't realize that was a button."
- "Why did I just die? What happened?"

**Real players will:**
- Ignore your tutorial
- Miss obvious UI elements
- Try things you never imagined
- Get stuck on things you thought were trivial
- Find bugs you can't reproduce

**This is all valuable data.** Every point of confusion is an opportunity to improve.

---

## Recruiting Playtesters

### Who to Ask

**Good playtesters:**
- Friends and family (easiest to recruit)
- Coworkers (if comfortable)
- Online communities (Reddit, Discord, itch.io)
- Kids in your target age range (if appropriate)

**Ideal mix:**
- Some who play games regularly
- Some who rarely play games
- Different ages if possible
- Different math comfort levels

### How Many Testers

**Minimum:** 3-5 people

**Sweet spot:** 5-10 people

**Diminishing returns after:** ~15 people for early testing

You don't need 100 testers. You need 5 fresh perspectives.

### What to Tell Them

**DO say:**
- "I'm making a game and need feedback"
- "I want to see where people get confused"
- "It's not finished, so don't worry about rough edges"
- "Be honest — criticism helps me improve"

**DON'T say:**
- "Here's how to play..." (let them figure it out)
- "This part is buggy, so ignore that..."
- "You're supposed to go left first..."

---

## The Playtest Session

### Before They Start

**Setup:**
1. Game fully restarts from beginning
2. No special debug modes
3. Clear any save files
4. If possible, record their screen
5. Have paper ready for notes

**Your mindset:**
- You are an observer, not a helper
- Their confusion is data
- Don't defend your choices
- Listen more than talk

### During Gameplay

**The Golden Rule: SHUT YOUR MOUTH**

The most valuable data comes from watching them struggle. The moment you say "click the blue button," you've lost information about whether your UI is clear.

**What to do:**
- Take notes on everything they do
- Note where they pause or hesitate
- Note what they try that doesn't work
- Note any verbal reactions ("huh?", "oh!", "what?")

**What NOT to do:**
- Explain mechanics
- Point out things they missed
- Apologize for bugs
- Tell them what to do next

**Only interrupt if:**
- They're completely stuck for 3+ minutes
- They ask a direct question (answer minimally)
- They want to quit
- There's a game-breaking bug

### After They Finish

**Ask open-ended questions:**
- "What did you think overall?"
- "Was anything confusing?"
- "What was the most frustrating part?"
- "What was the most fun part?"
- "Would you play more?"

**Ask specific questions:**
- "Did you understand what the potions do?"
- "Did you realize you could [specific mechanic]?"
- "How did the math difficulty feel?"

**Don't ask:**
- "Did you like it?" (too vague, too easy to please you)
- "Should I change X to Y?" (don't lead them)

---

## What to Observe

### Red Flags to Watch For

**UI/UX Issues:**
- Clicking wrong things
- Not noticing important information
- Asking "what do I do now?"
- Looking at wrong part of screen

**Gameplay Issues:**
- Dying repeatedly to same thing
- Ignoring key mechanics
- Finding exploits/cheese strategies
- Getting bored before finishing

**Math Difficulty:**
- Taking too long on "easy" problems
- Breezing through "hard" problems
- Consistently failing one operation type
- Frustration during problem-solving

**Pacing Issues:**
- Rushing through dialogue
- Grinding in wrong areas
- Quitting before boss
- Finishing too quickly or slowly

### Your Notes Template

```
Playtester: [Name/ID]
Date: 
Time to complete: 

OBSERVATIONS:
[Timestamp] What happened

0:00 Started game
0:30 Didn't notice "Attack" button, clicked randomly
1:15 Got first problem wrong, seemed confused
2:00 Asked "do I click or type the answer?"
...

QUOTES:
- "Wait, what does mana do?"
- "Oh, I didn't see that chest"
- "This multiplication is hard"

POST-GAME ANSWERS:
Overall impression:
Most confusing part:
Most fun part:
Frustrations:
Would play more?
```

---

## Analyzing Feedback

### Look for Patterns

One person confused? Maybe they're unusual.
Three people confused? You have a design problem.

**Compile observations:**
```
Issue: Players don't understand potion effects
- Tester 1: "What do potions do?"
- Tester 2: Used wrong potion type repeatedly
- Tester 4: Never used potions at all
- Tester 5: "I thought they were healing potions"

Conclusion: Potion system needs better explanation
Priority: HIGH
```

### Categorize Issues

**Critical (Fix before next test):**
- Game crashes
- Softlocks (can't progress)
- Core confusion about main mechanic

**High (Fix soon):**
- Consistent confusion points
- Frustration-causing design
- Missed features everyone ignores

**Medium (Fix eventually):**
- Minor UI improvements
- Balance tweaks
- "Nice to have" suggestions

**Low (Maybe later):**
- Personal preferences
- Feature requests for future
- Edge cases

### Feedback ≠ Solutions

Players are great at identifying problems.
Players are usually bad at designing solutions.

**If player says:** "You should add a tutorial popup"
**What they mean:** "I was confused at the start"
**Real solution:** Could be tutorial, OR better UI, OR different starting sequence

Listen to the problem, not the prescription.

---

## Common Playtest Discoveries

### Almost Every Game Has These Issues

**No one reads tutorials**
- They click through
- They skip text
- They learn by doing

**Players don't see what you see**
- Important button ignored
- Key info overlooked
- "Obvious" path missed

**First 30 seconds are critical**
- Confusion here = bad first impression
- Early frustration = quitting

**Players find unintended strategies**
- "I just spammed addition to heal constantly"
- "I ran from every fight"
- "I never used potions because I forgot"

---

## Making Changes

### The Iteration Cycle

```
Playtest → Identify Issues → Prioritize → Fix Top Issues → Playtest Again
```

**Don't fix everything at once.**
Fix the top 3-5 issues, then test again with NEW people.

**New testers see fresh problems.**
Old testers remember solutions. They're contaminated.

### How Many Rounds?

**Minimum:** 2 rounds of testing
**Recommended:** 3-5 rounds
**Until:** New players can enjoy without guidance

### When to Stop

Stop playtesting when:
- New players understand mechanics without help
- No one gets stuck at the same spot
- Feedback shifts from "confused" to "suggestions"
- You're making smaller and smaller changes

---

## Remote Playtesting

### If You Can't Watch In Person

**Option 1: Screen share call**
- Discord, Zoom, etc.
- Ask them to "think aloud"
- You watch live, take notes
- Can see their face reactions

**Option 2: Recorded video**
- They record screen while playing
- They talk through their thoughts
- You watch later
- Loses some immediacy but works

**Option 3: Written feedback**
- Send them the game
- They play and write notes
- Least useful method
- Better than nothing

**Option 4: Survey**
- Play game, then answer questions
- Good for specific questions
- Bad for discovering unknowns

### Tools for Recording

- OBS Studio (free, screen recording)
- Built-in OS recording (Windows Game Bar, Mac)
- Loom (browser extension, easy sharing)

---

## Feedback From Different Groups

### Non-Gamers

**Valuable for:**
- Clarity of instructions
- Intuitive UI
- Overall accessibility

**Expect:**
- More confusion
- Longer time to understand
- Different assumptions about controls

### Kids (If Target Audience)

**Valuable for:**
- Math difficulty calibration
- Fun factor
- Engagement level

**Expect:**
- Shorter attention span
- Less filter in feedback
- Unexpected approaches

### Experienced Gamers

**Valuable for:**
- Comparison to similar games
- Balance feedback
- Quality expectations

**Expect:**
- Higher standards
- More specific feedback
- May rush through content

---

## Time Estimate for Phase 9

| Task | Time |
|------|------|
| Recruit 3-5 testers | 1-2 days |
| First round playtests | 3-5 hours |
| Analyze round 1 feedback | 2-3 hours |
| Fix top issues | 4-8 hours |
| Recruit new testers | 1-2 days |
| Second round playtests | 3-5 hours |
| Analyze round 2 feedback | 2-3 hours |
| Fix remaining issues | 4-8 hours |
| (Optional) Third round | 4-6 hours |
| **Total** | **~1-3 weeks** |

---

## Phase 9 Checklist

**Round 1:**
- [ ] Recruited 3-5 testers
- [ ] Watched each playtest without helping
- [ ] Took notes during sessions
- [ ] Asked follow-up questions
- [ ] Compiled observations
- [ ] Identified top 3-5 issues
- [ ] Fixed critical issues

**Round 2:**
- [ ] Recruited NEW testers
- [ ] Watched playtests
- [ ] Noted if issues from round 1 are resolved
- [ ] Identified any new issues
- [ ] Made fixes

**Completion Criteria:**
- [ ] New players can play without getting stuck
- [ ] Core mechanics are understood
- [ ] No consistent confusion points
- [ ] Game is fun (players say they'd play more)
- [ ] Math difficulty feels appropriate

---

## What You Should Have Now

A game that real humans can pick up and play without you holding their hand. Confusing parts have been smoothed out. The experience flows.

This is the version you can release.

---

## Next Up

**Phase 10: Polish and Ship** — Final bug fixes, menus, and getting your game into players' hands.
