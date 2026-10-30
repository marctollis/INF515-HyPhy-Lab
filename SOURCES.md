# Sources and provenance

## Teaching source and data

This lab adapts the question sequence and source–recipient framing of the [HyPhy selection teaching tutorial](https://github.com/veg/hyphy-tutorials/blob/master/docs/selection/README.md).

- Upstream dataset: [HIV.nex](https://github.com/veg/hyphy-tutorials/blob/master/docs/selection/data/HIV.nex).
- Local source: user-supplied HIV.nex from the course dnds_lab_NEW folder, copied without changes.
- Source NEXUS: 16 entries, 864 nucleotide columns (288 codons), 13 distinct aligned sequences. Datamonkey pilot outputs retain 13 entries, with identical input trees across the three outputs and all 21 branches designated test.
- Duplicate groups: D20_235/D20_236/D20_232; D20_234/D20_237. The retained names in the pilot are D20_235 and D20_234.
- Original sampling publication, exact genomic coordinates, collection dates, and detailed clinical metadata are not established here. Tutorial attribution is not a substitute for a verified original-study citation.
- No new license is asserted over upstream data or teaching materials. Confirm applicable upstream redistribution terms before public release. This package has not been published.

## Methods

- [BUSTED documentation](https://hyphy.org/methods/busted/). Murrell et al. (2015), Gene-wide identification of episodic selection, Molecular Biology and Evolution 32:1365–1371.
- [aBSREL documentation](https://hyphy.org/methods/absrel/). Smith et al. (2015), Less is more: an adaptive branch-site random effects model for efficient detection of episodic diversifying selection, Molecular Biology and Evolution 32:1342–1353.
- [MEME documentation](https://hyphy.org/methods/meme/). Murrell et al. (2012), Detecting individual sites subject to episodic diversifying selection, PLoS Genetics 8:e1002764.
- [HyPhy JSON field documentation](https://hyphy.org/resources/json-fields/).

## Pilot results supplied by the instructor

Verified on October 30, 2026. HyPhy runtime version 2.5.101; BUSTED method 4.7; aBSREL 2.6; MEME 4.1. See reference_results for original JSON outputs and checksums.sha256 for file identities. BUSTED settings report SRV Yes, multiple-hit None, error-sink 0, MSS No. MEME reports two rate classes and multihit None.

The JSON overall timers report 42 seconds (BUSTED), 22 seconds (aBSREL), and 21 seconds (MEME). These do not include upload/queue delays. Reference p-values may differ from older tutorial outputs and later software runs.
