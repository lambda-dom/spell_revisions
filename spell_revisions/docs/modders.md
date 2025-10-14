# A. Namespace management.

# B. Phases.

## B. 1. Spell symbols.

Because of data dependencies, there is a well defined ordering in which surgery of `spell.ids` proceeds.

1. Add new spell symbols.

2. Add new spell symbols that alias existing symbols.

3. Move spell symbols to a new slot in their level (e. g. aliased ones).

4. Replace old spell symbols with new ones. In particular, the old spell symbols become unavailable and any code relying on their existence will fail.

5. Add new symbols, assigning them to unused slots.

## B. 2. Sectypes.

## B. 3. VVCs.

Name the .vvc and required .bam animations identically with a fixed, statically defined name prefixed by the global prefix (for now settled on `dl`). The symbolic names are derived from the spells they are attached to.

## B. 4. Projectiles.

Same naming scheme as .vvc *but* this will probably change as now these are all *new* resources and we should rather, in some instances, override existing resources. This is particularly true for projectiles with a label suffixed sr.

## B. 5. Icons.

Since some spells will take up the slots of vaniolla spells and they have different bams, we name the corresponding bams using the affix trick.
