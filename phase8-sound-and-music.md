# Phase 8: Sound and Music

## Overview

Audio is the most underrated aspect of game development. A game without sound feels empty, lifeless, unfinished. Good audio makes correct answers satisfying, battles tense, and victories triumphant.

You don't need to compose music or record sounds. Free resources will get you 90% there.

---

## Why Audio Matters

**Sound creates feedback loops:**
- Correct answer → satisfying "ding" → dopamine → want to play more
- Enemy hit → impact sound → feels powerful
- Level up → fanfare → achievement feels real

**Music creates atmosphere:**
- Village music = safety, home, relaxation
- Dungeon music = tension, danger, adventure
- Boss music = epic, high stakes, climax

**Silence is also a choice:**
- Quiet before boss room builds anticipation
- No music during dialogue focuses attention

---

## Audio Asset Checklist

### Sound Effects Needed

**Battle Sounds:**
- [ ] Correct answer (satisfying ding/chime)
- [ ] Wrong answer (buzz/error)
- [ ] Enemy hit (impact)
- [ ] Player hit (different impact or grunt)
- [ ] Critical/Perfect hit (special impact)
- [ ] Heal sound (sparkle/restore)
- [ ] Buff applied (power-up)
- [ ] Buff expired (power-down, subtle)

**UI Sounds:**
- [ ] Menu select/hover
- [ ] Menu confirm
- [ ] Menu cancel/back
- [ ] Purchase item
- [ ] Inventory open
- [ ] Level up fanfare

**World Sounds:**
- [ ] Footsteps (optional, can get repetitive)
- [ ] Chest open
- [ ] Door open
- [ ] NPC interaction (small chime)
- [ ] Save point/heal point

**Victory/Defeat:**
- [ ] Victory jingle (5-10 seconds)
- [ ] Defeat jingle (sad, 3-5 seconds)
- [ ] Boss defeated (extended victory)

### Music Needed

**Tracks:**
- [ ] Title screen theme
- [ ] Village/town theme (peaceful)
- [ ] Overworld/exploration theme
- [ ] Dungeon theme (tense)
- [ ] Normal battle theme
- [ ] Boss battle theme (intense)
- [ ] Victory fanfare (short)
- [ ] Game over theme (optional, could be just jingle)

**Total: 6-8 music tracks**

---

## Free Audio Sources

### Sound Effects

**Freesound.org**
- Massive library of user-uploaded sounds
- Requires free account
- Check licenses (many are CC0)
- Quality varies wildly

**OpenGameArt.org**
- Game-specific sounds
- Usually game-ready
- Good organization by type

**Kenney.nl**
- Small but high-quality sound pack
- CC0 license
- Consistent style

**BFXR / SFXR**
- Generate retro 8-bit sounds
- Free tools, you make the sounds
- Great for that classic feel

### Music

**OpenGameArt.org**
- Many free game music tracks
- Various styles and quality

**Incompetech.com (Kevin MacLeod)**
- Royalty-free music
- Credit required
- Huge variety of styles

**Free Music Archive**
- Check licenses carefully
- Some gems if you dig

**itch.io**
- Search "game music pack"
- Many free or pay-what-you-want

### Recommended Approach

1. Start with BFXR for retro sound effects
2. Get music from OpenGameArt or Incompetech
3. Keep a credits file of everything you use

---

## Creating Your Own Sound Effects

### Using BFXR / SFXR

**What it is:** Free tool that generates 8-bit style sound effects

**Download:** bfxr.net (browser or download)

**How to use:**
1. Click preset buttons (Pickup, Hit, Jump, etc.)
2. Click "Randomize" until you hear something you like
3. Tweak sliders if needed
4. Export as WAV

**Generating sounds for Math RPG:**

| Sound | BFXR Preset | Tweaks |
|-------|-------------|--------|
| Correct answer | Pickup/Coin | Higher pitch |
| Wrong answer | Hit/Hurt | Lower pitch, shorter |
| Enemy hit | Hit/Hurt | Punchy, mid-range |
| Player hit | Hit/Hurt | Different pitch than enemy |
| Level up | Powerup | Longer, sweeping |
| Heal | Powerup | Sparkly, rising |

---

## Implementing Audio

### Basic Audio System

**Most engines have:**
- Play sound effect (one-shot, fire and forget)
- Play music (loops, one at a time)
- Volume controls

**Pseudocode:**
```
// Sound effects - fire and forget
function playSound(soundName):
    audio.playSFX(sounds[soundName])

// Music - only one track at a time
function playMusic(trackName):
    if currentMusic != trackName:
        audio.fadeOutMusic(0.5 seconds)
        audio.playMusic(music[trackName], loop=true)
        currentMusic = trackName
```

### When to Play Sounds

**Battle events:**
```
function onCorrectAnswer():
    playSound("correct")
    // ... rest of logic

function onWrongAnswer():
    playSound("wrong")
    // ... rest of logic

function onEnemyHit(damage):
    playSound("hit")
    // ... rest of logic

function onPlayerHit():
    playSound("player_hurt")
    // ... rest of logic
```

**UI events:**
```
function onMenuItemHover():
    playSound("menu_hover")

function onMenuItemSelect():
    playSound("menu_confirm")

function onMenuBack():
    playSound("menu_cancel")
```

**Music transitions:**
```
function enterVillage():
    playMusic("village_theme")
    // ... rest of logic

function startBattle():
    playMusic("battle_theme")
    // ... rest of logic

function enterBossRoom():
    playMusic("boss_theme")
    // ... rest of logic
```

---

## Music Guidelines

### Looping Music

Game music needs to loop seamlessly. Look for:
- Tracks labeled "loop" or "looping"
- Check that end connects to beginning
- No awkward silence at loop point

**If track doesn't loop well:**
- Fade out at end, fade in at restart
- Use audio editing software to fix loop point
- Or find a different track

### Music Volume Balance

**Problem:** Music drowning out sound effects

**Solution:** 
- Mix music quieter than SFX
- Let players adjust in settings

**Typical volumes:**
```
Music: 50-70%
Sound Effects: 80-100%
```

### Emotional Matching

**Village:** 
- Tempo: Slow to medium
- Key: Major (happy)
- Instruments: Soft, acoustic feel

**Dungeon:**
- Tempo: Medium
- Key: Minor (tense)
- Instruments: Atmospheric, echoing

**Battle:**
- Tempo: Fast
- Key: Can be major or minor
- Instruments: Energetic, driving rhythm

**Boss:**
- Tempo: Fast
- Key: Minor (epic/dramatic)
- Instruments: Everything louder and more intense

---

## Sound Design Tips

### Make Correct Answers Satisfying

The "correct answer" sound is the most important sound in your game. Players will hear it hundreds of times.

**It should be:**
- Short (under 0.5 seconds)
- Pleasant (not grating)
- Rewarding (makes you feel good)
- Distinct (clearly means "success")

**Test it:** Play the sound 50 times in a row. Still tolerable? Good.

### Make Wrong Answers Clear, Not Painful

Wrong answer sound should:
- Clearly indicate failure
- Not make player feel bad
- Be noticeably different from correct

**Avoid:** Harsh buzzer sounds that feel punishing. A gentle "boop" works better than "BZZZZT."

### Layer Sounds for Impact

**Big moments get multiple sounds:**
```
function onPerfectAnswer():
    playSound("correct")
    playSound("perfect_bonus")  // Extra sparkle on top
    // ... rest of logic
```

**Level up:**
```
function onLevelUp():
    playSound("level_up_fanfare")
    // Could also play music sting
```

---

## Audio Settings

### Let Players Control Volume

**Essential settings:**
- Master volume
- Music volume
- SFX volume

**Nice to have:**
- Mute button
- Individual sound toggles (rare)

**Settings UI:**
```
+---------------------------+
|      AUDIO SETTINGS       |
+---------------------------+
| Master:   [████████░░]    |
| Music:    [██████░░░░]    |
| SFX:      [████████░░]    |
|                           |
| [Mute All]                |
+---------------------------+
|      [Save] [Cancel]      |
+---------------------------+
```

### Saving Audio Preferences

Store volume settings and restore on game launch:
```
settings = {
    masterVolume: 0.8,
    musicVolume: 0.5,
    sfxVolume: 0.9
}

function saveSettings():
    writeToFile("settings.json", settings)

function loadSettings():
    if fileExists("settings.json"):
        settings = readFromFile("settings.json")
        applyAudioSettings(settings)
```

---

## Testing Audio

### Playtest Checklist

- [ ] Every action has appropriate sound
- [ ] No action is missing sound (silent feels broken)
- [ ] Sounds don't overlap badly (cacophony)
- [ ] Music loops don't have gaps
- [ ] Music transitions don't cut harshly
- [ ] Volume balance feels right
- [ ] Nothing is painfully loud
- [ ] Correct answer sound is satisfying after 100 plays

### Get Feedback

Ask playtesters:
- "Did any sound annoy you?"
- "Did anything feel silent that should have sound?"
- "Did the music fit the mood?"

### Common Audio Problems

**Problem:** Sounds cutting each other off
**Solution:** Allow multiple simultaneous sounds, or prioritize

**Problem:** Sound delay feels laggy
**Solution:** Preload sounds, ensure immediate playback

**Problem:** Music too loud/quiet relative to gameplay
**Solution:** Adjust volumes, test on different speakers

**Problem:** Loop gap in music
**Solution:** Fade transition, or find better loop point

---

## Organizing Audio Files

### Folder Structure

```
/audio
    /sfx
        correct.wav
        wrong.wav
        hit_enemy.wav
        hit_player.wav
        heal.wav
        buff.wav
        level_up.wav
        menu_select.wav
        menu_confirm.wav
        chest_open.wav
        victory.wav
        defeat.wav
    /music
        title.ogg
        village.ogg
        dungeon.ogg
        battle.ogg
        boss.ogg
```

### File Formats

**Sound effects:** WAV (uncompressed, fast loading)
**Music:** OGG or MP3 (compressed, smaller files)

Most engines handle both formats. OGG is generally preferred over MP3 for games (no licensing concerns).

---

## Credits and Licensing

### Keep a Credits File

As you add audio, track sources:

```
# Audio Credits

## Sound Effects
- correct.wav: Generated with BFXR
- hit_enemy.wav: "Punch" by UserName, Freesound.org, CC0
- menu_select.wav: Kenney.nl UI Sound Pack, CC0

## Music
- village.ogg: "Peaceful Village" by Composer, OpenGameArt, CC BY 3.0
- battle.ogg: "Epic Battle" by Kevin MacLeod, incompetech.com, CC BY 3.0
```

### Display Credits In-Game

Add a credits screen accessible from main menu:
- List all audio sources
- Fulfill attribution requirements (CC BY licenses)

---

## Time Estimate for Phase 8

| Task | Time |
|------|------|
| Source/create battle sound effects | 2-3 hours |
| Source/create UI sound effects | 1-2 hours |
| Source/create world sound effects | 1-2 hours |
| Find music tracks | 2-4 hours |
| Implement sound effect triggers | 2-3 hours |
| Implement music system | 2-3 hours |
| Volume settings UI | 1-2 hours |
| Test and balance volumes | 2-3 hours |
| Credits file/screen | 1 hour |
| **Total** | **14-23 hours** |

---

## Phase 8 Checklist

- [ ] Correct answer sound implemented
- [ ] Wrong answer sound implemented
- [ ] Enemy hit sound
- [ ] Player hit sound
- [ ] Heal sound
- [ ] Buff sounds (apply and expire)
- [ ] Level up fanfare
- [ ] Menu navigation sounds
- [ ] Chest open sound
- [ ] Victory jingle
- [ ] Defeat jingle
- [ ] Title screen music
- [ ] Village/safe area music
- [ ] Dungeon music
- [ ] Battle music
- [ ] Boss music
- [ ] Music loops properly
- [ ] Music transitions smoothly
- [ ] Volume settings work
- [ ] Settings persist between sessions
- [ ] Credits file created
- [ ] Full playthrough with audio feels complete

---

## What You Should Have Now

Close your eyes and listen to someone play your game. You should be able to tell:
- When they get an answer right or wrong
- When they're in battle vs. exploring
- When they win or lose
- When they level up

The audio tells the story even without visuals.

---

## Next Up

**Phase 9: Playtest With Real Humans** — The most humbling and valuable phase of development.
