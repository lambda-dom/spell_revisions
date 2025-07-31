Not just things to (still) do but also proposed changes to spells.

# A. Divine spells.

## A. 1. Level 1.

* Armor of Faith: restore resistances of old spell.

* Entangle: current implementation is incorrect as the decrease movement applies to all creatures, including those that should be immune. Solution: if we want to use the subspell (and we should), we may need another spell to decrease speed and then call the subspell.

* Goodberry: scaling, slow regenerating effect of 1 hp for round. Only castable outdoors and ooc.

* Find Familiar: yet to implement.

## A. 2. Level 2.

* Chant: have good chant nullify bad chant and vice versa.

* Cure Moderate Wounds: move Cleric_Cure_Medium_Wounds to level 2.

* Regenerate Moderate Wounds: handle stacking of regen spells. The idea is that higher level remove and block lower level.

## A. 3. Level 3.

* Dispel Magic: only the description is in.

* Insects: only the description is in. It needs sectype adding, which requires weidu_library support not existing yet.

# B. Arcane spells.

## B. 1. Level 1.

* Grease: follow implementation of Entangle? Use a sleep subspell? Also increase aoe.

* Sleep: display ineffective spell for creatures with dice > caster level.

* Spook: True Seeing makes one immune to Spook and this is handled in the True Seeing spell. Better to add a TRUE_SIGHT state to splstate.ids, set it via Set Spell State [328] in True Seeing and then use the usual shenanigan in Spook (e. g. 318) to make True Seeing nullify it. This spell state is apparently missing and is being set via proficiencies, but these are not detected via 318 and related opcodes (or at least I do not know how).

## B. 2. Level 2.

* Battering Ram: move unconsciousness from knockback to its own subspell? This would need weidu_library patching.

# C. General.

* Handle replacements: for now, they are just new spells, but they should replace old which implies doing surgery on `spell.ids`.
