---

## 16. Phase 1 — Team Task Breakdown

> **Team:** Dor, Orr, Shai, RBS — all SW engineers, minimal game design background, no art background.
> **Approach:** Use placeholder shapes and free asset packs for all art in Phase 1. No custom art required. Focus is on systems and gameplay feel.
> **Art resources to use:** [Kenney.nl](https://kenney.nl) — free top-down asset packs, no attribution required.

---

### 🧑‍💻 Orr — Project Lead & Core Systems

Orr sets up the project and owns the foundational systems everything else plugs into.

**Tasks:**
- [ ] Create Unity 6 project, set up Git repository, define folder structure (`Scripts`, `Scenes`, `Prefabs`, `Art`, `Audio`)
- [ ] Configure Unity for top-down 2D (camera orthographic, physics layers, input system)
- [ ] Implement **PlayerController** — 8-directional WASD movement, mouse aim, character rotation toward cursor
- [ ] Implement **dash/roll** mechanic with cooldown
- [ ] Implement **health system** — base `HealthComponent` class usable by both player and enemies
- [ ] Implement **death and respawn** — player death event, respawn at last checkpoint
- [ ] Set up **scene management** — main menu scene, game scene, respawn flow
- [ ] Define and document **coding standards** for the team (naming conventions, prefab structure)

---

### 🧑‍💻 Dor — Combat & Weapons

Dor owns everything related to fighting — how attacks work, how weapons behave, how damage is dealt.

**Tasks:**
- [ ] Implement **melee attack system** — attack direction based on mouse, hitbox activation, damage dealing, swing animation trigger
- [ ] Implement **ranged attack system** — bullet prefab, fire direction toward mouse cursor, bullet travel and collision
- [ ] Implement **pistol weapon** — fire rate, ammo count, reload mechanic, ammo depletion
- [ ] Implement **weapon swap system** — player holds 2 weapons, swap with Q
- [ ] Implement **ammo pickup** — ammo item in world, player walks over to collect
- [ ] Implement **knockback** — enemies pushed back on hit
- [ ] Implement **headshot detection** — bonus damage when bullet hits enemy head hitbox
- [ ] Wire combat events into HealthComponent (Orr's system)

---

### 🧑‍💻 Shai — Enemy AI & World

Shai owns the enemies and the game world they live in.

**Tasks:**
- [ ] Implement **Walker enemy** — patrol behavior, player detection radius, walk toward player, melee attack on contact
- [ ] Implement **Runner enemy** — same as Walker but faster, shorter detection range, more aggressive
- [ ] Implement **basic enemy AI state machine** — Idle → Chase → Attack → Dead states
- [ ] Implement **enemy spawner** — spawn enemies at set points, respawn after cooldown
- [ ] Build **Phase 1 test zone** — Suburbs map using Kenney top-down assets (roads, houses, fences, trees)
- [ ] Place **tilemaps** — ground layer, obstacle layer (collisions), decoration layer
- [ ] Place **checkpoint** objects in the world that wire into Orr's respawn system
- [ ] Implement **loot drop** — enemy drops a loot item on death (ammo or health pickup)

---

### 🧑‍💻 RBS — UI & Game Feel

RBS owns everything the player sees on screen plus juice and polish that makes the game feel good.

**Tasks:**
- [ ] Implement **HUD** — HP bar, ammo counter (current / max), equipped weapon icon, minimap placeholder
- [ ] Implement **damage numbers** — floating text popup on hit showing damage dealt
- [ ] Implement **screen shake** on hit received and on shooting heavy weapons
- [ ] Implement **hit flash** — enemy sprite flashes white when damaged
- [ ] Implement **main menu screen** — Play button, placeholder logo, basic layout
- [ ] Implement **death screen** — "You Died" screen with respawn button
- [ ] Implement **pause menu** — Esc to pause, resume/quit options
- [ ] Add **basic sound effects** using free SFX (freesound.org) — gunshot, melee hit, zombie groan, player hurt, pickup sound

---

### 🤝 Shared / Integration Tasks (whole team)
- [ ] Weekly playtest session — everyone plays the current build and logs bugs
- [ ] Integration milestone: Combat + AI working together (Dor + Shai sync)
- [ ] Integration milestone: UI wired to all systems (RBS syncs with Orr + Dor)
- [ ] Final Phase 1 build — playable from main menu to death/respawn in the suburbs zone

---

### 📅 Suggested Timeline

| Week | Goal |
|---|---|
| Week 1 | Project setup, movement, basic world tile map |
| Week 2 | Combat working (melee + pistol), Walker enemy |
| Week 3 | Runner enemy, health system, death/respawn |
| Week 4 | HUD, UI, sound effects, loot drops |
| Week 5 | Integration, bugfix, full playtest of Phase 1 |# DEAD SIDE
## Game Design Document — v0.1
### Confidential / Internal Use

---

## 1. Game Overview

| Field | Details |
|---|---|
| **Title** | Dead Side |
| **Genre** | Top-Down 2D Multiplayer RPG |
| **Platform** | PC (Primary), potential console ports |
| **Engine** | Unity 6 |
| **Target Audience** | Fans of Zombie games, top-down RPGs like Hotline Miami, Enter the Gungeon, Survivors |
| **Player Count** | 1–4 players (online co-op) |
| **Tone** | Dark, gritty, survival-focused with RPG depth |

### Elevator Pitch
Dead Side is a 2D side-scrolling multiplayer RPG set in a zombie apocalypse. Players choose from distinct survivor classes — each with a rich backstory from before the outbreak — and fight their way through a devastated world filled with increasingly dangerous zombie variants. Through combat, looting, leveling, and cooperation, players build powerful survivors and uncover the story of how the world ended.

---

## 2. Core Pillars

1. **Meaningful Class Identity** — Your class defines not just how you play but who your character is. Each class has a unique backstory, weapon preferences, and skill tree.
2. **Tense Resource Management** — Ammo is finite. Supplies are scarce. Every fight has weight.
3. **Rewarding Progression** — Levels, loot, skills, and gear constantly push the player forward.
4. **Better Together** — Multiplayer co-op is deeply rewarding, with synergy bonuses and party mechanics that make teamwork genuinely impactful.

---

## 3. Setting & Story

### World
The game takes place in a mid-sized American city and its surrounding suburbs, forests, and industrial zones — roughly 18 months after a viral outbreak turned most of the population into the undead. Society has collapsed. Power grids are down. Small pockets of survivors cling to life in fortified safe zones.

### Premise
The players are survivors who have found each other at a last-known safe house. A radio broadcast hints at a government research facility that may hold the key to a cure — or at least a way out. The journey there is long, dangerous, and full of hard choices.

### Tone
Grounded and gritty. The world feels real and lost. There is dark humor in moments, but the core emotional experience is one of desperate survival, human resilience, and the occasional triumph against overwhelming odds.

---

## 4. Gameplay Overview

### 4.1 Core Loop
```
Enter Zone → Fight Zombies → Collect Loot → Complete Objectives
→ Return to Safe House → Upgrade Gear / Skills → Enter Next Zone
```

### 4.2 Movement & Controls
Top-down 2D movement with twin-stick style controls:

| Action | Input |
|---|---|
| Move | WASD |
| Aim | Mouse cursor |
| Attack / Shoot | Left Click |
| Dash / Roll | Shift |
| Interact | E |
| Swap Weapon | Q / Scroll Wheel |
| Open Inventory | Tab |
| Use Consumable | R |
| Reload | R (when weapon equipped) |
| Sprint | Hold Shift (walk) |

Character always faces the mouse cursor. Movement is in all 8 directions.

### 4.3 Combat
- **Melee:** Directional attacks with combo chains. Different weapons have different range, swing speed, and damage.
- **Ranged:** Aim with mouse. Weapons have recoil, spread, and reload mechanics. Ammo is a finite resource managed through the inventory.
- **Headshots:** Deal 2x damage and grant bonus XP.
- **Knockback:** Heavy weapons stagger zombies.
- **Stamina:** Affects dash frequency and heavy attack availability.

---

## 5. Weapons

### 5.1 Melee Weapons

| Weapon | Damage | Speed | Range | Notes |
|---|---|---|---|---|
| Machete | Medium | Fast | Short | Reliable early weapon |
| Sword | Medium-High | Medium | Medium | Balanced, good combo potential |
| Axe | High | Slow | Short | Cleave hits multiple enemies |
| Crowbar | Low-Medium | Fast | Short | Common loot, never breaks |
| Chainsaw | Very High | Medium | Short | Loud — attracts nearby zombies |

### 5.2 Ranged Weapons

| Weapon | Damage | Fire Rate | Range | Ammo Type | Notes |
|---|---|---|---|---|---|
| Pistol | Low-Med | Fast | Medium | Pistol | Reliable, common ammo |
| Shotgun | High | Slow | Short | Shells | Devastating up close, spread |
| Rifle / AR | Medium | Medium | Long | Rifle | Versatile, moderate ammo cost |
| Sniper Rifle | Very High | Very Slow | Very Long | Sniper | One-shot weak zombies, skill-based |
| SMG | Low | Very Fast | Short-Med | Pistol | Spray and pray, burns ammo fast |
| Bow | Medium | Slow | Long | Arrows | Silent, arrows are recoverable |

### 5.3 Ammo System
- Each weapon type uses a specific ammo category (Pistol, Rifle, Shells, Sniper, Arrows)
- Ammo is found as loot drops, in crates, or crafted
- Running dry forces melee or retreat — creates real tension
- Tactical Vests increase ammo carry capacity per slot

---

## 6. Classes

Each class begins with a unique tutorial that reflects their life before the outbreak. Class determines starting gear, available weapon types, and skill tree branches.

---

### 6.1 🪖 Soldier

**Background Story:**
Marcus Webb was a decorated Army Sergeant who had done two tours overseas and was three months from retirement when everything fell apart. He was on base when the first reports came in — dismissed as riots at first. By the time command gave the order to evacuate civilians, it was already too late. Marcus fought his way out of the base alone, watching his unit fall one by one. He carries their dogtags. He doesn't talk about it. His military training is the only reason he's still breathing — and he knows it.

**Starting Gear:** Assault Rifle, Combat Knife, Military Vest  
**Preferred Weapons:** Rifles, SMGs, all melee  
**Role:** Frontline DPS / Tank hybrid  

**Skill Tree Branches:**
- **Combat Training** — Increased melee damage, combo length, block mechanics
- **Weapons Specialist** — Reduced recoil, faster reload, ammo efficiency
- **Leadership** — Party-wide attack/defense buffs, rally cry ability

---

### 6.2 🩺 Doctor

**Background Story:**
Dr. Priya Nair was a trauma surgeon at City General Hospital. She was mid-surgery when infected patients started flooding the ER. She barricaded herself in the operating room with three nurses and a security guard. Over the next 72 hours she kept them alive using whatever supplies were left in the room. Only she made it out. The experience left her cold and precise. She wastes nothing — not supplies, not words, not chances. Her medical bag goes everywhere with her.

**Starting Gear:** Scalpel, Medkit x3, Syringe Gun (custom)  
**Preferred Weapons:** Pistols, improvised melee, medical tools  
**Role:** Support / Utility  

**Skill Tree Branches:**
- **Field Medicine** — Enhanced healing items, revive speed, passive HP regen aura
- **Chemistry** — Craft advanced consumables, poison/acid throwables, stimulant injections
- **Triage** — Keep downed players alive longer, emergency stabilization skills

---

### 6.3 🏹 Hunter

**Background Story:**
Danny Rourke grew up hunting with his father in rural Montana. He moved to the city for work, never quite fitting in — always more comfortable in the woods than in an office. When the outbreak hit, Danny did what felt natural: he packed his gear and headed out of the city on foot. He's been surviving in the wilderness for months, picking off infected from a distance and moving before they find him. He thinks people who stayed in cities are idiots. He's not entirely wrong.

**Starting Gear:** Compound Bow, Hunting Knife, Camouflage Vest, 20 Arrows  
**Preferred Weapons:** Bow, Crossbow, Sniper Rifle, Traps  
**Role:** Ranged DPS / Battlefield Control  

**Skill Tree Branches:**
- **Marksmanship** — Increased ranged accuracy, headshot damage, arrow retrieval rate
- **Trapper** — Deployable traps (bear traps, tripwires, spike pits), slow/stun effects
- **Wilderness Survival** — Enhanced loot from nature zones, stamina bonuses, animal companion (dog)

---

### 6.4 🌾 Farmer

**Background Story:**
Earl Hutchins ran a 300-acre farm outside of town with his wife and two sons. He was never rich but he was self-sufficient — grew his own food, fixed his own machinery, built half of his farmhouse himself. When the dead started walking, Earl fortified the farm. He held it for four months. His wife and boys made it out to a refugee camp. Earl stayed behind to buy them time, then followed on foot. He has powerful hands, an unshakeable calm, and absolutely no patience for people who panic. He's also a surprisingly good cook.

**Starting Gear:** Pitchfork, Shotgun, Work Boots (stamina bonus), Food Supplies x5  
**Preferred Weapons:** Shotgun, Axe, Pitchfork, improvised weapons  
**Role:** Tank / Sustain / Crafter  

**Skill Tree Branches:**
- **Hard Labor** — Increased HP, carrying capacity, melee knockback, stamina pool
- **Resourcefulness** — Craft weapons and consumables from scrap, find more food loot, repair gear
- **Fortification** — Build barricades and defensive structures, placeable cover, resource caches

---

## 7. Progression Systems

### 7.1 Experience & Leveling
- XP gained from killing zombies, completing quests, discovering locations, and crafting
- Level cap: **100** (with prestige system planned post-launch)
- Each level grants: +HP, +1 Skill Point, minor stat improvements
- Level milestones (20, 40, 60, 80) unlock advanced skill tree tiers

### 7.2 Skill Trees
Each class has 3 branches with approximately 15 skills each (45 total per class). Skills include:
- **Passive bonuses** — stat increases, resistance buffs
- **Active abilities** — cooldown-based special moves
- **Mastery skills** — powerful capstone abilities at the end of each branch

### 7.3 Gear & Rarity
| Rarity | Color | Description |
|---|---|---|
| Common | White | Basic loot, widely available |
| Uncommon | Green | Minor stat bonuses |
| Rare | Blue | Notable bonuses, sometimes with special effects |
| Military Grade | Purple | High performance, limited availability |
| Experimental | Orange | Unique effects, pre-outbreak prototype gear |

### 7.4 Gear Slots
| Slot | Examples |
|---|---|
| Head | Helmets, caps, hoods |
| Chest | Tactical vests, jackets, body armor |
| Legs | Cargo pants, knee pads |
| Boots | Work boots, tactical boots |
| Gloves | Combat gloves, work gloves |
| Weapon (Main) | Primary weapon |
| Weapon (Secondary) | Sidearm or melee |
| Backpack | Increases inventory size |
| Accessory | Watches, dog tags (stat bonuses) |

---

## 8. Inventory System

- **Base inventory:** Grid-based (8x6 slots)
- **Backpack upgrades** expand grid size (up to 12x10 with best backpack)
- Items have physical grid sizes (e.g. sniper rifle = 1x5, pistol = 1x2, medkit = 1x2)
- **Tactical Vests** add dedicated ammo pouches outside the main grid
- **Quick slots:** 4 hotbar slots for consumables and quick-swap weapons
- **Item inspection:** View item stats, lore descriptions, condition level
- **Item condition:** Gear degrades with use, can be repaired (especially relevant for Farmer class)

---

## 9. Enemies

### 9.1 Zombie Types

| Type | Description | Behavior | Threat Level |
|---|---|---|---|
| Walker | Standard infected | Slow, shambles toward sound/sight | Low |
| Runner | Recently turned, athletic | Fast sprint, unpredictable | Medium |
| Bloater | Swollen, gas-filled | Slow, explodes on death dealing AOE damage | Medium |
| Screamer | Vocal cords intact | Doesn't attack — screams to call nearby hordes | High (utility) |
| Crawler | Legless, ground level | Below swing height of most weapons, hard to hit | Medium |
| Armored | Turned while in riot gear | High defense, requires targeting weak points | High |
| Spitter | Mutated salivary glands | Ranged acid spit, keeps distance | Medium-High |
| Brute | Enormous infected | Very high HP, throws objects, AOE slam | Very High |
| Boss Zombies | Unique named variants | Zone-specific mechanics, multi-phase fights | Boss |

### 9.2 Horde Events
- Random or triggered large-scale zombie swarms
- Rewards players who survive with bonus loot drops
- Scale with player level and zone difficulty

---

## 10. World Structure

### 10.1 Zones
The game world is divided into connected zones with increasing difficulty:

| Zone | Setting | Recommended Level |
|---|---|---|
| Tutorial — Your Story | Class-specific intro (farm, hospital, etc.) | 1–5 |
| Suburbs | Residential streets, houses, backyards | 5–15 |
| Downtown | City streets, stores, office buildings | 15–30 |
| Industrial District | Warehouses, factories, rail yards | 30–50 |
| Hospital Complex | Multi-floor interior, labs | 50–65 |
| Military Checkpoint | Overrun base, armories | 65–80 |
| Research Facility | Endgame zone, story climax | 80–100 |

### 10.2 Safe Houses
- Scattered throughout zones
- Act as respawn points, fast travel nodes, and social hubs in multiplayer
- Can be upgraded with crafting stations, storage, and NPC traders

---

## 11. Multiplayer

### 11.1 Server Model
Dead Side uses a **persistent open-world server model** similar to MapleStory:
- Players share the same world zones in real time — you see and interact with everyone in the same map
- Each zone/channel has a **player capacity** (e.g. 50–100 players per channel)
- Multiple **channels** exist per zone — if a channel is full, players pick another
- Players are always online in the shared world, not in private sessions
- Safe Houses act as social hubs where players meet, trade, and form parties

### 11.2 Party System
- Up to **6 players** per party
- Party members share XP (split with bonus multiplier to encourage grouping)
- Individual loot rolls per player — no loot stealing
- Party buff: Mixed class compositions grant passive bonuses
- Party quests: Special instanced co-op dungeons (separate from the open world)
- Party members shown on minimap

### 11.3 Social Features
- Global chat, zone chat, party chat, whisper
- Friend list and friend locator
- Guild system (post-launch)
- Player trading — direct trade window between players
- NPC merchant stalls in Safe Houses

### 11.4 Networking Architecture
- **Dedicated servers** hosted per region (NA, EU, Asia)
- Server authoritative model — server validates all combat and loot
- Planned implementation: **Photon Fusion** (recommended for MMO-lite scale) or **Mirror + custom server**
- Zone instancing handles player load — seamless channel switching

### 11.5 Instanced Content
While the open world is shared, some content is instanced per party:
- **Party Dungeons** — special high-difficulty zones
- **Boss Raids** — up to 10 players, scheduled spawn times
- **Tutorial zones** — always private/single player

---

## 12. Tutorial

The first 3–5 levels are **class-specific single-player tutorials** that serve as both a gameplay introduction and a narrative prologue:

- **Soldier:** Fight through an overrun military base on the first day of the outbreak
- **Doctor:** Escape City General Hospital as the ER falls to infected patients
- **Hunter:** Track and survive in the wilderness outside the city, arriving days later
- **Farmer:** Defend the farmstead through the first night of the outbreak

Each tutorial teaches movement, combat, and class-specific mechanics in a contextually appropriate way. They end with the character arriving at the shared safe house, where the main game begins.

---

## 13. Audio & Visual Direction

### Visual Style
- Top-down 2D perspective
- Dark, gritty aesthetic with high contrast sprites
- Desaturated world palette with color pops for loot, fire, UI elements
- Smooth camera follow with slight zoom out during combat
- Blood and impact effects on hits
- Weather effects: rain, fog, ash fallout

### Audio Direction
- Ambient: wind, distant moaning, creaking structures
- Combat: impactful, weighty sound design for weapons
- Music: sparse, tension-based score — silence used deliberately
- Each class has unique voice lines

---

## 14. Development Phases

### Phase 1 — Playable Prototype
- Basic top-down movement and 8-directional controls
- Mouse aim and attack direction
- One zone (Suburbs)
- One class (Soldier)
- Two enemy types (Walker, Runner)
- Basic combat (melee + pistol)
- Health system and death/respawn

### Phase 2 — Core Systems
- Inventory system
- Loot drops and gear
- Leveling and basic skill tree
- All weapon types
- 2 more enemy types

### Phase 3 — Full Single Player
- All 4 classes with tutorials
- All zones
- Quest system
- Full skill trees
- All enemy types and bosses

### Phase 4 — Multiplayer
- Party system
- Online co-op
- Party quests
- Leaderboards

### Phase 5 — Polish & Launch
- Full audio implementation
- Balancing pass
- Additional content (events, seasonal updates)
- Console ports

---

## 15. Open Questions / TBD

- [ ] Crafting system depth — how complex?
- [ ] Permadeath / hardcore mode?
- [ ] Paid content model — cosmetics only?
- [ ] Ninja and Scavenger as additional classes post-launch?
- [ ] Vehicle mechanics (motorcycle for Engineer)?
- [ ] Mobile port viability?

---

*Document version 0.1 — Dead Side internal use only*
*Last updated: March 2026*
