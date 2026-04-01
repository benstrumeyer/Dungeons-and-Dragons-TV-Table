# BubbaBoard - D&D TV Table App

> Working title: **BubbaBoard** (named after Bubba)
> Collaborators: **ben** + **cypherix93**
> Platform: **Web app** displayed on a TV laid flat as a tabletop
> Date: January 26-28, 2026

---

## Vision

A web-based TTRPG battlemap interface running on a TV used as a tabletop. The TV is just an external monitor driven by a PC. The app is **system-agnostic** at its core — not locked to 5E, Roll20, or Foundry — but can integrate with them. Players interact via a companion phone/web app.

**Design philosophy:** Start with physical minis + a digital surface. Don't over-engineer mechanics — D&D 5E is vast. Build what makes the table *feel cool*, not what replaces the rulebook.

---

## MVP Features

### Battle Grid
- Default: **square grid**, 1 inch = 5 ft (in-game)
- Switchable to **hex grid**
- Scalable units — if the background image doesn't match pixel ratio, scale the grid to compensate
- Resizable grid overlay
- Physical minis sit on top of the TV surface

### HUD (BG3-inspired)
- **Top bar:** Initiative tracker (turn order)
- **Bottom bar:** PC portraits with status
- Buff/debuff icons on character portraits (HUD-style, not on the map)
- HP bars — visible, noticeable when damage is taken

### HP & Damage Animations
- On hit: damage number animation on the token area
- HP bar with **white trailing damage** that decreases after a short delay (fighting game style)
- Heal animation (reverse effect)
- HP change must be **noticeable** — whether on a token-adjacent bar or in the HUD

### Condition Effects
- Status auras/rings around token positions (rage, grappled, poisoned, etc.)
- Dynamic status rings on the map around where minis sit
- Animated effects: burning, bleeding, etc.

### Background & Map Layer
- Static or animated background images
- Maps viewable from all sides (no rotation — orientation matters)
- Slight isometric perspective is OK, no full 3D rotation (motion sickness concern)

### DM Controls
- DM manages the board from their own screen
- Invisible tokens visible only on DM's end (for hidden enemies, traps)
- DM moves digital tokens; effects target the physical token space

---

## Post-MVP Features

### Player Companion App (Phone/WebRTC)
- Players connect their phones to the table
- Move their own token from their phone
- Play sound effects / personal anime themes out of the table speakers
- Trigger emotes on their token (purely cosmetic, anytime, no gameplay effect)
- Light a torch (if lighting system is active)
- Interactive spell input — e.g., swirl on phone to mix a cauldron
- Cast a spell from D&D Beyond app, choose target on the table

### Spell & Attack Animations
- Flashy VFX for spells (fireball drops from sky like a meteor onto target squares)
- Pixel art / anime-inspired effects (Gojo domain expansion vibes)
- Condition-triggered animations: rage = super saiyan aura, grappled = NPC token expression change

### Dynamic Maps & Boss Encounters
- Maps that change during battle (phase transitions)
- Boss fights with scripted phases: new walls, lighting shifts, music swaps, arena hazards
- Camera pans (auto or DM-triggered)
- Interactive map elements: doors, elevators, teleport circles, pressure plates, traps

### Fog of War & Vision
- Player vision cones / line of sight
- Fog of war that reveals as players explore
- Auto-stealth rolls integration

### Height & Flying
- "Floors" concept — height toggler on the side, 10ft increments
- Fish-eye zoom effect centered on origin as height changes
- Stretch goal: Three.js 3D grid expansion for true flying encounters
- Pragmatic note: flying is usually theater-of-the-mind'd, don't over-engineer

### Digital Minis (alternative to physical)
- Isometric animated tokens
- Bigger boss minis (potentially AI-generated movement via Blender)
- Character effects: bleeding, burning, status visuals directly on the token
- Token emotes (cosmetic, player-triggered)

### Integrations
- **D&D Beyond API** — live character info, HP sync, spell slots
- **D&D Beyond iframe/Puppeteer** — embed parts of the site for quick reference
- **5E fuzzy search** — quick lookup for spells, items, monsters, rules
- **Foundry VTT modules** — inspiration for hooks-based scripting (not a hard dependency)
- Roll20 API — optional, not a primary target

### Voice Recognition
- Always-listening mic on the table picks up spell/action keywords
- Someone says "Fireball" → fireball sound effect + VFX triggers on the table
- "Healing Word" → healing chime + green glow on target
- "Eldritch Blast" → crackling energy SFX
- Could map any spell name to a sound + animation combo
- DM can say "Roll for initiative" → initiative tracker auto-opens with fanfare
- Configurable keyword → action map (JSON or UI editor)
- WisprFlow / Whisper API for transcription, keyword matching on the output
- Stretch: voice tone detection — whispering triggers quieter/subtler effects, shouting triggers bigger ones

### Hand Signs & TouchDesigner
- Hand gesture recognition for casting spells
- TouchDesigner integration for advanced visual effects
- Domain expansion hand signs

### Projection
- MadMapper projection mapping support
- Project the battlemap onto physical surfaces (not just TV)

---

## Physical Token Tracking (Unsolved)

How to sync physical minis with digital state:

| Approach | Pros | Cons |
|----------|------|------|
| Touch screen + sensors on mini bases | True tracking | Needs hardware |
| Kinect / depth camera overhead | No mini modification needed | Accuracy concerns |
| Player moves digital token, places mini on top | Simple, no hardware | Double-move breaks immersion |
| DM-only digital tokens (invisible on table) | Clean for players | DM overhead |

**Current lean:** DM manages digital tokens on their screen; effects render on the TV at token positions. Revisit when hardware options are explored.

---

## Tech Decisions

| Decision | Choice | Reasoning |
|----------|--------|-----------|
| Platform | Web app (browser) | Easy UI, runs on any PC driving the TV |
| Grid rendering | Canvas/WebGL | Performance for animations |
| 3D (stretch) | Three.js | Only if flying/height needs it |
| Phone connection | WebRTC or WebSocket | Real-time sync for player app |
| VTT dependency | None (integrations optional) | Don't want to be locked in or deprecated |

---

## Open Questions

1. How much do we actually need from Roll20/Foundry vs. building custom?
2. Best approach for physical-to-digital token tracking?
3. Digital minis vs. physical minis as the primary mode?
4. How to handle group battles efficiently?
5. What's the starter asset set for MVP?

---

## Name Candidates

- BubbaBoard
- Bubba FX
- Bubba Magic
- Bubba Boom
- Bubba Bing Bubba Boom
