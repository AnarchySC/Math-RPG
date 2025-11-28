# Phase 1: Pick Your Engine

## Overview

Before writing a single line of code, you need to choose your development environment. This decision affects everything from how you structure your project to what resources are available when you get stuck.

**Don't overthink this.** Any modern engine can build your Math RPG. The best engine is the one you'll actually use.

---

## The Three Main Options

### Option A: Godot (Recommended for Beginners)

**What it is:** A free, open-source game engine with excellent 2D support.

**Pros:**
- Completely free, no strings attached
- Lightweight (under 100MB download)
- GDScript is beginner-friendly (similar to Python)
- Built specifically with 2D games in mind
- Huge community creating free tutorials

**Cons:**
- Smaller job market than Unity
- Fewer third-party assets available
- Less name recognition

**Best for:** Hobbyists, indie developers, anyone who wants to start making games fast without cost.

---

### Option B: Unity

**What it is:** Industry-standard game engine used by professionals and hobbyists alike.

**Pros:**
- Massive asset store with pre-built components
- Skills transfer directly to game industry jobs
- Enormous community and tutorial library
- C# is a widely-used programming language

**Cons:**
- Steeper learning curve
- More complex than necessary for 2D games
- Recent pricing controversies have shaken trust
- Can feel bloated for simple projects

**Best for:** People who want game development careers, or who already know C#.

---

### Option C: RPG Maker

**What it is:** Specialized tool for creating classic JRPG-style games.

**Pros:**
- Fastest path to a working RPG
- Minimal coding required (event-based system)
- Built-in battle systems, menus, and inventory
- Assets included out of the box

**Cons:**
- Less flexible — fighting the engine for custom mechanics
- Games can look "RPG Maker-y" without custom assets
- Limited to RPG genre
- Costs money ($25-80 depending on version)

**Best for:** People who want to focus on game design over programming, or who specifically want a classic JRPG look.

---

## How to Decide

Ask yourself these questions:

**"Do I want to learn programming?"**
- Yes → Godot or Unity
- Not really → RPG Maker

**"Is budget a concern?"**
- Yes → Godot (free forever)
- No → Any option works

**"Do I want a career in games?"**
- Yes → Unity (industry standard)
- No/Unsure → Godot

**"Do I just want to make THIS game as fast as possible?"**
- Yes → RPG Maker

---

## Your Action Items

### Step 1: Watch One "First Game" Tutorial for Each Engine (1 hour total)

Don't install anything yet. Just watch:

- **Godot:** Search "Godot 4 beginner tutorial" — watch the first 15-20 minutes
- **Unity:** Search "Unity 2D beginner tutorial" — watch the first 15-20 minutes  
- **RPG Maker:** Search "RPG Maker MZ tutorial" — watch the first 15-20 minutes

Pay attention to which one feels least intimidating.

### Step 2: Install Your Chosen Engine

**Godot:**
1. Go to godotengine.org
2. Download Godot 4.x (standard version, not .NET)
3. Unzip and run — no installer needed

**Unity:**
1. Go to unity.com
2. Download Unity Hub
3. Install the latest LTS (Long Term Support) version
4. Select "2D" template when creating projects

**RPG Maker:**
1. Purchase from Steam or rpgmakerweb.com
2. RPG Maker MZ is the latest version
3. Install through Steam or standalone installer

### Step 3: Complete the Official Getting Started Tutorial

Every engine has official beginner docs:

- **Godot:** docs.godotengine.org → "Getting Started" → "Step by Step"
- **Unity:** learn.unity.com → "Pathways" → "Unity Essentials"
- **RPG Maker:** Built-in help menu + rpgmakerweb.com/support

Spend 1-2 hours here. Don't skip this.

### Step 4: Make a Character Move on Screen

Your "Hello World" for game development:

1. Create a new project
2. Add a sprite (a colored rectangle is fine)
3. Make it move with arrow keys or WASD
4. Celebrate — you're a game developer now

This should take 30-60 minutes with tutorial guidance.

### Step 5: Confirm Your Choice

After completing steps 1-4, ask yourself:
- Did I enjoy this, or was it painful?
- Can I see myself using this for months?
- Did I understand what I was doing?

If you're miserable, try a different engine. Better to switch now than 3 weeks in.

---

## Recommended: Godot for This Project

For the Math RPG specifically, **Godot is the best fit** because:

1. The math battle system requires custom code — Godot makes this easy
2. You don't need Unity's 3D power or asset store
3. RPG Maker would fight you on the custom combat mechanics
4. It's free, so no sunk cost if you abandon the project
5. GDScript is readable and beginner-friendly

That said, if you already know C# or Unity, stick with what you know.

---

## Common Mistakes to Avoid

**Mistake 1: Spending weeks "researching" engines**
Analysis paralysis is real. Pick one and start. You can always switch later (your design skills transfer).

**Mistake 2: Picking based on what big studios use**
AAA studios use custom engines or heavily modified Unity/Unreal. What works for a 200-person team doesn't matter for a solo project.

**Mistake 3: Buying expensive assets before learning the basics**
You don't need a $50 sprite pack yet. Use colored rectangles until your mechanics work.

**Mistake 4: Trying to learn multiple engines simultaneously**
Master one. Dabbling in three engines means you're mediocre at all three.

---

## Time Estimate for Phase 1

| Task | Time |
|------|------|
| Watch comparison tutorials | 1 hour |
| Install engine | 15-30 minutes |
| Complete getting started guide | 1-2 hours |
| Make character move | 30-60 minutes |
| **Total** | **3-4 hours** |

---

## Phase 1 Checklist

- [ ] Watched introductory tutorial for at least 2 engines
- [ ] Made a decision (and committed to it)
- [ ] Installed chosen engine
- [ ] Completed official getting started tutorial
- [ ] Created a project where a character moves with keyboard input
- [ ] Confirmed this engine feels right for you

---

## Next Up

Once you can move a character around a screen, you're ready for **Phase 2: Make It Playable Ugly First** — where you'll build the core math-battle system with placeholder graphics.
