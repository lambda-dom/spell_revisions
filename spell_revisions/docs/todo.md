# A. Divine spells.

## A. 1. Level 1.

* Entangle: current implementation is incorrect as the decrease movement applies to all creatures, including those that should be immune. Solution: if we want to use the subspell (and we should), we may need another spell to decrease speed and then call the subspell.

* Find Familiar: implement.

## A. 2. Level 2.

# B. Arcane spells.

## B. 1. Level 1.

* Grease: follow above implementation? Use a sleep subspell?

* Sleep: display ineffective spell for creatures with dice > caster level.

* Spook: True Seeing makes one immune to Spook and this is handled in the True Seeing spell. Better to add a TRUE_SIGHT state to splstate.ids, set it via Set Spell State [328] in True Seeing and then use the usual shenanigan in Spook (e. g. 318) to make True Seeing nullify it. This spell state is apparently missing and is being set via proficiencies, but these are not detected via 318 and related opcodes (or at least I do not know how).
