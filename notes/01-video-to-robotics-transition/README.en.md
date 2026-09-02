# From Video Models to Robotics

[한국어](https://2seungeun.github.io/2seungeun/notes/01-video-to-robotics-transition/) | **English**

<p align="center" class="article-byline">By <a class="article-author" href="https://www.linkedin.com/in/lee-seungeun" target="_blank" rel="author me noopener">Seungeun Lee</a><span aria-hidden="true"> · </span><time datetime="2026-09-01">September 1, 2026</time></p>

This note began with the impression that many people who worked on video were moving into robotics. Current affiliations alone did not tell that story very well. I needed to look at the video problems each researcher had worked on and where that experience later appeared in robotics.

The audited sample now contains 57 researchers and 66 papers. These are not one-to-one lists: a paper can have several relevant authors, and a researcher can appear on several papers. I selected one representative video paper and one representative robotics paper only when making researcher-level comparisons.

The papers are grouped by how they are used in the analysis.

| Paper group | Count | Meaning | Spreadsheet label |
|---|---:|---|---|
| Direct bridge papers | 31 | The paper itself shows a video representation, prediction, or generation mechanism being used for a robotics problem | Yes |
| Context and lineage papers | 22 | No direct robotics transfer is demonstrated, but the paper is needed to trace or compare the technical lineage | Adjacent |
| One-side reference papers | 13 | A representative video-side or robotics-side paper used to establish a researcher's starting point or destination | No |

## The research boundary blurred more than people switched fields

Each of the 57 researchers is assigned to exactly one of five transition types.

| Type | Count | Meaning in this note |
|---|---:|---|
| Switcher | 2 | The primary topic or organization clearly moved from video toward robotics or world models |
| Bridger | 39 | Produced important work on both sides or directly connected the technologies |
| Native hybrid | 11 | Worked on video and robotics together from a relatively early stage |
| Robotics-first | 4 | Robotics-centered comparison cases with no verified video-origin paper |
| Video-first | 1 | A comparison case with verified video and virtual embodied-agent work but no selected physical-robot paper |
| **Total** | **57** | Each researcher is counted once |

Only two people fit a narrow definition of switching fields. The more common pattern was a Bridger moving between both areas or carrying a structure developed for video into a robotics problem. This looks less like a mass migration and more like two research areas becoming tightly entangled.

![Researcher transition types](assets/researcher_transition_types.png)

## I separated the video mechanism, model output, and robot role

The main problem with the previous table was that a single architecture column mixed three different questions. The revised version keeps them separate:

1. **Video mechanism**: what is learned or predicted from video
2. **Focal output**: what the paper's model actually emits
3. **Robot role**: perception, reward, data generation, world simulation, planning, or direct policy

### Video mechanism

| Code | Short meaning | Boundary | Common robotics role |
|---|---|---|---|
| G1 | Visual generation | Generates image or video pixels or tokens; robot action is not a central input | Synthetic data, visual subgoals, video plans |
| G2 | Action-conditioned future prediction | Action may be an input, but the output is future video or state rather than action | World simulation, planning |
| G3 | Joint visual-action generation | Future visual states and actions are emitted together | Direct policy |
| U1 | Semantic and action understanding | Represents events, actions, or scene meaning | Perception backbone |
| U2 | Motion and tracking understanding | Represents motion, point tracks, interactions, or affordance | Perception, reward, policy conditioning |
| U3 | Latent future prediction | Predicts future representations rather than reconstructing pixels | Latent planning |
| VL | Video-language | Aligns temporal video information with language or reasons over both | Reward, reasoning, policy conditioning |
| None | No verified video origin | Robotics comparison case or no video lineage could be verified | Comparison only |

Within the generative family, G1, G2, and G3 are separated mainly by **what the model outputs**, not merely by whether action appears somewhere in the system. G1 emits visual content without action as a central condition. G2 may take action as a condition but emits future visual states. G3 emits visual states and actions jointly.

### Focal output

| Code | What the paper emits | How to read it |
|---|---|---|
| G1 | Generated images or video | Can serve as a visual plan or synthetic data |
| G2 | Predicted future video or state | Action may condition the prediction but is not the output |
| G3 | Future visual state and action | Visual state and action are jointly generated |
| A | Action trajectory or action token | Action only |
| R | Representation, reward, value, or latent | An intermediate representation or evaluation signal |
| D | Dataset or benchmark | Not forced into a model-output category |

G3 and A can both end in a direct policy. They are separated not because their robot roles differ, but because their output modalities and training structures do: G3 generates future visual states and actions together, while A generates actions only.

<details>
<summary><strong>Game-oriented G2 papers are included</strong> <em>(expand for why they are not counted as direct robotics evidence)</em></summary>

[GameNGen](https://arxiv.org/abs/2408.14837) and [Genie](https://arxiv.org/abs/2402.15391) meet the architectural definition. They generate the next visual state from past frames and actions, or from latent actions learned from video, so both are G2. Neither paper demonstrates transfer to a robot or physical system. I therefore retain them as Adjacent context but exclude them from the 31 direct bridge papers. **Being G2** and **showing a robotics transfer** are separate judgments.

![Lineage of game and general interactive G2 models](assets/interactive_g2_lineage.png)

</details>

## Researchers and papers are shown in separate charts

The first chart counts researcher starting points. Each person receives one representative video mechanism and one primary robotics role. Tim Rocktäschel is shown under “no verified robot role” because I could not verify a physical-robot paper for him. G3 is zero because no researcher in this sample was assigned G3 as the representative starting point. It does not mean that the paper set contains no G3 models.

![Researchers by video starting point](assets/architecture_to_robot_role.png)

After rechecking the underlying rows, G1 → Planning contains six researchers: Yilun Du, Jiajun Wu, Karthik Dharmarajan, Ruohan Zhang, Sherry Yang, and Wenlong Huang. The earlier count of five came from not applying G1 consistently to Yilun Du's representative starting paper, UniPi.

The next two charts count the 31 direct bridge papers rather than people. They use separate vertical axes because what a paper carries over from video can differ from what its final model emits.

![Direct bridge papers by video mechanism and robot role](assets/bridge_paper_mechanism_to_robot_role.png)

![Direct bridge papers by focal output and robot role](assets/bridge_paper_output_to_robot_role.png)

In the second chart, GR-2 and Cosmos Policy appear under G3 → Direct policy. Action-only policies remain under A → Direct policy. This keeps G3 visible without folding it into A.

## Citations and researcher scores were recalculated

All citation counts use the [OpenAlex](https://openalex.org/) cited_by_count snapshot from September 2, 2026. Different scholarly search services merge paper versions differently, so these are source-specific values intended for comparison within one snapshot.

Cumulative citations favor older papers. I therefore added a simple age-adjusted view:

$$
\text{Citations per year}
= \frac{\text{Observed citations}}
{\max(1,\ 2026-\text{publication year}+1)}
$$

Under this convention, a 2025 paper is in its second publication year and a 2023 paper in its fourth. This is not a month-level citation velocity or a field-normalized metric; it is only a rough check on paper age.

![Cumulative and age-adjusted citations](assets/top_bridge_papers_by_citations.png)

The researcher score is calculated only when the representative video and robotics papers are **two distinct papers**:

$$
\text{Bridge Impact}
= \sqrt{(C_{video}+1)(C_{robotics}+1)} \times w_{evidence}
$$

Evidence_strength receives a weight of 1.0 for High and 0.8 for Medium. High means direct authorship on both sides or a verified official project role. Medium means one side relies on a team announcement, a recent project page, an indirect technical lineage, or authorship that could not be verified with enough confidence. The 0.8 weight is a conservative rule, not a statistically estimated coefficient.

When one bridge paper supplies both the video and robotics evidence, it remains useful evidence but its citation count is not entered twice into the geometric mean. The 57 researchers divide exactly as follows:

| Score-data status | Count | Ranking treatment |
|---|---:|---|
| Two distinct representative papers covered | 24 | Ranked only when Important_both=Yes; 20 people qualify |
| One bridge paper used on both sides | 22 | Excluded |
| Representative paper or citation input partially missing | 11 | Excluded |
| **Total** | **57** |  |

Under this rule, Chelsea Finn and Sergey Levine are tied for first, Thomas Brox is third, and Frederik Ebert and Sudeep Dasari are tied for fourth. Agrim Gupta is tied for seventh. The ordering now follows the selected papers and one citation snapshot rather than the order in which names first came to mind.

## This is not a general ranking of researchers

Bridge Impact first selects people with important work visible on both the video and robotics sides, then scores that intersection. Researchers already known in both areas are likely to rank highly partly because of that sampling rule. The metric is not designed to discover new switchers independently or to measure overall career impact.

Selecting one or two representative papers also leaves out contributions, and citation counts cannot separate the roles of individual coauthors. Papers from 2025–2026 can change position quickly. Cumulative citations, the age-adjusted view, and the qualitative evidence should therefore be read together.

Separating generation, understanding, and video-language—and then tracing their roles in robotics—changed my initial impression. The larger pattern seems to be less about people moving fields and more about **representations and predictive structures learned from video moving into robotic world models, planning, and policies**.

## Reference

The spreadsheet contains the 57-researcher table, the 66-paper table, both architecture matrices, transition counts, correction log, and source links.

- [Download the research data](video_to_robotics_architecture_pilot.xlsx)
- Citation snapshot: September 2, 2026

<p align="center" class="article-copyright">© 2026 Seungeun Lee. All rights reserved.</p>
