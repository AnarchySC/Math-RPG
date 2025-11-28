# Phase 7: Art Pass

## Overview

Your game works. Now it needs to look like a game. This phase replaces programmer rectangles with actual graphics — sprites, tiles, UI elements, and visual polish.

**Important:** You don't need to be an artist. Free assets, simple pixel art, and clean UI design can make your game look great.

---

## Art Style Decision

### Pixel Art (Recommended)

**Why pixel art?**
- Forgiving for beginners
- Small file sizes
- Classic RPG aesthetic
- Huge free asset libraries
- Quick to iterate

**Resolution suggestion:** 16×16 or 32×32 pixels per tile

### Other Options

**Hand-drawn:** Unique but time-intensive
**Vector:** Clean and scalable, less RPG-feeling
**3D rendered to 2D:** Complex pipeline, skip this
**Purchased assets:** Fast but costs money

---

## Asset Checklist

### What You Need

**Characters:**
- [ ] Player sprite (idle, walk cycle optional)
- [ ] Enemy sprites (one per enemy type)
- [ ] NPC sprites (shop keeper, villagers)
- [ ] Boss sprite (should look special)

**Tiles:**
- [ ] Grass/ground tiles
- [ ] Path tiles
- [ ] Wall tiles
- [ ] Water tiles (if used)
- [ ] Dungeon floor tiles
- [ ] Dungeon wall tiles

**Objects:**
- [ ] Treasure chest (closed and open)
- [ ] Doors
- [ ] Stairs
- [ ] Save point / healing point
- [ ] Shop sign

**UI Elements:**
- [ ] Health bar
- [ ] Mana bar
- [ ] Menu buttons
- [ ] Dialogue box
- [ ] Battle UI frame

**Icons:**
- [ ] Potion icons (each type)
- [ ] Buff icons (attack, defense)
- [ ] Gold/coin icon
- [ ] Attack icon
- [ ] Defend icon

---

## Free Asset Sources

### Recommended Sites

**itch.io (Best for pixel art)**
- Search "RPG tileset"
- Many free packs with CC0 or attribution license
- Quality varies; preview carefully

**OpenGameArt.org**
- Large library
- Check licenses carefully (some require attribution)

**Kenney.nl**
- High quality, CC0 license (no attribution required)
- More modern style than classic pixel

**Game-icons.net**
- Thousands of free icons
- Great for UI and item icons
- CC BY 3.0 (credit required)

### License Types to Look For

| License | What It Means |
|---------|---------------|
| CC0 / Public Domain | Use however you want, no credit needed |
| CC BY | Must credit the creator |
| CC BY-SA | Must credit AND share your game under same license |
| CC BY-NC | Non-commercial only |

**Recommendation:** Stick to CC0 or CC BY to keep things simple.

---

## Creating Your Own Art

### If You Want to Draw

**Tools:**
- **Aseprite** ($20, best pixel art tool)
- **GIMP** (free, powerful but complex)
- **Piskel** (free, browser-based, beginner-friendly)
- **Pixilart** (free, browser-based)

### Pixel Art Basics

**Start with silhouette:** Can you recognize the shape with just black and white?

**Limited palette:** Use 4-8 colors max. Fewer colors = more cohesive look.

**Suggested starter palette:**
```
Background: #1a1c2c (dark blue-gray)
Primary: #5d275d (purple) or #b13e53 (red)
Secondary: #38b764 (green) or #257179 (teal)
Highlight: #f4f4f4 (off-white)
Shadow: #333c57 (dark gray)
Skin: #e8b796 or #c49c82
```

**Simple character recipe:**
1. Draw 16×16 square
2. Head in top half (8×8)
3. Body in bottom half
4. 2 pixels for eyes
5. Hair/hat on top
6. Done. You have a character.

### Walk Cycle (Optional)

A 2-frame walk cycle is enough:
- Frame 1: Left foot forward
- Frame 2: Right foot forward

Alternate between frames while moving. Looks surprisingly good.

---

## Implementing Art in Your Game

### Replacing Player Rectangle

**Before:** ColorRect or placeholder sprite

**After:**
1. Import your player sprite image
2. Create Sprite/Image node
3. Assign texture
4. Adjust size/scale if needed
5. Position at player coordinates

**Code change:**
```
// Before
draw_rectangle(player.x, player.y, 32, 32, BLUE)

// After  
draw_sprite(playerSprite, player.x, player.y)
```

### Setting Up Tilemap Graphics

**Process:**
1. Create tileset image (all tiles in one file, grid layout)
2. Import into engine's tilemap system
3. Define which tiles are walkable
4. Paint your maps

**Tileset layout example:**
```
+---+---+---+---+
| G | P | W | F |   G = Grass
+---+---+---+---+   P = Path
| D | S | C | T |   W = Wall (exterior)
+---+---+---+---+   F = Floor (dungeon)
| W1| W2| W3| W4|   D = Door
+---+---+---+---+   S = Stairs
                    C = Chest
                    T = Tree
                    W1-4 = Wall variations
```

### Battle UI Design

**Key principles:**
- Information hierarchy (HP most prominent)
- Readable fonts (not too small)
- Contrast between text and background
- Consistent color scheme

**Battle screen layout:**
```
+----------------------------------------+
| [Player Area]              [Enemy Area]|
|  +-----------+            +-----------+|
|  | Sprite    |            | Sprite    ||
|  +-----------+            +-----------+|
|  HP: ████████░░           HP: ██████░░ |
|  MP: ██████░░░░                        |
|  [ATK+5 2T]                            |
+----------------------------------------+
|                                        |
|              17 × 8 = ?                |
|                                        |
|            [___________]               |
|            [  SUBMIT  ]                |
|                                        |
|            Timer: 2.4s                 |
|                                        |
+----------------------------------------+
|  [Potions ▼]              [Run]        |
+----------------------------------------+
```

---

## UI Design Guidelines

### Fonts

**Pixel fonts for pixel art games:**
- Match the aesthetic
- Free options: Press Start 2P, Silkscreen, VT323

**Where to find:**
- Google Fonts (filter by "pixel")
- dafont.com (check licenses)
- fontsquirrel.com

### Color Scheme

**Pick 3-5 colors for UI:**
- Background color
- Primary color (buttons, highlights)
- Text color
- Accent color (warnings, important info)

**Example scheme:**
```
UI Background: #2c3e50 (dark blue)
Panels: #34495e (slightly lighter)
Text: #ecf0f1 (off-white)
Health: #e74c3c (red)
Mana: #3498db (blue)
Gold: #f1c40f (yellow)
Buttons: #27ae60 (green)
```

### Consistency

- Same button style everywhere
- Same font sizes (Title > Header > Body > Small)
- Same spacing/margins
- Same corner rounding (all sharp OR all rounded)

---

## Attack Effects and Animations

### Simple Effects That Work

**Screen shake:** Move camera 2-4 pixels randomly for 0.1-0.2 seconds

**Flash:** Tint the enemy sprite white for 0.1 seconds when hit

**Number popup:** Show damage number that floats up and fades

**Implementation:**
```
function onEnemyHit(damage):
    shakeScreen(intensity=3, duration=0.15)
    flashSprite(enemySprite, WHITE, 0.1)
    spawnDamageNumber(damage, enemy.position)
```

### Damage Number Animation

```
function spawnDamageNumber(amount, position):
    number = createText(amount)
    number.position = position
    number.color = RED
    
    // Animate: float up, fade out
    tween(number.position.y, position.y - 50, 1.0 seconds)
    tween(number.alpha, 0, 1.0 seconds)
    
    after(1.0 seconds):
        destroy(number)
```

### Particle Effects (Optional)

- Sparkles on perfect answer
- Dust when walking
- Magic particles on buff activation

Keep particles simple. A few squares moving randomly = "magic sparkles."

---

## Creating Enemy Sprites

### Enemy Design Tips

**Silhouette first:** Each enemy should be recognizable by shape alone

**Color coding:** 
- Green = weak
- Blue = medium  
- Red = strong
- Purple/black = boss

**Size indicates threat:** Bigger enemies look more dangerous

### Simple Enemy Types

**Slime:** Blob shape, single color, maybe eyes
**Rat:** Small, horizontal oval, tail, ears
**Skeleton:** White, stick figure-ish, skull head
**Goblin:** Green, small, pointed ears
**Orc:** Large, green, muscular
**Boss:** 2x size of normal enemy, unique colors

---

## Polish Details

### Small Things That Matter

**Smooth movement:** Don't teleport between tiles, slide smoothly

**Button feedback:** Buttons change color/scale when hovered or clicked

**Transitions:** Fade between maps instead of instant switch

**Loading indicator:** Show something while loading (even if it's fast)

**Menu sounds:** Click sounds for UI (covered in Phase 8)

### Visual Juice Checklist

- [ ] Screen shake on hit
- [ ] Enemy flash when damaged
- [ ] Damage numbers popup
- [ ] Health bar smoothly animates (doesn't jump)
- [ ] Buff icons pulse or glow
- [ ] Perfect answer gets special effect
- [ ] Victory screen has fanfare feel

---

## Iteration Process

### Don't Perfectionist

1. Get placeholder graphics in
2. Play the game
3. Note what looks worst
4. Fix that one thing
5. Repeat

**Progress > Perfection.** Ship with "good enough" art. You can always update later.

### Getting Feedback

Show screenshots to friends/family:
- "What do you notice first?"
- "Anything confusing?"
- "Does it look like an RPG?"

Don't ask "do you like it?" — too vague.

---

## Time Estimate for Phase 7

| Task | Time |
|------|------|
| Decide art style | 1 hour |
| Source/create player sprite | 2-4 hours |
| Source/create enemy sprites | 3-5 hours |
| Source/create NPC sprites | 1-2 hours |
| Source/create tileset | 3-5 hours |
| Implement tiles in maps | 2-4 hours |
| Design battle UI | 2-3 hours |
| Implement battle UI | 2-4 hours |
| Create menu UI | 2-3 hours |
| Potion and buff icons | 1-2 hours |
| Add visual effects (shake, flash) | 2-3 hours |
| Title screen | 1-2 hours |
| Testing and polish | 2-4 hours |
| **Total** | **24-42 hours** |

---

## Phase 7 Checklist

- [ ] Art style chosen
- [ ] Player sprite replaces rectangle
- [ ] Player has walk animation (even if 2 frames)
- [ ] All enemy types have sprites
- [ ] NPC sprites created/sourced
- [ ] Tileset created for overworld
- [ ] Tileset created for dungeon
- [ ] All maps updated with tiles
- [ ] Treasure chests have sprites
- [ ] Battle UI designed and implemented
- [ ] Health bars look good
- [ ] Mana bar displayed
- [ ] Buff icons visible
- [ ] Potion icons in inventory
- [ ] Screen shake on damage
- [ ] Flash effect on hit
- [ ] Damage numbers popup
- [ ] Font chosen and implemented
- [ ] Color scheme consistent
- [ ] Title screen exists
- [ ] Full game playthrough looks cohesive

---

## What You Should Have Now

A game that LOOKS like a game. Same mechanics as before, but now with real graphics. People could see a screenshot and think "that's an RPG."

Still no sound though. That's next.

---

## Next Up

**Phase 8: Sound and Music** — Audio transforms a game from "project" to "experience."
