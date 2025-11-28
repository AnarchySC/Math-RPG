# Phase 6: Create the World

## Overview

You have combat. You have progression. Now you need a world to explore. This phase adds maps, movement, NPCs, and multiple enemies — transforming isolated battles into a real adventure.

Start small. One village, one dungeon, one boss. Expand later.

---

## World Design Philosophy

**Rule 1: Tiny but Complete**
A 3-room dungeon players can finish is better than a 50-room dungeon you'll never complete.

**Rule 2: Every Screen Has Purpose**
If a location doesn't teach, reward, or challenge, cut it.

**Rule 3: Guide Through Design**
Players should know where to go without explicit instructions. Use visual cues, NPC hints, and blocked paths.

---

## Your First World Map

### Minimum Viable World

```
[Village]
    │
    ▼
[Forest Path] ← Weak enemies
    │
    ▼
[Dungeon Entrance]
    │
    ▼
[Dungeon Floor 1] ← Medium enemies
    │
    ▼
[Dungeon Floor 2] ← Harder enemies
    │
    ▼
[Boss Room] ← BOSS
```

That's 6 locations. That's enough for a complete game arc.

### Location Details

**Village (Safe Zone)**
- No enemies
- NPCs: Shop owner, hint-giver, maybe a "save point" character
- Player starts here after battles
- Feels like home

**Forest Path (Tutorial Zone)**
- Weak enemies (slimes, level 1-2)
- Teaches combat without high stakes
- Maybe 1-2 treasure chests
- Leads to dungeon

**Dungeon Entrance (Transition)**
- Visual shift from outdoors to indoors
- Last chance to return to village
- Maybe a warning sign NPC

**Dungeon Floor 1**
- Medium enemies (level 3-4)
- Some exploration required
- Health restore point (fountain? crystal?)
- Treasure with potions or gold

**Dungeon Floor 2**
- Harder enemies (level 5-6)
- More complex layout
- Key item or switch puzzle (optional)
- Build tension before boss

**Boss Room**
- Dramatic entrance
- Boss enemy (special mechanics?)
- Victory = game complete (for now)

---

## Implementing Tile-Based Movement

### What is Tile-Based Movement?

The map is a grid. Player occupies one tile. Arrow keys move one tile at a time.

```
+---+---+---+---+---+
|   |   | P |   |   |   P = Player
+---+---+---+---+---+   W = Wall
| W | W |   | W | W |   T = Treasure
+---+---+---+---+---+   E = Enemy
|   |   |   |   | T |
+---+---+---+---+---+
| E |   | W |   |   |
+---+---+---+---+---+
```

### Implementation Steps

**Step 1: Create a Tilemap**

Most engines have tilemap support:
- **Godot:** TileMap node
- **Unity:** Tilemap component
- **RPG Maker:** Built-in map editor

**Step 2: Define Tile Types**

| Tile Type | Walkable | Effect |
|-----------|----------|--------|
| Floor | Yes | None |
| Wall | No | Blocks movement |
| Water | No (usually) | Blocks unless special item |
| Treasure | Yes | Opens chest when stepped on |
| Door | Conditional | Opens if unlocked |
| Stairs | Yes | Transitions to another map |
| Enemy Spawn | Yes | May trigger encounter |

**Step 3: Handle Input**

```
function handleInput():
    newPosition = currentPosition
    
    if keyPressed(UP):
        newPosition.y -= 1
    elif keyPressed(DOWN):
        newPosition.y += 1
    elif keyPressed(LEFT):
        newPosition.x -= 1
    elif keyPressed(RIGHT):
        newPosition.x += 1
    
    if isWalkable(newPosition):
        currentPosition = newPosition
        checkTileEvents(currentPosition)
```

**Step 4: Check Tile Events**

```
function checkTileEvents(position):
    tile = getTileAt(position)
    
    if tile.type == "treasure" and not tile.opened:
        openTreasure(tile)
    elif tile.type == "stairs":
        transitionToMap(tile.destination)
    elif tile.type == "enemy_spawn":
        maybeStartBattle()
```

---

## Collision Detection

### Blocking Walls and Objects

Before moving the player, check if destination is valid:

```
function isWalkable(position):
    // Check bounds
    if position.x < 0 or position.x >= mapWidth:
        return false
    if position.y < 0 or position.y >= mapHeight:
        return false
    
    // Check tile type
    tile = getTileAt(position)
    if tile.type == "wall" or tile.type == "water":
        return false
    
    // Check for blocking NPCs
    if npcAtPosition(position):
        return false
    
    return true
```

### Interacting with Objects

When player tries to walk into something interactable:

```
function tryMove(direction):
    targetPosition = currentPosition + direction
    
    if isWalkable(targetPosition):
        move(targetPosition)
    elif hasInteractable(targetPosition):
        interact(getObjectAt(targetPosition))
```

---

## Creating NPCs

### NPC Types

**Shop Keeper**
- Doesn't move
- Opens shop when interacted with

**Hint Giver**
- Doesn't move
- Displays dialogue when talked to

**Wandering NPC**
- Moves randomly
- Dialogue when talked to
- Blocks player movement

**Quest Giver** (optional for now)
- Gives quest, tracks completion
- Different dialogue based on quest state

### NPC Interaction

```
function interactWithNPC(npc):
    if npc.type == "shopkeeper":
        openShopUI()
    elif npc.type == "hint_giver":
        showDialogue(npc.dialogue)
    elif npc.type == "quest_giver":
        handleQuest(npc)
```

### Basic Dialogue System

**Dialogue data structure:**
```
npc.dialogue = [
    "Welcome, traveler!",
    "The dungeon to the north is dangerous.",
    "Stock up on potions before you go."
]
```

**Dialogue display:**
1. Show dialogue box at bottom of screen
2. Display first line
3. Player presses button → show next line
4. After last line → close dialogue

**Simple implementation:**
```
dialogueLines = npc.dialogue
currentLine = 0

function showNextLine():
    if currentLine < dialogueLines.length:
        displayText(dialogueLines[currentLine])
        currentLine += 1
    else:
        closeDialogue()
```

---

## Enemy Encounters

### Random Encounters vs. Visible Enemies

**Random Encounters:**
- Enemy not visible on map
- Each step has % chance to trigger battle
- Classic JRPG style

**Visible Enemies:**
- Enemy sprite on map
- Battle starts when you touch them
- Player can choose to engage or avoid

**Recommendation:** Start with visible enemies. Less frustrating, more strategic.

### Visible Enemy Implementation

**Enemy on map:**
```
enemy = {
    position: {x: 5, y: 3},
    enemyType: "slime",
    level: 2,
    movePattern: "random"  // or "chase", "patrol"
}
```

**Collision triggers battle:**
```
function checkEnemyCollision():
    for enemy in currentMap.enemies:
        if player.position == enemy.position:
            startBattle(enemy.enemyType, enemy.level)
            removeEnemyFromMap(enemy)
```

### Enemy Movement Patterns

**Stationary:** Enemy doesn't move

**Random:** Every few seconds, move in random direction
```
function randomMove(enemy):
    direction = randomChoice([UP, DOWN, LEFT, RIGHT])
    if isWalkable(enemy.position + direction):
        enemy.position += direction
```

**Chase:** Move toward player
```
function chasePlayer(enemy):
    if distance(enemy, player) < 5:  // Only chase if close
        direction = directionToward(player)
        if isWalkable(enemy.position + direction):
            enemy.position += direction
```

**Patrol:** Move back and forth along set path

---

## Map Transitions

### Transitioning Between Maps

**Trigger:** Player steps on stairs, door, or map edge

**Process:**
1. Save any map state (opened chests, defeated enemies)
2. Load new map data
3. Place player at entry point
4. Display new map

**Implementation:**
```
function transitionToMap(newMapId, entryPoint):
    saveCurrentMapState()
    
    currentMap = loadMap(newMapId)
    player.position = entryPoint
    
    loadMapState(newMapId)  // Restore chests, enemies
    
    fadeIn()  // Visual transition
```

### Preserving Map State

When player leaves and returns:
- Opened chests stay opened
- Defeated enemies stay gone (or respawn? your choice)
- NPCs reset to default positions

```
mapStates = {
    "forest": {
        treasures: {
            "chest_1": opened,
            "chest_2": closed
        },
        enemiesDefeated: ["enemy_1", "enemy_3"]
    }
}
```

---

## Enemy Roster

### Creating Multiple Enemy Types

| Enemy | Location | Level | HP | Attack | Gold | XP |
|-------|----------|-------|----|----|------|-----|
| Slime | Forest | 1 | 30 | 5 | 8 | 15 |
| Rat | Forest | 2 | 40 | 7 | 10 | 20 |
| Goblin | Dungeon 1 | 3 | 60 | 10 | 15 | 35 |
| Skeleton | Dungeon 1 | 4 | 75 | 12 | 20 | 45 |
| Orc | Dungeon 2 | 5 | 100 | 15 | 30 | 60 |
| Ghost | Dungeon 2 | 6 | 80 | 18 | 35 | 70 |
| BOSS: Dark Knight | Boss Room | 8 | 250 | 22 | 200 | 500 |

### Enemy Variety Ideas

**Different enemies could have:**
- Higher attack but lower HP (glass cannon)
- High defense, low attack (tank)
- Attacks that cause status effects (not implemented yet)
- Weakness to certain math types (advanced mechanic)

---

## Simple Dungeon Design

### Dungeon Floor 1 Layout Example

```
+---+---+---+---+---+---+---+
| E |   |   | W | T |   | E |   Entrance at bottom
+---+---+---+---+---+---+---+   Stairs at top
|   | W | W | W |   | W |   |
+---+---+---+---+---+---+---+   E = Enemy
|   |   |   |   |   |   |   |   T = Treasure
+---+---+---+---+---+---+---+   W = Wall
|   | W |   | W | W |   | W |   S = Stairs up
+---+---+---+---+---+---+---+   H = Heal point
| H |   |   |   |   |   | S |
+---+---+---+---+---+---+---+
|   | W | W | W | W |   |   |
+---+---+---+---+---+---+---+
|   |   |   | ▲ |   |   |   |   ▲ = Entrance from outside
+---+---+---+---+---+---+---+
```

### Dungeon Design Principles

1. **Multiple paths** — Let player choose route
2. **Treasure off main path** — Reward exploration
3. **Healing before boss** — Don't punish with attrition
4. **Increasing difficulty** — Deeper = harder enemies
5. **Visual landmarks** — Help player navigate

---

## Boss Design

### What Makes a Boss Special?

**Higher stats:** More HP, more attack
**Unique mechanic:** Something regular enemies don't have
**Build-up:** The journey TO the boss is part of the experience
**Reward:** Major XP, gold, maybe story progression

### Boss Mechanic Ideas for Math RPG

**Math Focus Boss:** Only gives one type of math problem. Forces player to practice their weakness.

**Speed Boss:** Tighter time limits. Pressure mode.

**Multi-Phase Boss:** Changes behavior at 50% HP.

**Simple approach for first boss:** Just make it beefy. High HP, high attack, decent gold/XP. Save fancy mechanics for later bosses.

---

## Treasure System

### Treasure Chest Contents

**Random loot:**
```
treasurePool = [
    { type: "gold", amount: 20-50 },
    { type: "potion", item: "addition_potion", amount: 1-2 },
    { type: "potion", item: "health_potion", amount: 1-3 }
]
```

**Fixed loot:**
```
chest_5 = { contents: "large_health_potion", amount: 1 }
```

### Chest Interaction

```
function openChest(chest):
    if chest.opened:
        showMessage("Already opened.")
        return
    
    chest.opened = true
    contents = generateLoot(chest.lootTable)
    addToInventory(contents)
    showMessage("Found " + contents.description + "!")
```

---

## Goal State: Beating the Game

### Victory Condition

**Minimum:** Defeat the boss

**Victory sequence:**
1. Boss HP hits 0
2. Victory fanfare
3. "Congratulations!" screen
4. Show final stats
5. Credits (just your name is fine)
6. Return to title screen

**Post-game options:**
- New Game (start over)
- Continue (keep playing, enemies respawn?)
- "Thanks for playing!"

---

## Time Estimate for Phase 6

| Task | Time |
|------|------|
| Design world layout | 1-2 hours |
| Implement tilemap system | 2-4 hours |
| Tile-based movement | 2-3 hours |
| Collision detection | 1-2 hours |
| Create village map | 1-2 hours |
| Create dungeon maps | 3-5 hours |
| NPC implementation | 2-3 hours |
| Dialogue system | 2-3 hours |
| Enemy spawning on maps | 2-3 hours |
| Map transitions | 2-3 hours |
| Treasure chests | 1-2 hours |
| Boss enemy | 2-3 hours |
| Victory sequence | 1-2 hours |
| Testing and polish | 3-5 hours |
| **Total** | **25-42 hours** |

---

## Phase 6 Checklist

- [ ] World layout designed on paper first
- [ ] Tilemap system working
- [ ] Player moves with arrow keys/WASD
- [ ] Collision stops player at walls
- [ ] Village map created
- [ ] At least one NPC in village
- [ ] Shop accessible from village
- [ ] Dialogue system displays text
- [ ] Forest/path area with weak enemies
- [ ] Dungeon with multiple floors
- [ ] Visible enemies on maps
- [ ] Touching enemy starts battle
- [ ] 3-5 different enemy types
- [ ] Map transitions work (stairs, doors)
- [ ] Map state preserved (chests stay open)
- [ ] Treasure chests give loot
- [ ] Boss enemy created
- [ ] Defeating boss shows victory
- [ ] Full playthrough possible (village → boss)

---

## What You Should Have Now

A tiny but complete RPG. Player wakes in village, explores, fights enemies, buys potions, dives dungeon, defeats boss, wins game.

It's still ugly. That's fine. The GAME is done.

---

## Next Up

**Phase 7: Art Pass** — Replace rectangles with real graphics and make it look like a game.
