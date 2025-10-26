Fixes to base SR, v4.19.

# A. Divine spells.

## A. 1. Level 1.

* Animal Summoning I: correction of bats: thac0, saves (went with the description).

* Armor of Faith: changed portrait icon to EE Armor of Faith.

* Cause Light Wounds: item of enchant level 1 -> 7, but this has to be re-checked, especially against protections like PfMW.

* Detect Alignment: -> know alignment and fixed wrong level in the docs.

* Entangle: area slow movement rate subject to same immunities as entangle proper.

* Faerie Fire: Question: why the variable stuff?

* Goodberry: power of opcodes in items 2 -> 0, resist_dispel 3 -> 0.

* Sunscorch: change damage dice sides to d4.

## A. 2. Level 2.

* Animal Summoning 2: drop sectype on dog scent. War dogs: correct int, hps and ac (went with the description).

* Chant: implementation changed to put the buff in an aux spell of its own. Aux spells special and at level 1. Add string display for evil chant. Fix sectypes on aux.

* Charm Person or Animal: fix off-by-1 errors in probability.

* Find Traps: Fix sectypes on aux.

* Resist Elements: Fix: description sectype abjuration -> transmutation in description.

* Flame Blade: Fix: give scimitar prof to flame blades and added modify profs opcode. Corrected spepd factor to take into account enchantment.

* Spiritual Hammer: Fix: give hammer prof to spiritual hammers and added modify profs opcode. Move spell to item block (this was only needed in oBG because of the next item); drop undocumented golem immunity to magic damage. Dropped aux spell that also has spurious (?) sectype. Fix weight 2 -> 0. Fix range description.

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

* Negative Plane Protection: description says abjuration, spell says transmutation: went with description.

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

* Conjure Fire Elemental: fire elemental: ac 4 -> 1, thac0 10 -> 7, general monster; fists damage bonus 3 -> 4. Greater fire elemental: ac 4 -> 0, thac0 7 -> 3, general monster; fists damage bonus 3 -> 5.

* Conjure Earth Elemental: earth elemental: thac0 11 -> 4, hps 126 -> 116. Fist: document mr penalty. damage bonus 3 -> 12. Greater earth elemental: thac0 8 -> 0. Fist: document mr penalty. damage bonus 3 -> 14, dice size 10 -> 8.

* Conjure Air Elemental: ac 4 -> 0, thac0 8 -> 5. Fist: document mr bonus. damage bonus 3 -> 4. Greater air elemental: ac 4 -> -1, thac0 5 -> 1. Fist: document mr penalty. damage bonus 3 -> 5.

* Fire Seeds: +6 -> +4 enchantment. Added dart prof so that characters with it can use it.

* False Dawn: spurious cast spell opcode.

* Animate Skeleton Warrior: standardized immunities. Damage bonus 1 (corrected description). Corrections to thac0.

## A. 7. Level 7.

* Summon Shambling Mound: remove undocumented -25% magic damage penalty. Fix damage bonus 3 -> 10. `dvmound1` non-existent spell, made it into recursive call. Fix thac0 8 -> 2. General gianthumanoid -> monster.

* Chaos: renamed back to Sphere of Chaos vanilla to improve compatibility.

* Finger of Death: correct save penalty -4 to -2 per description.

* Holy Word: change sectype conjuration -> disabling.

* Regeneration: fix description: speed 6 -> 7 per implementation.

* Resurrection: fix range 10 -> 1 per description.

* Unholy Word: change sectype none -> disabling.

* Animal Summoning 7: Polar Bear: non-magical; damage bonus 0 -> 11. Polar Bear: charisma 10 -> 8, thac0 12 -> 8.

* Symbol of Stunning: range 70 -> 30.

* Symbol of Death: range 70 -> 30.

* Earthquake: sectype offensivedamage -> battleground.

# B. Arcane spells.

## B. 1. Level 1.

* Armor: changed protection against self -> refresh. Protection against other armor spells dropped. The idea here is to let higher level spells cancel and replace lower-level but not the other way around.

* Burning Hands: change last line of description slightly to explicitly mention the last level.

* Color Spray: SR overrides the original `cspray.pro` spell, but I do not know what are the exact changes implemented by SR. We do not override, but simply add a whole new projectile.

* Chromatic Orb: fix description to mention that poison lasts for 3 rounds.

* Grease: Added Mist and Illusionary to the immunities. The duration is 7, not the expected (by me at least) duration 6 of one round. In the forums, Kjeron mentioned that periodic (via the projectile) tick spells are a complicated matter. Sometimes overreach is needed, sometimes it is not.

* Sleep: fix off-by-1 errors in probability.

* Monster Summoning I: gibberlings: correct thac0 (per description).

* Chill Touch: Removed undispellable flag from item.

* Dimension Jump: correct range in description.

* Know Alignment: casting speed 2 -> 1 per level 1 spell.

## B. 2. Level 2.

* Resist Fear: casting speed 2 for consistency.

* Ghoul Touch: fix description to mention that paralyze lasts for 3 rounds only. Sectype (of main spell) to `offensivedamage` for consistency with similar spells. Removed undispellable flag from item.

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

* Enchanted Weapon: weight set to 0 as per description. We also set to 0 the strength requirements.

* Polymorph Other: standardized range to long per description (40 -> 30). The SR implementation goes by creating an item in the weapon slot that does the animation and stat changes. Polymorph opcode is not used (is bugged in the EEs per the IESDP).

* Simbul Spell Matrix: out of combat only.

* Monster Summoning IV: Correct description on the amount of poison damage (3 -> 2) and damage bonuses on both stings. Correct probability of poison (20 -> 100) on sword spider sting. Standardized implementation of immunities. Giant Spider: corrections to ac, thac0 and saves. Sword spider: corrections to thac0 and saves.

* Fire Shield: sectype offensivedamage -> specificprotections.

* Secret Word: school enchant (description) -> abjuration.

* Minor Spell Sequencer: out of combat only. 

## B. 5. Level 5.

* Summon Shadow: Shadow: added immunities to fear and fatigue; standardized immunities. Missing save on opcode in shadow touch. Corrections to thac0. Wraith: added immunities to fear and fatigue; standardized immunities and dropped blindness immunity. Standardized level drain. Corrections to thac0, ac. Range of spell long -> medium.

* Cloudkill: fixed levels on the slay opcodes.

* Monster Summoning V: correct ridiculous damage bonus 9 -> 3, 1. Ogre Berserker: corrections to thac0, hps. Ogre Mage: corrections to int, wis, chr, hps, ac, thac0, saves.

* Hold Monster: use subspells?

* Dispelling Screen: undocumented bonus of mr (patched out later?).

* Breach: range 40 -> 30 per description (Long).

* Phantom Blade: correct damage to undead. Moved prof opcode to it. Fixed thac0 bonus 4 -> 8 (+4 plus melee +4).

* Conjure Elemental: standardized duration to 2 turns (= level 10 in old spell) instead of 3 to accentuate "difficult to maintain portal" blurb. Fix off-by-1 probability errors. Air Elemental: added polymorph immunity per other elementals. Corrections to ac, thac0. Added 50% electricity resistance. Earth elemental: corrections to ac, thac0. Fire elemental: corrections to ac, thac0. Giant humanoid -> monster.

## B. 6. Level 6.

* Invisible Stalker: corrections to int and wis; thac0. Damage bonus on fists 2 -> 4. Corrections to immunities as per description: remove fear, fatigue, berserk and added sleep.

* Improved Haste: missing remove of haste sectype. Spell sectype is set but (unless I am mistaken) should be none.

* Contingency: out of combat only.

* Chain Lightning: main target spell scales at one level less than it should.

* Disintegrate: power of Use Eff [177] 5 -> 6.

* Conjure Elemental: standardized duration to 2 turns (= level 10 in old spell) per lesser version.

* Monster Summoning VI: Baby wyvern: sting damage bonus 1 -> 3. Document sting is only 25% chance and fix one-off error. Corrections to str 19 -> 17, thac0 14 -> 12. Wyvern: thac0 13 -> 8, save vs. spell 10 -> 14, wyvern sting damage bonus 2 -> 9. Document sting is only 25% chance and fix one-off error.

* Summon Nishruu: standardize to fixed 1 turn. Description level 7 -> 6. thac0 11 -> 7. Mention constant detect invis. Contact: correct enchant 0 -> 3 and thac0 bonus; correct item flags. Fix ridiculous feeblemindedness duration.

* Animate Skeleton Warrior: see level 6 Cleric version.

## B. 7. Level 7.

* Monster Summoning 7: Otyugh: thac0 13 -> 10.

* Mordenkainen's Sword: Sword: fix dice 4d5 -> 5d4. Removed add strength bonus. Implemented mind immunities directly. Corrections to thac0 6 -> 2. Script: remove detect illusions block copied from nishruu which is used to implement vulnerability to dispel.

* Mass Invisibility: range 35 -> 30.

* Death Knight: sword: make a real sword, thac0 bonus 4 -> 3, damage bonus 5 -> 11. Death knight: thac0 7 -> 1, apr 2 -> 3.

* Summon Efreeti: sword: make a real sword, damage bonus 4 -> 10. Efreet: increase first class 9 -> 10, str 18/00 -> 19, wis 15 -> 14, hps 80 -> 98, ac 4 -> 1, thac0 10 -> 5, apr 3/2 -> 2, saves wand 8 -> 11, saves spell 7 -> 11, neutral -> ally, gender male -> summoned.

* Summon Djinni: sword: make a real sword, remove apr bonus (move to cre), damage bonus 4 -> 5. Djinni: increase first class 9 -> 10, wis 15 -> 14, hps 70 -> 89, ac 5 -> 0, thac0 10 -> 7, apr 3/2 -> 3, neutral -> ally, gender male -> summoned.

* Summon Hakeashar: fix icons. Swap the contact with the nishruu to give hakeashar the better version. thac0 4 -> 2, allegiance enemy -> ally. Fix eff that summons nishruu -> hakeashar.

* Chaos: renamed sphere of chaos for compatibility with the wizard version. The description already contains sphere talk in it so this is lore justified.

## B. 8. Level 8.

* Pierce Shield: range 40 -> 30.

* Moment of Prescience: there is an ac vs. all bonus 10 contradicting the 20 bonus. Is this a mistake? For now assuming yes.

* Summon Fiend: Glabrezu pincers: damage bonus 4 -> 12. Creature: Hps 100 -> 160, thac0 8 -> 1, apr 3 -> 4

* Bigby's Icy Grasp: range 35 -> 30.

* Umber Hulk: Claws: damage bonus 3 -> 11. Creature: dice 7 -> 8, thac0 13 -> 6. Undocumented physical resistances 5 (missile 100) -> 0.

## B. 9. Level 9.

* Black Blade of Disaster: add prof opcode. This should not make a real difference as thac0 is set to 0.

* Pit Fiend: review fire spell protections on weapon (and maybe move them to ring). Damage bonus 4 -> 16. Fix probabilities out of whack, duration of disease display string. Change constrict save to vs. breath. Creature: hps 120 -> 170, ac -6 -> -7, thac0 5 -> -7, apr 4 -> 5.
