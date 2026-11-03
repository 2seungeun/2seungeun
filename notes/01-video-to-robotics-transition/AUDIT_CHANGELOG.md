---
layout: default
title: "Video to Robotics: revision history"
lang: en
permalink: /notes/01-video-to-robotics-transition/revision-history.html
---

# Video→Robotics 수정 이력 / Revision history

[한국어](./) · [English](english.html)

## 2026-09-05 — 표본 재검토 / Sample re-audit

Researcher sample: **52 → 46**. Excluded because an individual physical-robotics connection was not verified under the stated rule: Andrea Vedaldi, João Carreira, José Lezama, Lijun Yu, Tim Brooks, Xun Huang.

Reference entries: **66 → 74**. All 66 previous Paper_ID entries were retained. Eight entries were added in commit `43eb3c4`, compared with `493faf9`.

| Paper ID | Added entry | Role in the sample |
|---|---|---|
| P067 | [Video-to-Video Synthesis](https://arxiv.org/abs/1808.06601) | No / G1 |
| P068 | [Learning to Imagine Manipulation Goals for Robot Task Planning](https://arxiv.org/abs/1711.02783) | Yes / G2 |
| P069 | [Learning Features by Watching Objects Move](https://arxiv.org/abs/1612.06370) | No / U2 |
| P070 | [Structured World Models from Human Videos](https://arxiv.org/abs/2308.10901) | Yes / G2 |
| P071 | [Time Reversal as Self-Supervision](https://arxiv.org/abs/1810.01128) | No / None |
| P072 | [Learning Correspondence from the Cycle-Consistency of Time](https://arxiv.org/abs/1903.07593) | No / U2 |
| P073 | [Learning Generalizable Dexterous Manipulation from Human Grasp Affordance](https://arxiv.org/abs/2204.02320) | No / None |
| P074 | [Affordances from Human Videos as a Versatile Representation for Robotics](https://arxiv.org/abs/2304.08488) | Yes / U2 |

## 2026-09-30 — 일관성 수정 / Consistency corrections

- Linked researcher representative metadata by Paper_ID: 35 mechanism mismatches and 35 output-description mismatches corrected. The researcher origin codes and role counts did not change.
- Restored 61 citation-source URLs from commit `493faf9` by Paper_ID. Existing historical citation counts were retained.
- Rewrote eight classification notes that referred to other papers and clarified Pandora's language-action boundary.
- Separated Samarth Sinha's official project/role evidence from authored single-paper bridges: 27 distinct paper pairs, 18 single-paper bridges, and 1 project/role case total 46 researchers. The ranked subset remains 23.
- Updated native table/filter extents to 74 paper entries and 46 researcher entries.
- Regenerated the interactive lineage figure from the workbook's September 2, 2026 OpenAlex snapshot. Renamed the citation-chart title to describe age-adjusted citations.
- Clarified G2 control actions, the absence of a separate A origin code, and the meaning of VL. Added visible modification dates and article dateModified metadata.

The current sample is **46 researchers / 74 reference entries / 34 direct bridge references**. Citation counts are historical snapshots, not current counts. The project article P032 remains one entry in the paper catalogue and is explicitly identified as a project article.

## 2026-11-03 — 문헌 현행화 / Evidence refresh

- Published the previously pending September consistency corrections first, in commit `d4c4580`.
- Added 10 individually sourced entries: nine research papers and one official announcement. Includes May–July backfills and September–November releases/revisions; sources checked November 3, 2026.
- Added a bilingual current-research section, a machine-readable JSON record, and the `Update_2026_11_03` workbook sheet.
- Preserved the original 46-person / 74-reference statistical sample and the September 2 citation snapshot. Combined archive: 84 references. New mechanism mappings are provisional; no new researcher assignments or current citation rankings are claimed.
- Disambiguated three unrelated R²-WAM papers by title and arXiv ID. Treated Genie 4 as an official simulation announcement, not evidence of physical policy transfer.

## 2026-11-03 — 인용수·순위 갱신 / Citation refresh

- Retrieved 82 research-paper records from OpenAlex; two official articles/announcements are not applicable. Counts of zero are observed record values, not missing lookups.
- Corrected mismatched work IDs for P067, P068, P069, P070, P072 and P074 using title, authors and DOI. Retained other matched records, without summing preprint/conference versions.
- Recomputed combined paper citation ranks, original direct-bridge ranks, 23 eligible researcher scores/ranks, and age-adjusted counts using unchanged first-publication years. Updated both citation-bearing figures.
- Added current retrieval/matching JSON, researcher ranking JSON and a clearly marked legacy snapshot. The old values are not a validated citation-growth baseline.
- Updated Korean/English text and workbook inputs, formulas, citation dates and snapshot sheet.
