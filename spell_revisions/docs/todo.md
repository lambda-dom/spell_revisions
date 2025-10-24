Not just things to (still) do but also proposed changes to spells.

# A. Divine spells.

## A. 1. Level 1.

* Armor of Faith: restore resistances of old spell.

* Detect Alignment: introduce alias CLERIC_DETECT_ALIGNMENT? Already have CLERIC_KNOW_ALIGNMENT.

* Goodberry: add scaling, non-concurrent, slow regenerating effect of 1 hp for round. Scale instant healing a little better. Only castable outdoors and ooc.

* Magical Stone: do the same dart treatment as fire seeds. Override original item.

* Resist Fear: use blocks library to implement immunity to fear, anchoring it to the Play Sound opcode in delayed mode (may need weidu_library support). The already existing block misses set spell state (RESIST_FEAR) opcode (needs weidu_library support to inline spell state values) and, optionally, a display portrait opcode.

* Strength of Stone: factor out immunity to knockback into a block of its own.

* Faerie Fire: what is the local variable stuff for?

* Obscuring mist: move blind-like part to a subspell.

* Animal Summoning I: Bat has no meaningful race and class.

* Sunscorch: nerf damage dice sides to d4.

## A. 2. Level 2.

* Aid: (technical) play visual opcode duration 6 -> 5 seconds to escape high duration patching side-effects. Make it fixed duration like other buffs?

* Chant: have good chant nullify bad chant and vice versa.

* Charm: fix: have to use a third subspell that is tasked with casting the two subspells.

* Find Traps: is subspells projectile correct?

## A. 3. Level 3.

* Animate Dead: gender "summoned" on skeletons may be incorrect. Double check.

* Dispel Magic: only the description is in.

* Invisibility Purge: review immunities on the subspell.

* Spike Growth: remove save from movement set for parity with entangle.

* Storm shield: standardize projectiles using a PfM scheme.

* Cause Serious Wounds: review the icons as they may be incorrect.

## A. 4. Level 4.

* Free Action: immunities are in but not curing them. Movement Rate 2 immunity dropped as it should as it is used as a penalty in Strength of Stone, for just one example.

* Death Ward: standardize immunities to instant death and disintegrate.

* Negative Plane Protection: No sectype; vanila is combination.

* Poison: move poison damage to subspells (at least the duration one).

## A. 5. Level 5.

* Cure Mortal Wounds: Implement immunity for non-living and extra-planar or delete from description?

* Flamestrike: has can target invis flag. Recheck when doing the flags patch.

* Raise Dead: removes shapechange spells; review for completeness and implement a PfM scheme to list them.

* True Seeing: there is a protection from the cloak of mirroring -- drop it if needed. Aux spell only removes illusion school spells up to level 2; remove illusionary protections of all levels? Missing protection against shadow door.

* Chaotic Commands: standardize immunities via blocks library.

* Cause and Cure Mortal Wounds: extend scaling to level 15?

* Greater Command: move sleep to subspell. Also, does not the recursive implementation imply that that it could go on for longer than 1 turn? Yes, so we have to unroll the recursion and put a bound to it.

* Protection from Acid: add protection to Vitriolic Sphere or not needed?

* Protection from Cold: only protectiom from wizard's cone of cold and icestrom. Add other.

* Protection from Fire: missing protections (e. g. aux flame arrow).

* Protection from Electricity: missing spell protections?

* Mass Regenerate: currently non-stacking. SR adds non-concurrent stacking, but is it needed?

* Harper's Call: to do. Drop the penalties and make it out of combat only.

## A. 6. Level 6.

* Physical Mirror: use PfM table to set up immunities to missiles. Shared mirror image effect with reflected image cannot be done because of different power levels.

* Banishment: second eff has wrong target; not clear what is the correct target, if any (summoned_demon?).

* Fire Seeds: mention in description that they are used as darts.

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

* Find Familiar: yet to implement.

* Grease: follow implementation of Entangle? Use a sleep subspell? Increase aoe of projectile -- see SRR.

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

* Enchant weapon: review exclusion flags on the items.

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

* Prismatic Mantle: move some of the effects to standardized subspells. The symbol is WIZARD_MANTLE but this is a case where introducing an alias is a good idea.

* Chaos: offload effects to subspells and fix off-by-one probability errors -- see cleric version. Why the rename? Keep the same symbol and rename it to vanilla Sphere of Chaos. Use the same name for the cleric version; this includes the symbol.

* Prismatic Spray: move effects to subspells.

* Mordenkainen's Sword: mention vulnerability to dispel; review list of spell immunities in sword. Move immunity to psionics to immunities? The problem is that it *may* conflict with SCS.

* Summon Efreeti: Add proficient with scimitars opcode. Review spell protections to fire spells. Make duration constant and fixed.

* Summon Djinni: Add proficient with scimitars opcode. Make duration constant and fixed.

* Summon Hakeashar: Make duration constant and fixed.

## B. 8. Level 8.

* Protection from Energy: review implementation, especially the spell protections list.

* Moment of Prescience: for now the symbol is added, as we do not want to override Improved Mantle.

* Incendiary Cloud: deleted protection against giant. Protections against "fire giants and salamanders" not implemented yet. Reduced viasual sight penalty should be hidden inside a spell to set up protections properly (e.g. bat).

* Power Word Blind: review spell protections; obscuring mist missing.

* Bigby's Icy Grasp: only description in.

* Summon Fiend: Immune to deafness but not mentioned in description. It's race is monster so animal summon buffs must exclude him explicitely. The detectable stuff in the immune to enchanted items +1 is most likely wrong so has to be reviewed and changed.

## B. 9. Level 9.

* Gate: Move effects of tail to subspells.

* Absolute Immunity: review spell protection list.

* Chain Contingency: probably discussed somewhere, but can we get rid of the seemingly useless cast spell opcode?

* Imprisonment: sectype patching not in yet.

* Meteor Swarm: what is the allow spotting (12) flag for? Should it be outdoors only?

* Energy Drain: protection from level drain does not block the bonuses to self; first move these bonuses to subspell then find a way to block them if *target* has level drain protection.

* Freedom: review spell removal and cures; sectype patching not in yet.

* Bigby's Crushing Hand: move stun to a subspell.

* Black Blade of Disaster: it has no strength bonuses but neither does it have the immaterial bonus of +4 thac0. Add it? The effect should also change? Check SRR.

# C. General.

* weidu_library stuff: (2) type the fields like those requiring tra refs by making the default -1 instead of *?

* weidu_library stuff: replacing spell symbols both in replaces and assigning to slot holes are slow operations.

* weidu_library stuff: damage types in damages.ids, item flags in cres in invitem.ids, item flags in itemflag.ids (the latter does not have the undispellable flag).

* Cure line of spells: mention in description that it also cures intoxication.

* Regenerate line of spells: handle inter-spell concurrency. The idea is that higher level remove and block lower level.

* Self-stacking debuffs: debuffs like Slow stack with themselves if not protected against -- this is achieved by a Protection from Spell [206] opcode and *not* by refreshing. The reason is that the debuffs apply on a failed save so it could happen that the refresh would clean the applied debuff and then fail to apply its effects due to a successful save. In the case of Slow, the problem is sharper because the debuff is applied via sectype, so while it does not stack with itself it will stack with other instances of the sectype. For now this is how it is done, but this ought to be revisited.

note(s):
* up to level 3 debuffs should also be revisited to see if they follow the rule.

* Armor line of spells: concurrency not handled yet.

* Display strings: this has only be handled in a small number of spells.

* Summon spell lists: summon spell lists also have to be combed over and eventually patched.

* Make use of states from splstate.ids.

* As per Cure Mortal Wounds description implement immunity for non-living and extra-planar for all cure spells.

* Elemental protection: deal more systematically with elemental protection: if elemental resist >= 100 then protection from resource to block spell. This also precludes the need to implement it in elemental damage spells.

* Anti-undead save-or-else spells like hold undead should bypass magic resistance.

* Use `append_item_block` instead of hack with `patch_block`. This is already (partially?) done.

* Conjure Elemental: remove probability of not summoning in wizard version? But then: how to differentiate druid version. Air Elemental: mentioned movement rate +3 in fists. Earth Elemental: mentioned movement rate -2 in fists. Review damage bonuses.

* Damage bonus on natural attacks: these are set seeming randomly; standardize them. What *seems* to be happening is that the description is taking into account str bonuses in damage *and* thac0. Check with SRR.

* Add snake race for snake summon (possibly others with no_race). See https://www.gibberlings3.net/forums/topic/40559-ee-race-updates for a Reptile suggestion.

* Incorporate spell flag setting in the spell tables.

* Revert names of sequencers to vanilla names? e. g. no "Simbul" and what not?

* Review ranges of natural weapons.

* Spell trap-like spells use a subspell to remove the resource when all the spell levels are removed -- resource mentioned in the spell deflection opcode. These should be overriden but this is the case only for spell trap.

* How to setup immunities to general effects like Entangle? The best way would be to use spell states, but we are lacking such as Entangle Immunity (but we do have Free Action, and that is already taken advantage of in standardized spell). Another option is to use sectypes, at least in the standardized effects; this is a little better now (but still not ideal), since we have decoupled subspells implementaion.

* [From the forums](https://www.gibberlings3.net/forums/topic/40132-royalprotectors-item-pack-zs_itempack/), a comment by jmerry: "Any sort of temporary proficiency bonus can be made permanent if you level up while it's active and take another proficiency in it. Even more spectacularly, I think a temporary proficiency bonus becomes permanent if you dual-class with it active; if you cast Black Blade of Disaster and then dual, that character gets grand master in long swords permanently.". Sigh.

# D. Projectiles.

* disintegrate: missing spgreorb aux resource.

# E. Icons.

* symbol of death, cleric: we override the c icon to fix a miscolor, but this *may* have been fixed in more recent EE versions (or maybe even the fixpack?).

* some bams are overriden by SR, but not all cases have been reviewed for graphical fidelity (that is, they are an actual improvement).

# F. Spell tables.

* We cannot existence check the spell resources in the spell tables because they are made available only later in the install order.

# G. Spell items.

* Item descriptions will probably have to wait IR to set up completely.

note(s):
* Even weapons on humanoids can be seen, so full descriptins are good for those as well as weapons conjured by spells, but natural weapons on monsters cannot, so in those cases descriptions can be left out.

* Clubs have Maces category instead of Clubs, why? Does it make a difference? This is probably a question for IR to deal with however.

* Magical Stone, Fire Seeds and Searing Orb are marked undispellable, contrary to most magical weapons. Is this justified? Searing Orb explicily says the spell is not affected by magic resistance so there is at least justification. Shillelagh explicitly mentions dispellability. Note that this can be controlled from the 2da table.

* Enchanted weapons need a second pass over the weapon speeds.

# H. Summons.

Naming of aux resources used literal, statically defined name with no override. The implication is that only "top level" resources used by spells use spell.ids name anchoring.

* Summons: missing dire wolf cre in summons table (dlmelee script). The table row is found somewhere in the backups.

* Should elementals be General monsters? The greater version (at least) have General as gianthumanoid, which is important for some spells like knockback, the animal buffs that have been extended to monsters, etc. The same for shambling mounds. More generally, we need a pass over the General categorization.

## H. 1. Scripts.

* weidu_library support: needs ways to systematize resource consumption; this involves (1) casting spells not in spell.ids (2) tlk references. The best way may be to use some form of variable expansion to be done at compile time using a table as the environment.

* Death Knight: checks for dw#sumfi item.

* Glabrezu: checks for dw#sumfi item.

* Pit Fiend: checks for dw#sumfi item.

* Shambling Mound: checks for dvinvis. This is a resource in SR, but we still have not discovered its use.

* Ogre Mage: uses blindness, supposed to be deprecated.

## H. 2. Spells.

* Bat swarm: must be targeted better, as currently it only filters for animals. Bats' race is no_race.

# I. Subspells.

* Is IMP correct for entangle immunity? Do not think it is...

* Divide charm in two subtypes: humanoid with elf and half-elf resistances and no creture type and generic, non-humanoid with no elf resistances but with given creature type.

* hold creature: remove uses of Use Eff [177] by filtering for (not ids = specified). This requires weidu_library support to retrieve the correct splprot entry.

* slow: review concurrency; review interaction with sectypes.

* slow movement rate ground: harmonize immunities with entangle.

* vampiric damage: patch damage description.
