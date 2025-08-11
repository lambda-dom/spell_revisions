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

* Animate Dead: gender "summoned" on skeletons may be incorrect. Double check.

* Dispel Magic: only the description is in.

* Spike Growth: remove save from movement set for parity with entangle.

## A. 4. Level 4.

* Free Action: immunities are in but not curing them. Movement Rate 2 immunity dropped.

* Death Ward: standardize immunities to instant death and disintegrate.

* Negative Plane Protection: description says abjuration, spell says transmutation: went with description. No sectype; vanila is combination.

## A. 5. Level 5.

* Cure Mortal Wounds: Implement immunity for non-living and extra-planar or delete from description?

* True Seeing: there is a protection from the cloak of mirroring -- drop it if needed. Aux spell only removes illusion school spells up to level 2; remove illusionary protections of all levels? Missing protection against shadow door.

* Chaotic Commands: standardize immunities (probably will need append_block support from weidu_library).

* Cause and Cure Mortal Wounds: extend scaling to level 15?

* Greater Command: move sleep to subspell.

* Protection from Acid: add protection to Vitriolic Sphere or not needed?

* Protection from Cold: only protectiom from wizard's cone of cold and icestrom. Add other.

* Protection from Fire: missing protections (e. g. aux flame arrow).

* Elemental protection: do the same dance as with wizard's protection from elemental energy.

* Mass Regenerate: currently non-stacking. SR adds non-concurrent stacking, but is it needed?

* Harper's Call: to do. Drop the penalties and make it out of combat only.

## A. 6. Level 6.

* Aerial Description: only description in.

* Conjure Fire Elemental: only description in.

* False Dawn: move blindness to subspell.

# B. Arcane spells.

## B. 1. Level 1.

* Grease: follow implementation of Entangle? Use a sleep subspell? Also increase aoe.

* Sleep: display "ineffective spell" for creatures with dice > caster level.

* Spook: True Seeing makes one immune to Spook and this is handled in the True Seeing spell. Better to add a TRUE_SIGHT state to splstate.ids, set it via Set Spell State [328] in True Seeing and then use the usual shenanigan in Spook (e. g. 318) to make True Seeing nullify it. This spell state is apparently missing and is being set via proficiencies, but these are not detected via 318 and related opcodes (or at least I do not know how).

## B. 2. Level 2.

* Battering Ram: move unconsciousness from knockback to its own subspell? This would need weidu_library patching.

## B. 3. Level 3.

* Dispel Magic: only the description is in.

* Remove magic: reinstate, with old icon but targeting everyone (that is remove magic becomes old dispel magic).

* Protection from Missiles: Externalize the missiles table (e. g. copy it to weidu_external and offer functions as a modder resource to use it). Needs a pass over missing projectiles.

* Skull Trap: has an extra protection for swords. Undocumented so dropped for now, but to be revisited.

* Vampiric Touch: I am not sure the flags have been chosen correctly or even if they can be so chosen, and by this I mean: do damage per amount + dice, maybe capped by max hp of target. Absorb only up to maximum hp. Concurrency with other Vampiric Touches must also be addressed (e.g. spin106).

* Protection from Fire and Cold: not yet done as these are moved to level 4.

* Melf's meteors: description says evocation school, spell says conjuration. Going with description for now.

## B. 4. Level 4.

* Blue Shield: reinstate it.

* Mestil's Acid Shield: replaces cold shield but we are reinstating it. Spell itself is not in (and is in level 5).

* Minor Glove of Invulnerability: pass through area spells of level <= that must be protected against. Externalize like with PfM?

* Otiluke Resilient Sphere: only description is in.

* Spirit Armor: handle concurrency with other armor spells.

* Polymorph other: aux resources do not seem to be used anywhere.

* Enchant weapon: the basic spell is in but the items are missing proper descriptions and the spell, descriptions and ability icons.

* Monster Summoning IV: cre and script for phase spider unused.

* Wizard Eye: change from non-stacking to refreshing? Review creature.

## B. 5. Level 5.

* Shadow Summon: refactor immunities by reusing undead immunities and moving everything else to the touch.

* Monster Summon 5: Ogre Mage casts haste not slow which he does not have; does not use invis at will which is not memorized anyway.

* Shadow Door: add a True Seeing state so that we can put immunity to the spell in the spell itself (see Spook above).

* Waves of Fatigue: add immunity for "non-living" (undead, elementals, constructs, etc.).

* Dispelling Screen: the base spell makes no sense so have to implement the patching.

* Conjure (Lesser) Elemental: Add water elemental and consolidate all spells in one.

* Spell Deflection: add display string.

# C. General.

* weidu_library stuff: (1) re-order saves in cre tables to align with standard ordering for better comparison. (2) type the fields like those requiring tra refs by making the default -1 instead of *.

* Handle replacements: for now, they are just new spells, but they should replace old which implies doing surgery on `spell.ids`.

* Cure line of spells: mention in description that it also cures intoxication.

* Regenerate line of spells: handle inter-spell concurrency. The idea is that higher level remove and block lower level.

* Self-stacking debuffs: debuffs like Slow stack with themselves if not protected against -- this is achieved by a Protection from Spell [206] opcode and *not* by refreshing. The reason is that the debuffs apply on a failed save so it could happen that the refresh would clean the applied debuff and then fail to apply its effects due to a successful save. In the case of Slow, the problem is sharper because the debuff is applied via sectype, so while it does not stack with itself it will stack with other instances of the sectype. For now this is how it is done, but this ought to be revisited.

note(s):
* up to level 3 debuffs should also be revisited to see if they follow the rule.

* Armor line of spells: concurrency not handled yet.

* Display strings: this has only be handled in a small number of spells.

* Cre scripts: set them in the patches instead of relying on name synchronicity.

* Cre scripts: some spells are cast in the script (example: leopard casts dvspratt). The resource names must be corrected in a patch to the script.

* Summon spell lists: summon spell lists also have to be combed over and eventually patched.

* Make use of states from splstate.ids.

* As per Cure Mortal Wounds description implement immunity for non-living and extra-planar for all cure spells.

* Elemental protection: deal more systematically with elemental protection: if elemental resist >= 100 then protection from resource to block spell.

* Anti-undead spells like hold undead should bypass magic resistance.

* Use `append_item_block` instead of hack with `patch_block`.

* Conjure Elemental: remove probability of not summoning. Air Elemental: mentioned movement rate +3 in fists. Earth Elemental: mentioned movement rate -2 in fists. Damage bonus 9 -> 4.

* Damage bonus on natural attacks: these are set seeming randomly; standardize them.

* Add snake race for snake summon (possibly other with no_race).
