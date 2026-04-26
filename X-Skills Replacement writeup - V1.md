# X-Skills Replacement

**Project Plan & Design Document** _Vintage Story Mod | Aldi's Classes RP Integration_ _March 2026 | Draft v1.0_

---

## 1. Project Overview

The X-Skills Replacement mod aims to rebuild the existing X-Skills framework from the ground up with three core priorities: performance optimization, deep cross-skill synergy, and a polished Enshrouded-style GUI. The current X-Skills mod causes noticeable server-side lag and lacks the tight integration needed to support an economy-driven RP server running Aldi's Classes RP Patch.

This mod will serve as the primary character progression system layered on top of Aldi's Classes, giving each class a distinct skill identity while keeping all classes interdependent — no single player or class can reach end-game without relying on others.

## 2. Design Goals

### 2.1 Performance

- Replace all polling-based tick loops with event-driven hooks (BlockBreak, EntityDeath, etc.)
    
- Lazy-load ability configs — only parse JSON for skills the player has unlocked
    
- Use server-side delta-sync for XP/level updates rather than broadcasting full skill state
    
- Minimize per-tick entity attribute lookups by caching frequently-read values
    

### 2.2 Synergy & Economy

- Every skill has at least one ability that provides materials or unlocks recipes needed by another skill
    
- High-tier crafting (steel tools, advanced pottery, compound alchemy) requires materials from multiple skill trees
    
- Class exp multipliers from Aldi's Classes are preserved and extended — your class defines your fastest growth path, not your only one
    
- End-game specialization abilities require proof of cross-skill investment (e.g., a Metalworking ability that scales with Mining level)
    

### 2.3 UI / UX

- Enshrouded-style skill tree GUI: dark background, glowing node icons, connection lines between nodes
    
- Separate skill trees per discipline, accessible from a single tabbed panel
    
- Tooltips show current values, next-tier values, and unlock requirements
    
- Visual XP bars per skill with floating +XP feedback on action
    
- Skill book items for gifting/trading XP boosts between players
    

## 3. Aldi's Classes Integration

The following classes are active under the RP Patch and map to skill disciplines. Each class gains a primary skill exp bonus, a secondary skill bonus, and penalties to competing disciplines.

---

**Class** **Primary Skill (+)** **Secondary Skill (+)** **Penalty Skills (-)** **Notes**

---

Miner Mining +25% Temporal Adaptation +15% Farming, Husbandry Best deep ore yield

Blacksmith Metalworking +25% Mining +15% Farming, Survival Only class to craft iron doors

Potter Pottery +25% Digging +50% Combat, Metalworking Kiln efficiency unlocks

Mason Masonry +25% Digging +25% Combat, Husbandry Stone path/road unlocks

Carpenter / Lumberjack Forestry +25% Digging +15% Temporal Adaptation Charcoal + advanced woodwork

Farmer Farming +25% Cooking +10% Combat, Metalworking Crop yield and rare seed unlocks

Innkeeper Cooking +25% Husbandry +25% Combat, Mining Stat buff food unlocks

Squire / Mercenary Combat +15/+25% Survival +15/+20% Pottery, Farming PvE and PvP unlocks

Wanderer / Wildrunner Survival +25% Temporal Adaptation +15% Metalworking, Combat Exploration and off-grid unlocks

Commoner All skills +10% — None Versatile, no specialization

Hunter Husbandry +20% Survival +20% Farming, Metalworking Animal tracking unlocks

Druid Farming +15% Temporal Adaptation +10% Metalworking, Combat Natural alchemy cross-skill

Entropic / Clockmaker Temporal Adaptation +25% Engineering +20% Survival, Farming Temporal gear and automation

## Malefactor / Blackguard Combat +20% Survival +15% Pottery, Cooking Darker ability unlocks (looting, ambush)

## 4. Skill Tree Designs

Each skill has a max level of 25 and uses a quadratic XP curve. Abilities unlock at specific level thresholds and have up to 3 upgrade tiers. Below is the proposed design for all 13 skill disciplines, including the two new skills: Alchemy and Engineering (plus Masonry, which extends the Digging/Mining axis for Mason class).

### 4.1 Mining

Core progression for ore extraction, stone cutting, and deep-earth expertise. The backbone of the server economy — Blacksmiths depend on Miners for smelting materials.

Existing abilities retained: Stonebreaker, Stonecutter, Oreminer, Gemstoneminer, Pickaxe Expert, Careful Miner, Miner (passive), Crystal Seeker, Bomberman, Geologist, Vein Miner, Tunnel Digger, Blaster.

#### New / Modified Abilities

- Deep Cartographer (Lv 8, Tier 2): Reveals nearby ore veins on the minimap within a radius. Tier 2 increases range and adds gemstone detection. Synergy: shares data with Geologist.
    
- Ore Scholar (Lv 12, Tier 1): +5% exp gain from all ore types per 5 levels of Metalworking skill. Direct cross-skill link.
    
- Blasting Compound (Lv 15, Tier 3): Unlocks crafting of advanced explosive charges requiring Saltpeter (Digging) and metal casings (Metalworking). Requires Mining Lv 15 + Metalworking Lv 10.
    

### 4.2 Survival

The universal baseline skill — every class gains it, but Wanderers, Wildrunners, and Shadowstriders excel. Covers health, food saturation, movement, and environmental adaptation.

Existing abilities retained: Longlife, Huge Stomach, Well Rested, Nudist, Meat Shield, Diver, Feather Fall, All-Rounder, Photosynthesis, Strong Back, On the Road, Scout, Healer, Steeplechaser, Sprinter, Abundance Adaptation, Soulbound Bag, Luminiferous, Cat Eyes, Meteorologist, Last Stand.

#### New / Modified Abilities

- Trail Blazer (Lv 6, Tier 2): While on a road or stone path (Mason-crafted counts), +8%/+15% movement speed. Incentivizes Mason road infrastructure.
    
- Forager's Eye (Lv 8, Tier 2): Chance to find hidden berry bushes or wild herbs while walking. Higher tier adds chance for rare Alchemy ingredients.
    
- Crisis Response (Lv 12, Tier 1): When HP drops below 20%, gain a 10-second burst of +30% movement speed. One-minute cooldown.
    

### 4.3 Pottery

Creates crucibles, storage vessels, kiln components, and alchemical containers. Potters are the backbone of early-game food storage and mid-game alchemy infrastructure.

Existing abilities retained: Thrift, Layer by Layer, Perfect Fit, Perfectionist, Potter (passive), Fast Potter, Jackpot, Infallible, Inspiration, Pottery Timer.

#### New / Modified Abilities

- Kiln Master (Lv 7, Tier 2): Reduces fuel consumed per firing. Tier 2 unlocks a 'superfire' mode that increases output quality. Cross-skill: works with Forestry's Stoker ability.
    
- Alchemical Vessel (Lv 10, Tier 3): Unlock crafting of sealed clay flasks and distillation pots required for Alchemy skill progression.
    
- Ceramic Tooling (Lv 12, Tier 1): Unlocks ceramic-tipped tool heads. Lower durability than iron but can be crafted without metalworking. Bridge ability for early-game non-blacksmith players.
    

### 4.4 Metalworking

The apex crafting skill — unlocks the highest tier tools, weapons, and structural components. Entirely dependent on Mining for ore supply and Forestry for charcoal fuel.

Existing abilities retained: Smelter, Metal Recovery, Heating Hits, Hammer Expert, Heavy Hits, Blacksmith (passive), Metalworker (passive), Finishing Touch, Duplicator, Salvager, Mastersmith, Sense of Time, Machine Learning, Bloomery Expert, Automated Smithing.

#### New / Modified Abilities

- Alloy Theory (Lv 8, Tier 3): Increases output when smelting alloys (bronze, bismuth bronze, etc.). Requires Mining Lv 5 as a prerequisite. Tier 3 enables experimental alloy recipes.
    
- Tool Sharpening Station (Lv 10, Tier 2): Unlocks a craftable sharpening block. Players can use it to restore 25%/50% of tool durability. Cross-skill: Survival's Strong Back ability reduces weight penalty of extra tools.
    
- Mechanist's Touch (Lv 15, Tier 2): Allows creation of mechanical components (gears, shafts) at improved quality. Cross-skill synergy with Engineering skill.
    

### 4.5 Husbandry

Animal care, butchering, tanning, and livestock breeding. Innkeepers and Hunters depend heavily on it. Provides raw materials for Cooking, Tailoring-adjacent crafting, and Alchemy (animal-derived ingredients).

Existing abilities retained: Hunter, Butcher, Furrier, Bone Breaker, Rancher, Feeder, Lightfooted, Shepherd, Preserver, Tanner, Cheesy Cheese, Catcher, Breeder, Mass Husbandry.

#### New / Modified Abilities

- Byproduct Harvesting (Lv 5, Tier 2): Chance to collect glands, bile, or rare animal materials when butchering. Required ingredients for Alchemy mid-tier recipes.
    
- Herd Efficiency (Lv 10, Tier 2): Each pen that has been tended reduces feeding interval. Tier 2 adds passive wool/milk generation without manual collection trigger. Cross-skill: Farming's Composting ability benefits from manure outputs.
    
- Trophy Taxidermy (Lv 13, Tier 1): Craft decorative trophies from creature drops. Primarily cosmetic/RP but grants small bonus to nearby player morale (stat buff while in proximity).
    

### 4.6 Forestry

Timber production, charcoal burning, resin tapping, and advanced woodcraft. Carpenters and Timberbourns are primary users. Charcoal is the single most important fuel for Metalworking.

Existing abilities retained: Lumberjack, Afforestation, More Ladders, Resin Farmer, Tree Nursery, Axe Expert, Careful Lumberjack, Forester, Charcoal Burner, Stoker, Grafter, Resin Extractor.

#### New / Modified Abilities

- Bark Stripper (Lv 5, Tier 2): Strips bark from logs for tannin yield. Cross-skill: tannin is required by Husbandry's Tanner ability for high-quality leather.
    
- Old Growth Scout (Lv 8, Tier 1): Passive ability to mark ancient trees on map — these yield double logs and rare wood types usable in Engineering builds.
    
- Sustainable Forestry (Lv 10, Tier 2): Saplings planted by this player grow 20%/40% faster. Tier 2 adds a chance for fruit-bearing trees to spawn from planting. Cross-skill: Farming's Beekeeper benefits from nearby flowering trees.
    

### 4.7 Farming

Crop cultivation, orcharding, beekeeping, and seed genetics. Farmers supply raw ingredients for Cooking, beeswax for Alchemy candles, and rare cultivars for the server economy.

Existing abilities retained: Green Thumb, Demeter's Blessing, Gatherer, Orchardist, Repotting, Recycler, Careful Hands, Farmer (passive), Bright Harvest, Cultivated Seeds, Beekeeper, Extensive Farming, Composting, Crossbreeding, Bee Master.

#### New / Modified Abilities

- Botanical Knowledge (Lv 8, Tier 3): Identifies wild plants with tooltip descriptions. Tier 2 adds a chance to transplant wild plants. Tier 3 unlocks rare herb cultivation required for Alchemy tier 2+.
    
- Fermentation Basics (Lv 10, Tier 2): Unlocks simple fermentation crocks. Items stored in them gain a 'fermented' tag required by Cooking's Gourmet ability at higher tiers. Cross-skill gateway.
    
- Soil Remediation (Lv 13, Tier 1): Tilled soil on this player's claim never degrades to stone. Passive quality-of-life for large farms.
    

### 4.8 Digging

Clay, peat, saltpeter, and soil extraction. The Potter and Mason classes depend on it heavily. Saltpeter is a key ingredient in Mining's advanced explosives.

Existing abilities retained: Clay Digger, Peat Cutter, Saltpeter Digger, Shovel Expert, Careful Digger, Mixed Clay, Quick Pan, Gold Digger, Digger (passive), Scrap Detector, Scrap Specialist.

#### New / Modified Abilities

- Compressed Earth (Lv 5, Tier 2): Compress clay into dense clay blocks used in advanced Masonry structures. Requires Digging Lv 5 + Masonry Lv 3.
    
- Mineral Prospector (Lv 8, Tier 2): Panning has a chance to produce trace mineral samples that identify nearby ore deposits. Cross-skill synergy with Mining's Geologist.
    
- Peat Fuel Processing (Lv 10, Tier 1): Processed peat bricks burn 50% longer. Alternative fuel source for players without Forestry charcoal access.
    

### 4.9 Cooking

Food preparation, preservation, juicing, and advanced recipes. Innkeepers are the primary chefs but every player benefits. High-tier cooking produces stat buff foods that enhance other skills.

Existing abilities retained: Canteen Cook, Fast Food, Well Done, Dilution, Desalinate, Salty Backpack, Gourmet, Chef (passive), Happy Meal, Juicer, Egg Timer.

#### New / Modified Abilities

- Herbalist Broth (Lv 8, Tier 3): Using herbs from Farming's Botanical Knowledge, brew specialty soups that grant temp buffs (+mining speed, +carry weight, etc.). Bridges Farming and Cooking.
    
- Aged Cuisine (Lv 10, Tier 2): Dishes that have been stored for 1+ in-game days gain an 'aged' quality bonus. Pairs with Farming's fermentation output.
    
- Field Rations (Lv 12, Tier 1): Craft compact ration packs that occupy 1 inventory slot but count as 3 food items. Essential for long expeditions — useful for Survival/combat builds.
    

### 4.10 Combat

Melee, archery, spear, defense, and special combat techniques. Mercenaries and Squires are primary combat classes but all players need basic survival combat skills due to Temporal Storms.

Existing abilities retained: Swordsman, Archer, Spearman, Tank, Defender, Guardian, Tool Mastery, Iron Fist, Monk, Looter, Heavy Armor Expert, Light Armor Expert, Armored Agility, Warrior, Bully, Sniper, Fresh Flesh, Shovel Knight, Adrenaline Rush, Vampire, Drunken Master, Burning Rage, Blood Lust, Monster Expert.

#### New / Modified Abilities

- Tactical Retreat (Lv 7, Tier 2): Short burst of speed when below 40% HP. Tier 2 reduces cooldown. Cross-skill synergy with Survival's Crisis Response.
    
- Equipment Expertise (Lv 10, Tier 2): Reduces durability loss of worn armor. Tier 2 scales with Metalworking skill level (better equipment knowledge = better maintenance).
    
- Temporal Storm Readiness (Lv 12, Tier 2): Reduces temporal stability drain during Temporal Storms. Cross-skill: stacks with Temporal Adaptation skill.
    

### 4.11 Alchemy (NEW)

A brand-new skill tree bridging Farming, Husbandry, Cooking, and Pottery. Alchemists create potions, salves, and reagents used in Engineering and advanced Combat.

Leveling Sources: Brewing potions, extracting essences, distilling tinctures, crafting candles.

**Abilities:**

- Herbalism (Lv 1, Tier 3): Increases yield when harvesting herbs. Cross-skill with Farming Botanical Knowledge.
    
- Crude Extraction (Lv 1, Tier 2): Basic resin/oil extraction from plant matter. Forestry Resin Farmer improves yield.
    
- Alchemist (Lv 5, Tier 1 passive): +40% exp gain from all alchemy actions.
    
- Salve Crafting (Lv 5, Tier 3): Craft healing salves from plant/animal ingredients. Better than bandages but requires Pottery vessels.
    
- Distillation (Lv 7, Tier 2): Use pottery distillation vessels to extract concentrated essences. Required for Tier 2 potions.
    
- Potion Brewing (Lv 8, Tier 3): Brew stat-modifying potions (mining speed, combat damage, carry weight). Each type requires materials from a specific other skill.
    
- Reagent Refinement (Lv 10, Tier 2): Increases the potency of refined reagents. Reduces ingredient waste.
    
- Candle Crafting (Lv 10, Tier 2): Craft long-burn candles from beeswax (Farming) + tallow (Husbandry). Provides superior light compared to torches.
    
- Tincture Mastery (Lv 12, Tier 3): Combine tinctures for compound effects. Requires Alchemy Lv 12 + Cooking Lv 8 + Farming Lv 10.
    
- Philosopher's Extract (Lv 15, Tier 1): Rare reaction that has a small chance to convert base materials to silver/gold traces. Extremely rare, balancing needed.
    
- Grand Transmutation (Lv 20, Tier 1): Legendary ability — craft a unique 'Catalyst' item tradeable for server-tier rewards. Requires Alchemy 20 + Metalworking 15 + Farming 15 + Pottery 12.
    

### 4.12 Engineering (NEW)

A new skill tree covering mechanical contraptions, automation, advanced tools, and structural reinforcement. Built around the Clockmaker/Entropic class but accessible to all.

Leveling Sources: Crafting mechanical parts, building helve hammers, windmills, and gear systems, repairing automated systems.

**Abilities:**

- Mechanical Aptitude (Lv 1, Tier 3): Reduces the material cost of mechanical parts. Cross-skill: Metalworking's Mechanist's Touch improves quality of parts used.
    
- Gear Efficiency (Lv 1, Tier 2): Gear-powered devices run longer before needing maintenance.
    
- Engineer (Lv 5, Tier 1 passive): +40% exp from engineering crafting and device operation.
    
- Contraption Builder (Lv 5, Tier 3): Unlock advanced multi-block contraption blueprints. Cross-skill: requires Metalworking Lv 8 for iron-tier components.
    
- Automated Harvester (Lv 8, Tier 2): Build a device that auto-collects crops in a radius. Cross-skill: device requires Farming Lv 8 to activate and scale with Farming level.
    
- Precision Smithing Jig (Lv 10, Tier 2): Craft jigs that reduce metalworking steps for repeat recipes. Cross-skill: reduces Metalworking exp cost for repeat items.
    
- Steam-Assisted Bellows (Lv 12, Tier 2): Upgrade the bloomery/forge with a bellows device that increases smelting speed. Requires Engineering 12 + Metalworking 10.
    
- Blueprint Mastery (Lv 15, Tier 3): Unlock 3 unique engineering blueprints per tier (9 total) for advanced structures. Blueprints require materials from Mining, Metalworking, and Forestry.
    
- Grand Design (Lv 20, Tier 1): Legendary ability — build a 'Workshop' multiblock structure that grants all nearby players a small exp boost to their primary skill.
    

### 4.13 Masonry (NEW)

A new skill tree focused on stone crafting, road building, structural reinforcement, and architectural permanence. Designed to match the Mason class added in Aldi's RP Patch.

Leveling Sources: Placing stone blocks, crafting stone blocks, building roads/paths, reinforcing structures.

**Abilities:**

- Stonemason (Lv 1, Tier 3): Increases yield when cutting stone. Cross-skill with Mining Stonecutter.
    
- Foundation Layer (Lv 1, Tier 2): Reduces material cost for placing structural foundation blocks.
    
- Mason (Lv 5, Tier 1 passive): +40% exp from all masonry actions.
    
- Road Builder (Lv 5, Tier 2): Unlocks stone path and cobblestone road recipes. Road blocks placed by this player grant Trail Blazer bonuses to all nearby players.
    
- Mortar Mixing (Lv 5, Tier 3): Craft reinforced mortar from limestone + clay. Used in advanced structural recipes. Requires Digging Lv 5.
    
- Arch Engineering (Lv 8, Tier 2): Unlock decorative arch and vault block recipes unique to Mason class.
    
- Structural Analysis (Lv 10, Tier 2): Nearby structures (within 16 blocks) gain a small damage resistance bonus. Useful for fortified settlements.
    
- Quarry Expertise (Lv 12, Tier 2): Quarried stone blocks have a chance to yield carved stone slabs as byproduct. Cross-skill: Pottery benefits from fired stone components.
    
- Grand Monument (Lv 18, Tier 1): Legendary ability — build a monument multiblock that grants a server-wide visible marker and nearby settlement bonus.
    

## 5. Cross-Skill Synergy Map

The following table summarizes the key dependency relationships between skills. A -> B means skill A produces materials or unlocks features that skill B depends on for high-tier progression.

---

**Provider Skill** **Dependent Skill** **Nature of Synergy**

---

Mining Metalworking Ore supply for all smelting tiers

Mining Engineering Raw materials for mechanical components

Forestry Metalworking Charcoal fuel for smelting

Forestry Alchemy Resin/bark inputs for extracts and candles

Forestry Engineering Timber for contraption frames and windmills

Digging Mining Saltpeter for advanced explosives

Digging Pottery Clay supply for all kiln-fired products

Digging Masonry Dense clay blocks for advanced masonry

Pottery Alchemy Sealed vessels and distillation pots for brewing

Pottery Cooking Storage crocks and cooking vessels

Farming Cooking Crop ingredients for all food recipes

Farming Alchemy Herbs and rare cultivars for potions

Farming Husbandry Composting loop — manure improves crop yield

Husbandry Cooking Meat, dairy, eggs for high-tier recipes

Husbandry Alchemy Animal glands/bile for advanced reagents

Metalworking Engineering High-quality mechanical parts

Metalworking Combat Better tool/weapon tiers available

Alchemy Combat Potions for buffs and healing

Alchemy Survival Healing salves as alternatives to bandages

Masonry Survival Roads enable Trail Blazer movement speed bonus

Cooking Survival High-saturation foods extend all skill XP gains

Engineering Farming Automated harvester device for large farms

## Temporal Adaptation Mining/Combat Stability bonuses for storm survival

## 6. Technical Architecture

### 6.1 Module Structure

The mod will be structured as a C# Vintage Story mod with the following namespace layout:

- XSkillsReplacement.Core — XP engine, level calculation, event hooks
    
- XSkillsReplacement.Skills — One class per skill discipline, inheriting from BaseSkill
    
- XSkillsReplacement.Abilities — One class per ability, inheriting from BaseAbility
    
- XSkillsReplacement.GUI — Enshrouded-style skill tree renderer using VS's GuiComposer
    
- XSkillsReplacement.Config — JSON config loading (mirrors existing x-skills JSON structure)
    
- XSkillsReplacement.Network — Delta-sync packets, server<->client skill state
    
- XSkillsReplacement.ClassIntegration — Aldi's Classes exp multiplier hooks
    

### 6.2 Performance Strategy

- Event-driven: All XP triggers use VS event delegates (BlockBroken, EntityDied, ItemCrafted, etc.) — no per-tick polling
    
- Caching: Player skill state is cached in a Dictionary<string, SkillState> per player — refreshed on level-up or config reload only
    
- Config lazy loading: Ability configs are loaded on first access per skill, not at startup
    
- Network efficiency: Only the changed skill's delta is broadcast on XP gain, not the full skill state
    
- GUI: Skill tree rendered on client-side only; server sends only raw numbers
    

### 6.3 Config File Format

The existing JSON config format from X-Skills is preserved for backwards compatibility. New fields will be additive only:

- synergySources: list of skill IDs that provide a bonus to this skill's XP
    
- prerequisiteSkills: map of ability name to required {skillId, minLevel} for cross-skill unlocks
    
- guiPosition: optional {x, y} override for ability node placement in the skill tree GUI
    

### 6.4 GUI Design

The skill tree GUI takes heavy inspiration from Enshrouded's node-based progression system:

- Dark charcoal background (#1A1A2E) with subtle texture
    
- Skill nodes represented as hexagonal icons with glowing borders (color-coded by skill)
    
- Connection lines between related/prerequisite nodes — lit when unlocked, dim when locked
    
- Tier indicators: small gems/dots beneath each node icon (up to 3)
    
- Tooltip on hover: ability name, description, current tier values, next tier values, unlock requirements
    
- Top bar: skill name, current level, XP bar, class bonus indicator
    
- Tab strip: one tab per skill discipline, icon-only for compact display
    

## 7. Development Milestones

---

**Phase** **Name** **Deliverables** **Est. Effort**

---

1 Core Engine XP system, level calc, event hooks, config loading, network sync High

2 Existing Skills Port Port all 10 existing X-Skills to new architecture (Mining–Temporal Adaptation) Medium

3 New Skills Implement Alchemy, Engineering, Masonry skill trees High

4 Cross-Skill Hooks Implement all synergy triggers (prereqs, material unlocks, shared buffs) High

5 GUI — Basic Tab strip, skill panels, basic node layout, XP bars Medium

6 GUI — Polish Enshrouded-style node renderer, connection lines, tooltips, animations High

7 Class Integration Aldi's Classes multiplier hooks, class-specific ability gates Medium

8 Balancing Pass XP curve tuning, cross-skill prerequisite level tuning, server testing Ongoing

## 9 QA & Release Server stress test, config documentation, release packaging Low

## 8. Open Questions & Decisions Needed

1. Specialization Limit: xleveling.json sets specialisationLimit: 1. Should this be raised to 2 to allow dual-specialization builds, or does the economy benefit from keeping it at 1?
    
2. Unlearn Cooldown: Currently 120 minutes. With deeper cross-skill investment, respeccing becomes more consequential. Should this be raised to 24 hours for RP servers?
    
3. Legendary Abilities (Lv 18-20): Should Grand Transmutation, Grand Design, and Grand Monument require server-admin approval or player trading to activate?
    
4. Alchemy Scope: Should Alchemy potions provide PvP-relevant buffs, or only PvE/utility buffs to avoid balance issues? (enableAbilitiesInPvP is currently False for Combat.)
    
5. Engineering Scope: How deep should automation go? A fully automated farm could undermine the multiplayer economy. Consider capping automated device count per player.
    
6. Masonry vs Digging Overlap: Both skills deal with stone/clay. Should Masonry be a separate skill file or a high-level branch within Digging?
    
7. Tailor Class Gap: Aldi noted Threadweaver/Tailor is underserved. Could Alchemy or Engineering have sub-branches that benefit tailoring/fiber crafting specifically?
    

_X-Skills Replacement — Internal Project Document | Draft v1.0 | March 2026_