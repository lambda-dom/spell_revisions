Fixes to base SR, v4.19.

# A. Divine spells.

## A. 1. Level 1.

* Animal Summoning I: the thac0 and saves of bats in the cre file and description disagree. Went with the description.

* Armor of Faith: changed portrait icon to EE Armor of Faith.

* Cause Light Wounds: Fix?? item of enchant level 1 -> 7, but this has to be re-checked, especially against protections like PfMW.

* Detect Alignment: -> know alignment and fixed wrong level in the docs.

* Faerie Fire: Question: why the variable stuff?

* Goodberry: power of opcodes in items 2 -> 0, resist_dispel 3 -> 0.

## A. 2. Level 2.

* Animal Summoning 2: Fix?? drop sectype on dog scent. Fix int 6 -> 4 (hps 16 and ac 6, due to con and dex mods? recheck). AC of war dogs disagrees in the cre file and the description. Went with the description.

* Chant: implementation changed to put the buff in an aux spell of its own. Aux spells special and at level 1. Add string display for evil chant. Fix sectypes on aux.

* Charm Person or Animal: fix off-by-1 errors in probability.

* Find Traps: Fix sectypes on aux.

* Resist Elements: Fix: description sectype abjuration -> transmutation in description.

* Flame Blade: Fix: give scimitar prof to flame blades.

* Spiritual Hammer: Fix: give hammer prof to spiritual hammers. Move spell to item block (this was only needed in oBG because of the next item); drop undocumented golem immunity to magic damage. Dropped aux spell that also has spurious (?) sectype. Fix weight 2 -> 0.

* Cause Moderate Wounds: Fix?? Stick power of cast spell opcode 1 -> 0 for consistency with cause light wounds.

# B. Arcane spells.

## B. 1. Level 1.

* Armor: changed protection against self -> refresh. Protection against other armor spells dropped. The idea here is to let higher level spells cancel and replace lower-level but not the other way around.

* Burning Hands: change last line of description slightly to explicitly mention the last level.

* Color Spray: SR overrides the original `cspray.pro` spell, but I do not know what are the exact changes implemented by SR. We do not override, but simply add a whole new projectile.

* Chromatic Orb: fix description to mention that poison lasts for 3 rounds.

* Grease: Added Mist and Illusionary to the immunities. The duration is 7, not the expected (by me at least) duration 6 of one round. In the forums, Kjeron mentioned that periodic (via the projectile) tick spells are a complicated matter. Sometimes overreach is needed, sometimes it is not.

* Sleep: fix off-by-1 errors in probability.

* Monster Summoning I: the thac0 of gibberlings in the cre file and description disagree. Went with the description.
