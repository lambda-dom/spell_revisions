Fixes to base SR, v4.19.

# A. Divine spells.

## A. 1. Level 1.

* Animal Summoning I: correction of bats: thac0, saves (went with the description).

* Armor of Faith: changed portrait icon to EE Armor of Faith.

* Cause Light Wounds: item of enchant level 1 -> 7, but this has to be re-checked, especially against protections like PfMW.

* Detect Alignment: -> know alignment and fixed wrong level in the docs.

* Faerie Fire: Question: why the variable stuff?

* Goodberry: power of opcodes in items 2 -> 0, resist_dispel 3 -> 0.

## A. 2. Level 2.

* Animal Summoning 2: drop sectype on dog scent. War dogs: correct int, hps and ac (went with the description).

* Chant: implementation changed to put the buff in an aux spell of its own. Aux spells special and at level 1. Add string display for evil chant. Fix sectypes on aux.

* Charm Person or Animal: fix off-by-1 errors in probability.

* Find Traps: Fix sectypes on aux.

* Resist Elements: Fix: description sectype abjuration -> transmutation in description.

* Flame Blade: Fix: give scimitar prof to flame blades.

* Spiritual Hammer: Fix: give hammer prof to spiritual hammers. Move spell to item block (this was only needed in oBG because of the next item); drop undocumented golem immunity to magic damage. Dropped aux spell that also has spurious (?) sectype. Fix weight 2 -> 0.

* Gust of Wind (druid version): mention in description that it dispels insect swarms in the area.

* Cause Moderate Wounds: stick power of cast spell opcode 1 -> 0 for consistency with cause light wounds.

## B. 3. Level 3.

* Animate Dead: greater skeleton: gender niether -> summoned (todo: this may be incorrect). Align neutral -> chaotic evil. Wis 11 -> 10. Charisma is also 9 instead of 1. Correct saves vs. death 0 -> 9. Charisma 1 -> 3 as currently, the implementation requires a minimum of 3. Corrections to ac and thac0. Correct damage bonus on mace and skeleton great sword 1 -> 2. Added 233 opcodes for proficiency. Undead immunities: fear, fatigue, berserk, charm, confusion, disease, hold, level drain, petrification, poison, stun, sleep, death: corrected description and implemented correctly via blocks library.

note(s):
* shield has an ac bonus of 2, but is classified as a buckler.

* Magic fang: the implementation is geared for old BG, with a convoluted method using Create Weapon [111]. In EE, we can use Enchantment Bonus [345] to vastly simplify the implementation. Extended spell to also monsters.

* Miscast Magic: implementation was incorrect, as it was only granting a save in the first two rounds.

* Unholy Blight: fix stacking of saves and thac0 penalty.

* Icelance: standardized hold to a subspell; does *not* use hold creature 2 opcode.

* Animal Summoning III: corrections to wolf summon: int, ac, thac0.

## A. 4. Level 4.

* Free Action: tightened implementation of immunities.

* Cause Critical Wounds: correct damage of level 10 header 36 -> 40.

* Animal Summoning IV: leopard claws missing +1 damage bonus. Leopard: corrections to wis, chr, ac. Corrections to pounce (+2 bonus instead of +4).

* Call Woodland Beings: hamadryad: correct ac, thac0, apr, saves (per description). Remove dire charm and dimension door. Nymph: ac, saves (per description), magic resistance bonus missing, incorrect alignment.

## A. 5. Level 5.

* Animal Summoning V: snake: corrections to ac, str, dex, con.

* Cure Mortal Wounds: casting speed 7 -> 5. Scaling 5 per level.

* Cause Mortal Wounds: same scaling as cure mortal wounds.

* Animal Growth: fixes to range (harmless) and casting speed. Fix target caster -> actor. Extended to monsters.

## A. 6. Level 6.

* Aerial Servant: add normal invis to fists. Fix damage bonus. Added polymorph per other elementals. Corrections to thac0 and ac. Deleted spurious immunity to maze opcode. Deleted spurious servsu.bcs script.

* Animal Summoning VI: cave bear: corrections to damage bonus in claws. Corrections to thac0.

* Conjure Elemental: standardized duration to 2 turns (= level 10 in old spell) per wizard lesser version.

* Fire Seeds: +6 -> +4 enchantment. Added dart prof so that characters with it can use it.

* False Dawn: spurious cast spell opcode.

* Animate Skeleton Warrior: standardized immunities. Damage bonus 1 (corrected description). Corrections to thac0.

# B. Arcane spells.

## B. 1. Level 1.

* Armor: changed protection against self -> refresh. Protection against other armor spells dropped. The idea here is to let higher level spells cancel and replace lower-level but not the other way around.

* Burning Hands: change last line of description slightly to explicitly mention the last level.

* Color Spray: SR overrides the original `cspray.pro` spell, but I do not know what are the exact changes implemented by SR. We do not override, but simply add a whole new projectile.

* Chromatic Orb: fix description to mention that poison lasts for 3 rounds.

* Grease: Added Mist and Illusionary to the immunities. The duration is 7, not the expected (by me at least) duration 6 of one round. In the forums, Kjeron mentioned that periodic (via the projectile) tick spells are a complicated matter. Sometimes overreach is needed, sometimes it is not.

* Sleep: fix off-by-1 errors in probability.

* Monster Summoning I: gibberlings: correct thac0 (per description).

## B. 2. Level 2.

* Ghoul Touch: fix description to mention that paralyze lasts for 3 rounds only. Sectype (of main spell) to `offensivedamage` for consistency with similar spells.

* Glitterdust: Question: why the variable stuff?

* Mirror Image: concurrent refresh with lower level reflected image.

* Power Word Sleep: fix off-by-1 errors in probability. Add immunities to golem, slime, sword and illusionary.

* Resist Elements: fix: drop sphere line in description and description sectype abjuration -> transmutation.

* Stinking Cloud: add immunity to (mordenkainen) swords and illusionary creatures.

* Strength: make it refreshing to not stack exceptional strength increment.

* Web: add immunity to mephits.

* Monster Summon II: fix: remove spurious poison icon from jelly pod. Fix int, wis, chr, acid resistance according (per description). Fix lack of immunities to disease and sleep. Fix poorly implemented immunities.

## B. 3. Level 3.

* Clairvoyance: correction of power in saves opcode.

* Non-detection: protection from spell type divinationattack.

* Protection from Missiles: externalized the projectiles that spell defends against. Fixed flame arrow projectile. Needs a pass over missing projectiles.

* Dire Charm: correction of off-by-one probability.

* Ghost Armor: added bonus to move silently.

* Monster Summoning III: Correction to the dice of bastard sword. Corrections to shaman: hps.

## B. 4. Level 4.

* Confusion: standardized range to long per description (35 -> 30).

* Polymorph Other: standardized range to long per description (40 -> 30). The SR implementation goes by creating an item in the weapon slot that does the animation and stat changes. Polymorph opcode is not used (is bugged in the EEs per the IESDP).

* Simbul Spell Matrix: out of combat only.

* Monster Summoning IV: Correct description on the amount of poison damage (3 -> 2) and damage bonuses on both stings. Correct probability of poison (20 -> 100) on sword spider sting. Standardized imlpementation of immunities. Giant Spider: corrections to ac, thac0 and saves. Sword spider: corrections to thac0 and saves.

* Fire Shield: sectype offensivedamage -> specificprotections.

* Secret Word: school enchant (description) -> abjuration.

* Minor Spell Sequencer: out of combat only. 

## B. 5. Level 5.

* Summon Shadow: Shadow: added immunities to fear and fatigue; standardized immunities. Missing save on opcode in shadow touch. Corrections to thac0. Wraith: added immunities to fear and fatigue; standardized immunities and dropped blindness immunity. Standardized level drain. Corrections to thac0, ac. Range of spell long -> medium.

* Monster Summoning V: correct ridiculous damage bonus 9 -> 3, 1. Ogre Berserker: corrections to thac0, hps. Ogre Mage: corrections to int, wis, chr, hps, ac, thac0, saves.

* Dispelling Screen: undocumented bonus of mr (patched out later?).

* Breach: range 40 -> 30 per description (Long).

* Phantom Blade: correct damage to undead. Moved prof opcode to it.

* Conjure Elemental: standardized duration to 2 turns (= level 10 in old spell) instead of 3 to accentuate "difficult to maintain portal" blurb. Fix off-by-1 probability errors. Air Elemental: added polymorph immunity per other elementals. Corrections to ac, thac0. Added 50% electricity resistance. Earth elemental: corrections to ac, thac0. Fire elemental: corrections to ac, thac0. Giant humanoid -> monster.

## B. 6. Level 6.

* Invisible Stalker: corrections to int and wis; thac0. Damage bonus on fists 2 -> 4. Corrections to immunities as per description: remove fear, fatigue, berserk and added sleep.

* Improved Haste: missing remove of haste sectype. Spell sectype is set but (unless I am mistaken) should be none.

* Chain Lightning: main target spell scales at one level less than it should.

* Disintegrate: power of Use Eff [177] 5 -> 6.
