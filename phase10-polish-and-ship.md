# Phase 10: Polish and Ship

## Overview

Your game works. People can play it. It's time to add final polish, squash remaining bugs, and actually release it into the world.

**The goal of this phase:** Get your game into players' hands. Done is better than perfect.

---

## What "Ship" Means

Shipping isn't just uploading files. It's:

1. **Stable build** — Game doesn't crash
2. **Complete experience** — Start to finish works
3. **Accessible** — Someone can download and play
4. **Presented** — Title screen, description, screenshots

You're not shipping to AAA standards. You're shipping a complete indie game.

---

## Polish Tasks

### Main Menu

Every game needs a main menu. Not optional.

**Required elements:**
- Game title
- New Game button
- Continue button (if save exists)
- Options/Settings button
- Credits button
- Quit button

**Main menu layout:**
```
+----------------------------------+
|                                  |
|           MATH RPG               |
|                                  |
|          [New Game]              |
|          [Continue]              |
|          [Options]               |
|          [Credits]               |
|          [Quit]                  |
|                                  |
+----------------------------------+
```

**Polish touches:**
- Title has your logo/art
- Background is game-related
- Subtle animation or particle effect
- Music plays

---

### Pause Menu

Player needs to be able to pause during gameplay.

**Required elements:**
- Resume button
- Options/Settings
- Save Game (if not autosave)
- Return to Main Menu
- Quit Game

**Pause menu:**
```
+----------------------------------+
|           PAUSED                 |
+----------------------------------+
|          [Resume]                |
|          [Options]               |
|          [Save Game]             |
|          [Main Menu]             |
|          [Quit]                  |
+----------------------------------+
```

**Warning:** Add confirmation for "Main Menu" and "Quit" — player might click accidentally.

---

### Options Menu

**Required:**
- Volume sliders (Master, Music, SFX)

**Nice to have:**
- Fullscreen toggle
- Resolution options
- Difficulty setting (if implemented)
- Controls display

**Options menu:**
```
+----------------------------------+
|           OPTIONS                |
+----------------------------------+
| Master Volume:  [████████░░]     |
| Music Volume:   [██████░░░░]     |
| SFX Volume:     [████████░░]     |
|                                  |
| [ ] Fullscreen                   |
|                                  |
|          [Back]                  |
+----------------------------------+
```

---

### Save System Review

Make absolutely sure saving/loading works:

**Test:**
- [ ] Save in middle of dungeon
- [ ] Quit game completely
- [ ] Relaunch game
- [ ] Continue loads correctly
- [ ] Position, stats, inventory all correct

**Edge cases:**
- [ ] Save file doesn't exist (new player)
- [ ] Save file is corrupted (handle gracefully)
- [ ] Player tries to continue without save (show message)

---

### Credits Screen

**Include:**
- Your name/studio name
- Asset credits (art, music, sound)
- Tools used (engine, software)
- Special thanks (playtesters, supporters)

**Credits example:**
```
MATH RPG

Created by: [Your Name]

Art:
- Character sprites by [Artist/Source]
- Tileset by [Artist/Source]

Music:
- "Village Theme" by Kevin MacLeod (incompetech.com)
- Licensed under CC BY 3.0

Sound Effects:
- Generated with BFXR
- UI sounds from Kenney.nl

Made with [Engine Name]

Special Thanks:
- [Playtesters]
- [Supporters]
- You, for playing!
```

---

## Bug Hunting

### The Bug Bash

Dedicate time to finding and fixing bugs. Play through the entire game multiple times.

**Bug bash checklist:**
- [ ] Play from new game to credits
- [ ] Try to break things intentionally
- [ ] Test all menu options
- [ ] Test save/load in different places
- [ ] Try unusual inputs
- [ ] Check edge cases (0 HP, max stats, empty inventory)

### Common Last-Minute Bugs

**Save/Load issues:**
- New features not saved
- Old saves break on new version
- Load puts player in wrong location

**UI issues:**
- Text overflow
- Buttons not working
- Wrong screen showing

**Balance issues:**
- Enemy too easy/hard
- Heal too powerful
- Math too difficult at certain level

**Audio issues:**
- Sound not playing
- Music not looping
- Volume settings not applying

### Bug Priority

**Must fix before release:**
- Crashes
- Softlocks (can't progress)
- Data loss (save corruption)
- Progression blockers

**Should fix:**
- Incorrect text
- Visual glitches
- Minor balance issues

**Can ship with:**
- Edge case weirdness
- "Won't encounter normally" bugs
- Minor visual polish

---

## Preparing for Release

### Export Your Build

**Godot:**
```
Project → Export → Add preset → [Platform]
Export Project → Choose location → Export
```

**Unity:**
```
File → Build Settings → Select platform
Build → Choose location
```

**RPG Maker:**
```
File → Deployment → Choose platform
Deploy
```

### Test the Exported Build

**Critical:** Play the exported version, not the editor version.

- [ ] Game launches
- [ ] Menu works
- [ ] New game starts
- [ ] Save/load works
- [ ] Can complete the game
- [ ] No missing assets
- [ ] Audio plays

### Create Release Assets

**Screenshots (3-5):**
- Title screen
- Combat screenshot
- World exploration
- Character progression/stats
- Anything that shows variety

**Tips for good screenshots:**
- Capture at native resolution
- Show interesting moments
- No debug text or UI clutter
- Consistent sizing

**Short description (1-2 sentences):**
"A 2D RPG where math skills power your attacks! Solve problems fast to deal massive damage and level up your stats."

**Long description (1-2 paragraphs):**
Include:
- What the game is
- Unique hook (math = combat)
- What player does
- Approximate length
- Any content warnings if relevant

**Trailer/GIF (optional but recommended):**
- 30-60 seconds of gameplay
- Show combat, exploration, progression
- Add music
- Tools: OBS (record) + any video editor

---

## Where to Release

### itch.io (Recommended First)

**Why itch.io:**
- Free to upload
- Easy to set up
- Built-in community
- Can set "pay what you want" including free
- No approval process

**Setup:**
1. Create itch.io account
2. Go to Dashboard → Create new project
3. Fill in title, description, screenshots
4. Upload your build (zip file)
5. Set pricing (free or PWYW)
6. Publish

### Other Platforms

**Game Jolt:** Similar to itch.io, game-focused

**Steam:** Requires $100 fee, more complex process, save for later

**Newgrounds:** If your game can run in browser

**Mobile stores:** Requires different builds, more work, maybe later

---

## Release Checklist

### Before Release

- [ ] Full playthrough with no crashes
- [ ] Save/load tested
- [ ] All menus work
- [ ] Audio working
- [ ] Credits complete
- [ ] Exported build tested
- [ ] Screenshots captured
- [ ] Description written
- [ ] Platform account created

### Release Day

- [ ] Upload build
- [ ] Add screenshots
- [ ] Write description
- [ ] Set pricing
- [ ] Publish
- [ ] Test download and play yourself
- [ ] Share link with friends/playtesters
- [ ] Announce somewhere (social media, forums)

### After Release

- [ ] Monitor for bug reports
- [ ] Respond to comments
- [ ] Track downloads/plays
- [ ] Celebrate! You shipped a game!

---

## Post-Release

### Expect Bugs

Players will find bugs you missed. That's okay.

**Handling bug reports:**
1. Thank the reporter
2. Try to reproduce
3. Fix if possible
4. Update the build
5. Note in changelog

### Gathering Feedback

**Good questions to ask:**
- What did you enjoy most?
- What was frustrating?
- Would you recommend it?
- What would you add?

### Updating Your Game

**When to update:**
- Critical bug fixes (ASAP)
- Quality of life improvements (batch together)
- New content (when ready)

**Keep a changelog:**
```
Version 1.1 - [Date]
- Fixed crash when using potion in boss fight
- Adjusted multiplication difficulty at level 5+
- Added visual feedback for buff expiring

Version 1.0 - [Date]
- Initial release
```

---

## Celebrate Your Achievement

You made a game. A real, playable game that other people can experience.

**This is huge.** Most people who start making games never finish. You did.

**What you've learned:**
- Game design
- Programming
- Project management  
- Art direction
- Audio implementation
- Playtesting
- Shipping a product

These skills transfer to anything you do next.

---

## What's Next?

### Option 1: Expand This Game
- More dungeons
- More enemies
- Story elements
- More math mechanics
- Multiplayer?

### Option 2: Make a New Game
- Apply everything you learned
- Start smaller and faster
- Try a different genre

### Option 3: Take a Break
- You've earned it
- Come back fresh
- Play other games for inspiration

**Whatever you do:** You are now a game developer. That never goes away.

---

## Time Estimate for Phase 10

| Task | Time |
|------|------|
| Main menu implementation | 2-3 hours |
| Pause menu | 1-2 hours |
| Options menu | 1-2 hours |
| Save system verification | 1-2 hours |
| Credits screen | 1 hour |
| Bug bash | 4-8 hours |
| Bug fixes | 4-8 hours |
| Export build | 1 hour |
| Test exported build | 1-2 hours |
| Screenshots and description | 1-2 hours |
| Upload to platform | 1 hour |
| **Total** | **18-32 hours** |

---

## Phase 10 Checklist

**Menus:**
- [ ] Main menu works
- [ ] Pause menu works
- [ ] Options menu works
- [ ] Credits screen exists

**Stability:**
- [ ] No crashes found
- [ ] No softlocks found
- [ ] Save/load works perfectly
- [ ] All menus navigate correctly

**Release Assets:**
- [ ] 3-5 screenshots
- [ ] Short description written
- [ ] Long description written
- [ ] (Optional) GIF or trailer

**Release:**
- [ ] Build exported
- [ ] Exported build tested
- [ ] Uploaded to itch.io (or platform)
- [ ] Page looks good
- [ ] Link works
- [ ] Download and play verified
- [ ] Announced to at least one person

**Celebration:**
- [ ] Recognized your accomplishment
- [ ] Told someone you shipped a game
- [ ] Felt proud

---

## Final Words

You started with an idea: "A game that teaches math through RPG combat."

You now have a finished product that real people can play.

That's game development. That's shipping.

**Go make something.**

---

## Appendix: Total Time Estimates

| Phase | Time Range |
|-------|------------|
| Phase 1: Pick Your Engine | 3-4 hours |
| Phase 2: Make It Playable Ugly | 8-15 hours |
| Phase 3: Design Your Numbers | 7-11 hours |
| Phase 4: Build Complete Battle | 14-22 hours |
| Phase 5: Add Progression | 16-26 hours |
| Phase 6: Create the World | 25-42 hours |
| Phase 7: Art Pass | 24-42 hours |
| Phase 8: Sound and Music | 14-23 hours |
| Phase 9: Playtest | 1-3 weeks |
| Phase 10: Polish and Ship | 18-32 hours |
| **Total** | **~130-220 hours** |

At 10 hours/week, that's 3-6 months.
At 20 hours/week, that's 2-3 months.

**Totally achievable.** Go build it.
