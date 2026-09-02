# From Video Models to Robotics

[한국어](https://2seungeun.github.io/2seungeun/notes/01-video-to-robotics-transition/) | **English**

This note began with a simple impression: a surprising number of people who worked on video now seem to be moving into robotics. To see whether that impression holds, I looked beyond current affiliations and traced both the video problems these researchers originally worked on and where that experience later appeared in robotics.

I collected 57 researchers and 55 papers as two separate sets. The papers comprise **31 with a direct, paper-level connection to robotics**, **17 without robot experiments but useful for tracing the same technical lineage**, and **7 representative video- or robotics-side references retained as comparison points**. These groups are labeled `Yes`, `Adjacent`, and `No`, respectively, in the spreadsheet. Researchers and papers do not map one-to-one: a paper may have several relevant authors, and a researcher may appear across several papers. Only for the researcher ranking did I select one representative video paper and one representative robotics paper per person.

## The boundary was blurring more than people were switching fields

The 57 researchers fall into four groups.

| Type | Count | Meaning in this note |
|---|---:|---|
| Switcher | 2 | The main research topic or organization clearly shifted from video to robotics or world models |
| Bridger | 42 | Produced important work in both areas or directly connected the architectures |
| Native hybrid | 11 | Worked on video and robotics together from a relatively early stage |
| Robotics-first | 2 | A comparison group centered on robotics, with weaker evidence of a video starting point |

Only two fit a narrow definition of switching fields. Far more common were the 42 `Bridgers`, who continued to move between the two areas or carried structures developed for video into robotics. The remaining 13 are 11 `Native hybrids`, who worked across both areas from the outset, and two `Robotics-first` cases retained to avoid overstating the transition.

It therefore seems more accurate to describe this as a rapid blending of two research areas than as a large-scale migration of video researchers. I was probably drawn to the question because my own interests followed a similar path, from video through world models toward robotics.

![Researcher transition types](assets/researcher_transition_types.png)

## Similar video models took on different roles in robotics

At first, I thought a split between video generation and video understanding would be enough. Once the papers were laid out together, however, the paths within those categories turned out to be different.

Video models that generate or predict future scenes tended to lead toward world simulation and planning. Models such as V-JEPA predict the future without reconstructing pixels, so I separated them from conventional video generation as `latent prediction`. Models trained on motion or tracking often connected to robotic perception, affordance, and video-conditioned policies. I treated video-language as a separate path as well: it aligns video and language into representations used for reward or reasoning, rather than directly producing actions like a VLA model.

The codes used in the figures should be read as follows. For the generation and prediction families, I distinguished G1, G2, G3, and A by considering both **what the model is trained to produce** and **whether action appears as an input, an output, or both**.

| Code | Main output or learning target | Where action appears | Typical role in robotics |
|---|---|---|---|
| G1 | Video pixels or tokens | Absent or not a central condition | Synthetic data, visual subgoals, video plans |
| G2 | Future video or states | May be used as a condition, but is not produced | World simulation, planning |
| G3 | Video or future states together with actions | Both are produced | Direct policy |
| U1 | Action, event, or semantic representations | Not classified by output | Perception backbone |
| U2 | Motion, tracking, or interaction representations | Not classified by output | Perception, reward, policy conditioning |
| U3 | Future latent representations | May be conditioned on action | Latent planning |
| VL | Video-language alignment and reasoning representations | Not classified by output | Reward, reasoning, policy conditioning |
| A | Action trajectories or tokens | Only actions are produced | Direct policy |

<details>
<summary><strong>Why game-oriented G2 papers were included but not counted as robotics evidence</strong> <em>(expand for the rationale and lineage)</em></summary>

[GameNGen](https://arxiv.org/abs/2408.14837) and [Genie](https://arxiv.org/abs/2402.15391) clearly meet the architectural definition. Both are G2 models because they generate the next visual state conditioned on past frames and actions, or on latent actions learned from video. Neither paper, however, demonstrates a transfer to robots or physical systems. I therefore included them as **papers without robot experiments that still help trace the same technical lineage**, marked them as `Adjacent` in the spreadsheet, and excluded them from the statistics on the 31 directly connected papers. In other words, **whether a model is G2** and **whether it has actually led to robotics** were judged separately.

![Lineage of game and general interactive G2 models](assets/interactive_g2_lineage.png)

</details>

G3 and A both lead to a `direct policy`. The distinction is not a difference in their robotic role, but in output modality and training structure: G3 jointly generates future visual states and actions, whereas A generates actions only.

I first counted researchers by their starting point. Each person was assigned one representative video origin and one primary role in robotics. G3 and A were omitted from this figure because they tend to emerge at the robotics stage rather than describe a researcher's original video background.

![Researchers by video starting point](assets/architecture_to_robot_role.png)

The next figure counts the 31 directly connected bridge papers instead of people. Here, GR-2 and Cosmos Policy appear as G3 direct policies because they jointly generate `video + action`. G3 was absent from the previous figure not because there were no G3 papers, but because that figure counted researchers' original starting points.

![Final architectures of directly connected bridge papers](assets/bridge_paper_architecture_to_robot_role.png)

## Reference

The spreadsheet contains the full researcher and paper lists, along with the evidence and decisions that did not fit in this note.

- [Download the research data](video_to_robotics_architecture_pilot.xlsx)
- List last updated: September 2, 2026
- Citation snapshot: August 30, 2026 for the original 40 papers; September 2, 2026 for the 15 papers added later

### How the list was built

I started with researchers who produced representative work in video generation, prediction, or understanding and later wrote important papers in robot learning or embodied AI. I also included papers in which a video model was directly used for perception, reward, data generation, world simulation, planning, or policy.

Working in both computer vision and robotics was not enough on its own. Nor did I treat a move to a robotics organization as evidence of a research transition. A small number of robotics-centered researchers with weak video starting points were retained as a `Robotics-first` comparison group.

`Evidence_strength` is separate from transition type. I assigned `High` when direct authorship of papers on both the video and robotics sides, or an official project role, could be verified. I assigned `Medium` when one side of the connection relied on a team-level announcement, a recent project page, or an indirect architectural lineage, or when direct authorship could not be verified with enough confidence.

`Citation_coverage` is a separate field again. `Both selected papers covered` means that the selected video and robotics papers both have IDs in the paper table and citation counts are available for both. If an ID, the connection, or a citation count is missing, the row is marked `Partial / missing selected-paper coverage`. Ten of the 57 researchers currently fall into the partial category. This field measures **whether the inputs needed for the score are complete**, not how credible the research connection is. Bridge Impact is recorded as `N/A`, rather than zero, for partial cases, and they are excluded from the ranking.

### I looked at both cumulative and age-adjusted citations

The first version of the paper list used qualitative labels such as `Landmark` and `Major`. That approach made it too easy for familiar researchers or papers that came to mind first to appear near the top, so I reordered the papers using actual citation counts.

Cumulative citations alone, however, compare a 2016 paper with a 2025 paper as if they had the same amount of time to accumulate citations. As a secondary measure for recent work, I divided citations by the number of publication years elapsed:

$$
\text{Citations per year}
= \frac{\text{Observed citations}}
{\max(1,\ 2026-\text{publication year}+1)}
$$

Under this convention, a 2025 paper is in its second year and a 2023 paper in its fourth. This is not a month-level citation velocity or a field-normalized metric. It is simply a way to check how strongly the cumulative ranking favors older papers. In the spreadsheet, directly connected bridge papers come first and are sorted by cumulative citations, with `Citations_per_year` shown in the adjacent column.

The left side of the figure below shows cumulative citations, and the right side shows the age-adjusted value. Older foundational papers are stronger on the left, while recent papers such as Cosmos and V-JEPA 2 move up relatively on the right.

![Cumulative and age-adjusted citations](assets/top_bridge_papers_by_citations.png)

I did not rank researchers by total career citations either. The aim here was to measure impact visible on **both** the video and robotics sides. I first identified people with important work in both areas, then took the geometric mean of citations to one representative video paper and one representative robotics paper.

$$
\text{Bridge Impact}
= \sqrt{(C_{video}+1)(C_{robotics}+1)} \times w_{evidence}
$$

I used a weight of 1.0 for `High` evidence and 0.8 for `Medium`. The value 0.8 is not statistically estimated; it is a rule chosen to discount cases with less direct evidence. I used a geometric rather than arithmetic mean so that a very highly cited paper on only one side would not dominate the score. The score was calculated only when `Important_both=Yes` and citation coverage was complete for both selected papers. Under this definition, Chelsea Finn, Sergey Levine, Ming-Yu Liu, Oier Mees, and Thomas Brox appear near the top.

### These numbers should not be read as a general ranking

The ranking starts by selecting researchers with important work visible on both the video and robotics sides, then calculates scores within that intersection. Researchers already well known in both fields are therefore likely to rank highly partly because of the sampling rule itself, not only because of the resulting metric. This is neither a score for independently discovering new switchers nor a ranking of researchers' overall impact.

The list is a sample chosen to study a pattern, not an exhaustive survey. Selecting only one or two representative papers leaves some contributions out, and a single bridge paper may sometimes serve as evidence on both the video and robotics sides. Citation counts also cannot separate the contributions of individual coauthors.

Citation counts themselves continue to change. Services report different numbers when arXiv and conference or journal versions are indexed separately, and papers from 2025–2026 may move substantially within a few months. The age-adjusted value does not solve these problems; it is only a second view for comparing older and newer papers.

Separating generation, understanding, and video-language—and then tracing the roles they take in robotics—changed my initial impression. The larger pattern seems to be less about people moving fields and more about **representations and predictive structures learned from video being carried into robotic world models, planning, and policies**.
