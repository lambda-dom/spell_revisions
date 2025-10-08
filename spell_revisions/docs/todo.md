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

* Physical Mirror: use PfM table to set up immunities to missiles. Shared mirror image effect with reflected image cannot be done because of different power levels.

* Banishment: second eff has wrong target; not clear what is the correct target, if any (summoned_demon?).

## A. 7. Level 7.

* Summon Shambling Mound: review the constrict spell: especially target vs. point casting and entangle implementation.

* Summon Death Knight: only description in. Implemented in the arcane level.

* Chaos: offload effects to subspells and fix off-by-one probability errors.

* Holy Word: offload effects to subspells.

* Regeneration: handle concurrent stacking.

* Resurrection: go over the list of spells to remove and find some way (a la PfM) to standardize it.

* Unholy Word: offload effects to subspells.

* Creeping Doom: only description in.

* Symbol of Stunning: offload effects to subspell.

* Earthquake: offload unconsciousness to a subspell. The implementation itself seems screwy because it relies on delayed cast spells targeting the targets (they should target the caster, but then the aoe would be caster centered). Maybe targeting via [148] succeeds? The IESDP seems to indicate that this will *not* work. Give projectiles to the subspells? Also, how is the last line of the description implemented?

# B. Arcane spells.

## B. 1. Level 1.

* Grease: follow implementation of Entangle? Use a sleep subspell? Also increase aoe of projectile.

* Sleep: display "ineffective spell" for creatures with dice > caster level.

* Spook: True Seeing makes one immune to Spook and this is handled in the True Seeing spell. Better to add a TRUE_SIGHT state to splstate.ids, set it via Set Spell State [328] in True Seeing and then use the usual shenanigan in Spook (e. g. 318) to make True Seeing nullify it. This spell state is apparently missing and is being set via proficiencies, but these are not detected via 318 and related opcodes (or at least I do not know how).

## B. 2. Level 2.

* Battering Ram: move unconsciousness from knockback to its own subspell? This would need weidu_library patching.

## B. 3. Level 3.

* Dispel Magic: only the description is in.

* Remove magic: reinstate, with old icon but targeting everyone (that is remove magic becomes old dispel magic).

* Protection from Missiles: Externalize the missiles table (e. g. copy it to weidu_external and offer functions as a modder resource to use it). Needs a pass over missing projectiles. Also used for physical mirror.

* Skull Trap: has an extra protection for swords. Undocumented so dropped for now, but to be revisited.

* Vampiric Touch: I am not sure the flags have been chosen correctly or even if they can be so chosen, and by this I mean: do damage per amount + dice, maybe capped by max hp of target. Absorb only up to maximum hp. Concurrency with other Vampiric Touches must also be addressed (e.g. spin106).

* Protection from Fire and Cold: not yet done as these are moved to level 4.

* Melf's meteors: description says evocation school, spell says conjuration. Going with description for now.

## B. 4. Level 4.

* Blue Shield: reinstate it.

* Mestil's Acid Shield: replaces cold shield but we are reinstating it. Spell itself is not in (and is in level 5).

* Minor Globe of Invulnerability: pass through area spells of level <= that must be protected against. Externalize like with PfM?

* Otiluke Resilient Sphere: only description is in.

* Spirit Armor: handle concurrency with other armor spells.

* Polymorph other: aux resources do not seem to be used anywhere.

* Enchant weapon: the basic spell is in but the items are missing proper descriptions and the spell, descriptions and ability icons.

* Monster Summoning IV: cre and script for phase spider unused.

* Wizard Eye: change from non-stacking to refreshing? Review creature.

## B. 5. Level 5.

* Monster Summon 5: Ogre Mage casts haste not slow which he does not have; does not use invis at will which is not memorized anyway.

* Shadow Door: add a True Seeing state so that we can put immunity to the spell in the spell itself (see Spook above).

* Waves of Fatigue: add immunity for "non-living" (undead, elementals, constructs, etc.).

* Dispelling Screen: the base spell makes no sense so have to implement the patching.

* Conjure (Lesser) Elemental: Add water elemental and consolidate all spells in one.

* Spell Deflection: add display string.

## B. 6. Level 6.

* Invisible Stalker: backstab x2 where exactly? *If* it can be added via class setting, class is already ranger so the kit field must be set to stalker. Only move silently is set to 120% as an invis effect is added through thje fists. What about hide in shadoes (set to 0 in the cre)?

* Globe of Invulnerability: see Minor Globe of Invulnerability.

* Flesh to Stone: why the remove combination spell type protections [221]?

* Banishment: see cleric's banishment.

* Improved Haste: missing remove spell resources to match protection from spell protections. Add like PfM? Check spell sectype should be none: should be in the code somewhere.

* Monster Summon 6: review damage bonuses, especially on the wyvern as they are too much?

* Stone to Flesh: not in yet.

## B. 7. Level 7.

* Protection from the Elements: review protections against specific spells. Add refreshing?

* Summon Death Knight: Add proficient with two-handed swords opcode. Systematize spell protections in the sword. Systematize fear aura. Missing resources (e. g. unholy fireball).

* Prismatic Mantle: move some of the effects to standardized subspells.

* Chaos: offload effects to subspells and fix off-by-one probability errors -- see cleric version.

* Prismatic Spray: move effects to subspells.

* Mordenkainen's Sword: mention vulnerability to dispel; review list of spell immunities in sword. Move immunity to psionics to immunities? The problem is that it *may* conflict with SCS.

* Summon Efreeti: Add proficient with scimitars opcode. Review spell protections to fire spells. Make duration constant and fixed.

* Summon Djinni: Add proficient with scimitars opcode. Make duration constant and fixed.

* Summon Hakeashar: Make duration constant and fixed.

## B. 8. Level 8.

* Ghostform: review implementation.

* Mind blank: review implementation.

* Protection from Energy: review implementation, especially the spell protections list.

* Summon Fiend: only description in.

* Incendiary Cloud: deleted protection against giant. Protections against "fire giants and salamanders" not implemented yet. Reduced viasual sight penalty should be hidden inside a spell to set up protections properly (e.g. bat).

* Power Word Blind: review spell protections; obscuring mist missing.

* Bigby's Icy Grasp: only description in.

* Summon Fiend: it is a fighter_mage_cleric so we need to set up third class in the cre tables. Immune to deafness but not mentioned in description. It's race is monster so animal summon buffs must exclude him explicitely. The detectable stuff in the immune to enchanted items +1 is most likely wrong so has tro be reviewed and changed.

* Monster Summoning VII: only description in.

# C. General.

* weidu_library stuff: (2) type the fields like those requiring tra refs by making the default -1 instead of *.

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

* Use `append_item_block` instead of hack with `patch_block`. This is already (partially?) done.

* Conjure Elemental: remove probability of not summoning in wizard version? But then: how to differentiate druid version. Air Elemental: mentioned movement rate +3 in fists. Earth Elemental: mentioned movement rate -2 in fists. Review damage bonuses.

* Damage bonus on natural attacks: these are set seeming randomly; standardize them. What *seems* to be happening is that the description is taking into account str bonuses.

* Add snake race for snake summon (possibly others with no_race).

* Incorporate spell flag setting in the spell tables.

* Revert names of sequencers to vanilla names? e. g. no "Simbul" and what not?

* Review ranges of natural weapons.
