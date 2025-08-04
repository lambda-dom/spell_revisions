Not just things to (still) do but also proposed changes to spells.

# A. Divine spells.

## A. 1. Level 1.

* Armor of Faith: restore resistances of old spell.

* Entangle: current implementation is incorrect as the decrease movement applies to all creatures, including those that should be immune. Solution: if we want to use the subspell (and we should), we may need another spell to decrease speed and then call the subspell or simply patch the subspell.

* Goodberry: scaling, slow regenerating effect of 1 hp for round. Only castable outdoors and ooc.

* Find Familiar: yet to implement.

## A. 2. Level 2.

* Chant: have good chant nullify bad chant and vice versa.

## A. 3. Level 3.

* Dispel Magic: only the description is in.

* Spike Growth: remove save from movement set for parity with entangle.

## A. 4. Level 4.

* Animal Summoning IV: only description is in.

* Free Action: temp immunities are in but not curing them. Movement Rate 2 immunity dropped for now.

* Death Ward: standardize immunities to instant death and disintegrate.

* Call Woodland Beings: only description is in.

* Negative Plane Protection: description says abjuration, spell says transmutation: went with description for now. No sectype; vanila is combination.

# B. Arcane spells.

## B. 1. Level 1.

* Grease: follow implementation of Entangle? Use a sleep subspell? Also increase aoe.

* Sleep: display "ineffective spell" for creatures with dice > caster level.

* Spook: True Seeing makes one immune to Spook and this is handled in the True Seeing spell. Better to add a TRUE_SIGHT state to splstate.ids, set it via Set Spell State [328] in True Seeing and then use the usual shenanigan in Spook (e. g. 318) to make True Seeing nullify it. This spell state is apparently missing and is being set via proficiencies, but these are not detected via 318 and related opcodes (or at least I do not know how).

## B. 2. Level 2.

* Battering Ram: move unconsciousness from knockback to its own subspell? This would need weidu_library patching.

## B. 3. Level 3.

* Dispel Magic: only the description is in.

* Remove magic: reinstate, with old icon but targetiing everyone (that is remove magic becomes old dispel magic).

* Protection from Missiles: Externalize the missiles table (e. g. copy it to weidu_external and offer functions as a modder resource to use it). Needs a pass over missing projectiles.

* Skull Trap: has an extra protection for swords. Undocumented but to be decided.

* Vampiric Touch: I am not sure the flags have been chosen correctly or even if they can be so shosen, and by this I mean: do damage per amount + dice, maybe capped by max hp of target. Absorb only up to maximum hp. Concurrency with other Vampiric Touches must also be addressed (e.g. spin106).

* Protection from Fire and Cold: not yet done as these are moved to level 4.

* Melf's meteors: description says evocation school, spell says conjuration. Going with description for now.

# C. General.

* Handle replacements: for now, they are just new spells, but they should replace old which implies doing surgery on `spell.ids`.

* Cure line of spells: mention in description that it also cures intoxication.

* Regenerate line of spells: handle inter-spell concurrency. The idea is that higher level remove and block lower level.

* Self-stacking debuffs: debuffs like Slow stack with themselves if not protected against -- this is achieved by a Protection from Spell [206] opcode and *not* by refreshing. The reason is that the debuffs apply on a failed save so it could happen that the refresh would clean the applied debuff and then fail to apply its effects due to a successful save. In the case of Slow, the problem is sharper because the debuff is applied via sectype, so while it does not stack with itself it will stack with other instances of the sectype. For now this is how it is done, but this ought to be revisited.

note(s):
* up to level 3 debuffs should also be revisited to see if they follow the rule.

* Armor line of spells: concurrency not handled yet.

* Display strings: this has only be handled in a small number of spells.

* Cre scripts: set them in the patches instead of relying on name synchronicity.
