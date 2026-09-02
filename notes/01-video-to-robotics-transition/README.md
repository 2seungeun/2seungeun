# 비디오 모델은 어떻게 로보틱스로 이어졌나

**한국어** | [English](https://2seungeun.github.io/2seungeun/notes/01-video-to-robotics-transition/english.html)

<p align="center" class="article-byline">By <a class="article-author" href="https://www.linkedin.com/in/lee-seungeun" target="_blank" rel="author me noopener">이승은</a><span aria-hidden="true"> · </span><time datetime="2026-09-01">2026년 9월 1일</time></p>

비디오를 하던 사람들이 로보틱스로 많이 넘어간 것 같다는 인상에서 시작했다. 그런데 사람의 현재 소속만 따라가서는 이 흐름이 잘 보이지 않았다. 원래 어떤 비디오 문제를 풀었는지, 그 경험이 로봇에서 어디에 쓰였는지를 함께 봐야 했다.

이번에 다시 확인한 표본은 연구자 57명과 논문 66편이다. 둘은 1:1 목록이 아니다. 한 논문에 여러 연구자가 있고, 한 연구자도 여러 논문에 걸친다. 연구자 단위 비교를 할 때만 대표 비디오 논문과 대표 로보틱스 논문을 한 편씩 골랐다.

논문은 쓰임에 따라 세 묶음으로 나눴다.

| 논문 묶음 | 편수 | 뜻 | 엑셀 표기 |
|---|---:|---|---|
| 직접 연결 논문 | 31 | 논문 안에서 비디오의 표현·예측·생성 구조가 로봇 문제에 쓰인 것이 확인됨 | Yes |
| 흐름을 설명하는 주변 사례 | 22 | 로봇 실험은 없거나 직접 연결은 아니지만, 기술 계보와 비교에 필요함 | Adjacent |
| 한쪽 분야의 기준 논문 | 13 | 비디오 또는 로보틱스 한쪽의 대표 작업으로, 연구자의 출발점과 도착점을 확인하는 데 사용함 | No |

## 사람의 이동보다 연구 경계가 더 많이 섞였다

57명은 겹치지 않게 다섯 유형 중 하나에만 넣었다.

| 유형 | 인원 | 이 글에서의 의미 |
|---|---:|---|
| Switcher | 2 | 주 연구 주제나 조직이 비디오에서 로보틱스·월드 모델로 뚜렷하게 이동 |
| Bridger | 39 | 두 분야에서 중요한 작업을 했거나 기술을 직접 연결 |
| Native hybrid | 11 | 비교적 이른 시기부터 비디오와 로보틱스를 함께 연구 |
| Robotics-first | 4 | 로보틱스가 중심이며 확인 가능한 비디오 출발 논문이 없는 비교군 |
| Video-first | 1 | 비디오·가상 embodied agent 작업은 확인되지만 물리 로봇 논문은 확인하지 못한 비교군 |
| **합계** | **57** | 각 연구자는 한 번만 셈 |

좁은 뜻의 ‘전환’에 해당하는 사람은 2명이었다. 더 흔한 경우는 비디오와 로보틱스를 오가거나, 비디오에서 쓰던 구조를 로봇 문제로 가져온 Bridger였다. 그래서 대규모 인력 이동보다는 두 연구 영역의 경계가 빠르게 섞이고 있다고 보는 편이 맞다.

![연구자 전환 유형](assets/researcher_transition_types.png)

## 출발 구조, 모델 출력, 로봇 역할을 따로 셌다

기존 표에서 가장 큰 문제는 하나의 ‘아키텍처’ 열에 서로 다른 질문이 섞여 있던 점이었다. 이번에는 세 축을 분리했다.

1. **비디오에서 가져온 메커니즘**: 무엇을 보고 배우거나 예측했는가
2. **해당 논문의 최종 출력**: 실제로 무엇을 내보내는가
3. **로봇에서의 역할**: perception, reward, data generation, world simulation, planning, direct policy 중 어디에 쓰이는가

### 비디오에서 가져온 메커니즘

| 코드 | 짧은 뜻 | 구분 기준 | 로봇에서 자주 맡는 역할 |
|---|---|---|---|
| G1 | 영상 생성 | 이미지·비디오 픽셀이나 토큰을 생성하며, 로봇 action은 핵심 입력이 아님 | 합성 데이터, visual subgoal, video plan |
| G2 | action 조건 미래 예측 | action을 입력으로 받을 수 있지만 출력하지 않고, 미래 영상·상태를 예측 | world simulation, planning |
| G3 | 영상·action 공동 생성 | 미래 시각 상태와 action을 함께 출력 | direct policy |
| U1 | 의미·행동 이해 | 장면의 사건, 행동, 의미를 표현 | perception backbone |
| U2 | 모션·트래킹 이해 | 움직임, 포인트 트랙, 상호작용, affordance를 표현 | perception, reward, policy condition |
| U3 | latent 미래 예측 | 픽셀 대신 미래의 잠재 표현을 예측 | latent planning |
| VL | video-language | 영상의 시간 정보와 언어를 정렬하거나 함께 추론 | reward, reasoning, policy conditioning |
| None | 확인된 비디오 출발점 없음 | 로보틱스 비교군이거나 비디오 계보를 확인하지 못함 | 비교용 |

생성 계열에서는 action이 들어가는지 자체보다 **무엇을 출력하는지**를 기준으로 G1, G2, G3를 갈랐다. G1은 시각 결과만 만들고 action이 핵심 조건이 아니다. G2는 action을 조건으로 받을 수 있지만 미래 시각 상태를 출력한다. G3는 시각 상태와 action을 함께 출력한다.

### 해당 논문의 최종 출력

| 코드 | 논문이 내놓는 것 | 읽을 때 주의할 점 |
|---|---|---|
| G1 | 생성된 이미지·비디오 | visual plan이나 합성 데이터가 될 수 있음 |
| G2 | 예측된 미래 영상·상태 | action은 조건일 수 있으나 출력은 아님 |
| G3 | 미래 영상·상태와 action | 시각 상태와 action을 공동 생성 |
| A | action trajectory 또는 action token | action만 출력 |
| R | representation, reward, value, latent | 중간 표현이나 평가 신호 |
| D | dataset 또는 benchmark | 모델 출력으로 억지 분류하지 않음 |

G3와 A는 모두 direct policy로 이어질 수 있다. 로봇에서의 역할이 달라서 나눈 것이 아니라 **출력 모달리티와 학습 구조가 다르기 때문**이다. G3는 미래 시각 상태와 action을 함께 만들고, A는 action만 만든다.

<details>
<summary><strong>게임형 G2도 넣었다</strong> <em>(왜 직접 로보틱스 근거로 세지 않았는지 자세히 보기)</em></summary>

[GameNGen](https://arxiv.org/abs/2408.14837)과 [Genie](https://arxiv.org/abs/2402.15391)는 이 기준에 들어온다. 과거 화면과 action, 또는 영상에서 배운 latent action을 조건으로 다음 화면을 만들기 때문에 G2다. 다만 두 논문 자체에는 로봇이나 물리 시스템으로의 전이가 없다. 따라서 기술 흐름을 설명하는 Adjacent 사례에는 넣고, 직접 연결 논문 31편에서는 제외했다. **G2에 해당하는가**와 **로보틱스로 실제 이어졌는가**를 별도로 판단한 것이다.

![게임·일반 interactive G2 계보](assets/interactive_g2_lineage.png)

</details>

## 연구자와 논문을 같은 차트에 섞지 않았다

첫 그림은 연구자의 출발점이다. 각 사람에게 대표 비디오 메커니즘 하나와 로보틱스의 주 역할 하나를 부여했다. 물리 로봇 논문을 확인하지 못한 Tim Rocktäschel은 ‘확인된 로봇 역할 없음’으로 따로 표시했다. G3는 이 표본에서 대표 출발점으로 택한 연구자가 없어 0이다. G3 논문이 없다는 뜻은 아니다.

![연구자의 비디오 출발점](assets/architecture_to_robot_role.png)

재검산 결과 G1 → Planning은 6명이다. Yilun Du, Jiajun Wu, Karthik Dharmarajan, Ruohan Zhang, Sherry Yang, Wenlong Huang이 해당한다. 기존의 5명은 Yilun Du의 대표 출발 논문인 UniPi를 G1로 일관되게 반영하지 못해 생긴 집계 오류였다.

다음 두 그림은 사람 대신 직접 연결 논문 31편을 센다. 왼쪽 축을 두 번 나눠 본 이유는 ‘비디오에서 무엇을 가져왔는가’와 ‘그 논문이 최종적으로 무엇을 출력하는가’가 같지 않을 수 있기 때문이다.

![직접 연결 논문의 비디오 메커니즘과 로봇 역할](assets/bridge_paper_mechanism_to_robot_role.png)

![직접 연결 논문의 최종 출력과 로봇 역할](assets/bridge_paper_output_to_robot_role.png)

두 번째 그림에서 GR-2와 Cosmos Policy가 G3 → Direct policy로 잡힌다. action-only 정책은 A → Direct policy에 따로 놓였다. 이 분리 덕분에 G3가 사라지거나 A와 합쳐지는 문제가 없어졌다.

## 인용수와 연구자 점수도 다시 계산했다

인용수는 2026년 9월 2일의 [OpenAlex](https://openalex.org/) cited_by_count로 통일했다. 검색 서비스마다 합본 방식이 달라 숫자는 달라질 수 있으므로, 이 값은 절대값이라기보다 같은 출처 안에서 비교하기 위한 스냅샷이다.

누적 인용수만 보면 오래된 논문이 유리해진다. 최신 논문을 함께 보기 위해 다음 보조값을 계산했다.

$$
\text{Citations per year}
= \frac{\text{Observed citations}}
{\max(1,\ 2026-\text{publication year}+1)}
$$

2025년 논문은 2년 차, 2023년 논문은 4년 차로 친다. 월 단위 citation velocity나 분야 보정값은 아니고, 논문 나이에 따른 차이를 거칠게 확인하는 값이다.

![누적 인용수와 연차 보정 인용수](assets/top_bridge_papers_by_citations.png)

연구자 순서는 대표 비디오 논문과 대표 로보틱스 논문이 **서로 다른 두 편으로 확인된 경우에만** 계산했다.

$$
\text{Bridge Impact}
= \sqrt{(C_{video}+1)(C_{robotics}+1)} \times w_{evidence}
$$

Evidence_strength가 High이면 1.0, Medium이면 0.8을 곱했다. High는 양쪽 논문의 직접 저자이거나 공식 프로젝트 역할을 확인한 경우다. Medium은 한쪽 연결이 팀 발표, 최근 프로젝트 페이지, 간접적인 기술 계보에 기대거나 직접 저자 여부를 충분히 확인하지 못한 경우다. 0.8은 추정된 통계 계수가 아니라 불확실한 연결을 보수적으로 낮추기 위한 규칙이다.

한 논문이 비디오와 로보틱스 양쪽 근거를 모두 제공하는 경우는 연결 사례로는 남기되, 같은 인용수를 두 번 넣어 기하평균하지 않았다. 연구자 57명의 점수 자료 상태는 다음처럼 정확히 나뉜다.

| 점수 자료 상태 | 인원 | 순위 계산 |
|---|---:|---|
| 서로 다른 대표 논문 두 편이 모두 있음 | 24 | 이 중 Important_both=Yes인 20명만 계산 |
| 한 편의 브리지 논문을 양쪽 근거로 사용 | 22 | 제외 |
| 대표 논문 또는 인용 자료가 일부 빠짐 | 11 | 제외 |
| **합계** | **57** |  |

이 기준의 상위권은 Chelsea Finn·Sergey Levine 공동 1위, Thomas Brox 3위, Frederik Ebert·Sudeep Dasari 공동 4위다. Agrim Gupta는 공동 7위다. 처음 떠올린 이름을 앞에 두지 않고, 정해 둔 대표 논문과 같은 날짜의 인용수로 다시 계산한 결과다.

## 이 숫자를 일반 연구자 순위로 읽으면 안 된다

Bridge Impact는 비디오와 로보틱스 양쪽에서 중요한 작업이 확인된 사람을 먼저 고른 뒤 그 교집합 안에서 계산한다. 이미 두 분야에서 알려진 사람이 위로 오르기 쉬운 것은 지표의 결과이면서 표본 선택의 결과이기도 하다. 새로운 전환자를 독립적으로 찾아내는 점수도, 연구자의 전체 커리어 영향력 순위도 아니다.

대표 논문을 한두 편만 고르면서 빠지는 기여가 있고, 공동저자의 실제 기여도도 인용수로 나눌 수 없다. 2025–2026년 논문은 몇 달 사이 인용수가 크게 변할 수 있다. 그래서 누적 인용수, 연차 보정값, 정성적인 근거를 함께 보는 편이 낫다.

그래도 생성, 이해, video-language를 한 덩어리로 세지 않고 로봇에서 맡는 역할까지 연결해 보니 처음의 인상은 조금 달라졌다. 핵심은 사람의 이동 자체보다 **비디오에서 배운 표현과 예측 구조가 로봇의 world model, planning, policy로 옮겨가는 과정**에 가까웠다.

## 참고

엑셀에는 57명의 연구자 표, 66편의 논문 표, 두 종류의 아키텍처 행렬, 전환 유형 집계, 수정 내역과 출처가 들어 있다.

- [조사 데이터 내려받기](video_to_robotics_architecture_pilot.xlsx)
- 인용수 기준일: 2026-09-02

<p align="center" class="article-copyright">© 2026 이승은. All rights reserved.</p>
