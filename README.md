# A 93,904,752,506-letter superpermutation on 14 symbols

This repository presents an **upper-bound construction**, not a proof of optimal length. The [compressed witness](n14-93904752506.detour) is a complete word over the alphabet `0123456789ABCD`, containing all 14! = 87,178,291,200 permutations as contiguous substrings. It is one letter shorter than its source, Jay Pantone's independently checked [W-0117](https://superpermutations.com/w/W-0117) (93,904,752,507 letters).

[中文说明](README.zh.md) · [reproducibility bundle](reproduction.zip) · [machine-readable splice certificate](splice.json)

## Construction

Cut at the following three transitions between 14-letter permutation windows in W-0117. Positions are zero-based starts of the source windows; the destination window starts at position plus old cost.

| Cut | Position | Source | Destination | Old cost |
|---|---:|---|---|---:|
| i | 8,018,599,985 | DCB015342A9876 | 0173426985ABCD | 14 |
| j | 36,587,897,101 | D1C02B459A3768 | 768234519ABCD0 | 11 |
| k | 50,281,547,842 | 0DC1B896425A37 | A37689B5214CD0 | 11 |

At each cut the block to the left includes the full source window, and the block to the right starts at the destination window. This produces four blocks A, B, C, D; adjacent blocks can overlap. A permutation occurrence that is not wholly contained in one block must start strictly between the source and destination window starts at one of these cuts. Two implementations of the Detour parser locate the stated windows, and direct checks show that **none of the 33 intervening windows is a permutation**. Every original permutation occurrence is therefore wholly retained inside a block.

Assemble the four blocks in the order **A, C, B, D**, using maximum suffix–prefix overlap. The three replacement append costs in that physical order are 12, 14 and 9. They cost 35 letters rather than 36, and each retained block is an unchanged contiguous substring of the result. Thus all permutations covered by W-0117 are still covered.

## Verification

- Decoded ASCII word, with no newline: SHA-256 `8450c6d588f333768f8c182dbe6848d805e40105d780e8bd1042a1246d598de7`
- Compressed Detour file: SHA-256 `24f2ecb46b9d3bf79831aaf532971fb4c0bbaaed3ccb891847b2bb1146ebb9b1`
- The entire decoded word was hashed in a stream. The emitted token spans and new bridge tokens were independently verified against the splice. Coverage certification relies on the checked coverage of W-0117 and the preservation proof above; we did not rerun a full coverage sweep of the new word.

The [reproducibility bundle](reproduction.zip) contains the source and result Detour files, search code, independent parser, checker, proof notes, and transcripts. Extract the bundle and run `bash verify.sh` for the token-splice check; use `CHECK_FULL_HASH=1 bash verify.sh` to additionally stream and hash the decoded words. See the [Detour file format](https://superpermutations.com/format.txt). Do not expand the roughly 94 GB text onto disk unless necessary.

## Attribution

The source word is Jay Pantone's [W-0117](https://superpermutations.com/w/W-0117), distributed by the Superpermutation Almanac under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). The derivative witness retains four source blocks, interchanges the middle two and replaces their three joins. Attribution to the source does not imply endorsement.

The published [lower bound](https://github.com/jaypantone/2026-10-superpermutation-lower-palomar) is 93,891,141,150, leaving a gap of 13,611,356 to this construction.
