# 비디오 모델은 어떻게 로보틱스로 이어졌나

비디오를 하던 사람들이 요즘 로보틱스로 많이 넘어간 것 같다는 인상에서 시작했다. 실제로 그런 흐름이 있는지 보려면 사람의 현재 소속만 볼 게 아니라, 원래 어떤 비디오 문제를 풀었는지와 그 경험이 로봇에서 어디에 쓰였는지를 같이 봐야 했다.

그래서 연구자 57명과 논문 40편을 모아 출발 아키텍처, 로보틱스에서의 역할, 대표 논문의 영향력을 따로 기록했다. 

## 전환이라기보다는 경계가 섞이고 있었다

확인해 보니 비디오에서 로보틱스로 연구 주제나 조직을 뚜렷하게 옮긴 경우는 57명 중 2명이었다. 그보다는 두 분야를 계속 오가거나, 비디오에서 쓰던 구조를 로봇 문제에 옮긴 사람이 훨씬 많았다. 이들을 `Bridger`로 분류했는데 42명이었다.

그래서 ‘비디오 연구자들의 대규모 이동’보다는 ‘두 연구 영역의 경계가 빠르게 섞이고 있다’고 보는 편이 맞아 보였다. 나 역시 비디오에서 월드 모델을 거쳐 로보틱스로 관심이 옮겨진 경우라 이 흐름이 더 궁금했던 것 같다.

![연구자 전환 유형](assets/researcher_transition_types.png)

## 같은 비디오 모델이라도 로봇에서 맡는 역할은 달랐다

처음에는 비디오 생성과 이해 정도만 나누면 될 줄 알았다. 그런데 논문을 모아 놓고 보니 그 안에서도 경로가 달랐다.

모션이나 트래킹을 배우는 모델은 로봇의 perception, affordance, video-conditioned policy로 연결되는 경우가 많았다. 반면 미래 장면을 생성하거나 예측하는 모델은 world simulation과 planning 쪽으로 이어졌다. V-JEPA처럼 미래를 예측하더라도 픽셀을 복원하지 않는 모델은 일반적인 비디오 생성과 묶기 어려워 `latent prediction`으로 따로 뒀다. Video-language도 마찬가지다. 영상과 언어를 정렬해 얻은 표현이 reward나 reasoning에 쓰이는 흐름이라, 바로 action을 내는 VLA와는 구분했다.

![연구자의 비디오 출발점](assets/architecture_to_robot_role.png)

먼저 연구자의 출발점만 따로 셌다. 각 사람에게 대표 비디오 출발점 하나와 로보틱스에서의 주 역할 하나를 부여했다. G3와 A는 비디오 연구의 출발점이라기보다 로봇 단계에서 생기는 구조라 이 그림에서는 뺐다.

다음은 사람 대신 브리지 논문을 센 그림이다. 여기서는 GR-2와 Cosmos Policy가 `video + action`을 함께 생성하는 G3 direct policy로 나타난다. 앞 그림에서 G3가 0이었던 것은 G3 논문이 없어서가 아니라, 연구자의 원래 출발점을 세고 있었기 때문이다.

![브리지 논문의 최종 아키텍처](assets/bridge_paper_architecture_to_robot_role.png)


그림에 쓴 코드는 아래처럼 읽으면 된다. 자세한 정의보다, 모델이 주로 무엇을 만들거나 이해하는지를 기준으로 나눴다.

| 코드 | 출발점 | 로봇에서 주로 이어진 역할 |
|---|---|---|
| G1 | 비디오 픽셀·토큰 생성 | synthetic data, visual subgoal, video plan |
| G2 | 미래 비디오·상태 예측 | world simulation, planning |
| G3 | 비디오와 action 공동 생성 | direct policy |
| U1 | 행동·사건·의미 이해 | perception backbone |
| U2 | 모션·트래킹·상호작용 이해 | perception, reward, policy condition |
| U3 | latent representation 예측 | latent planning |
| VL | video-language 정렬·추론 | reward, reasoning, policy conditioning |
| A | action trajectory·token 생성 | direct policy |

게임형 interactive world model은 조금 다르다. [GameNGen](https://gamengen.github.io/)이나 [Genie](https://arxiv.org/abs/2402.15391)는 action을 조건으로 미래 프레임이나 환경을 생성한다. action까지 출력하는 정책은 아니므로 이 글의 기준에서는 G3가 아니라 G2다. 다만 두 논문은 현재 40편의 pilot 목록에는 들어 있지 않아 위 숫자에는 포함되지 않았다.

## 참고

아래 엑셀에는 이 글에 다 넣지 못한 연구자·논문 목록과 판단 근거 URL이 들어 있다.
- [조사 데이터 내려받기](video_to_robotics_architecture_pilot.xlsx)
- 조사 기준일: 2026-08-30

### 목록을 만든 기준

비디오 생성·예측·이해 분야에서 대표 작업을 한 뒤 로봇 학습이나 embodied AI에서 중요한 논문을 쓴 경우를 먼저 찾았다. 한 논문 안에서 비디오 모델이 perception, reward, data generation, world simulation, planning, policy에 직접 사용된 경우도 포함했다.

유럽 쪽 흐름도 놓치지 않으려고 Paris, London, Oxford, Freiburg 연구 클러스터를 별도로 확인했다. 여기서 지역은 국적이나 현재 거주지를 뜻하지 않고, 이 조사에서 확인한 연구 조직과 논문의 맥락에 가깝다.

반대로 컴퓨터 비전과 로보틱스를 모두 했다는 이유만으로 넣지는 않았다. 로봇 조직으로 소속이 바뀐 것만으로도 전환이라 부르지 않았다. 직접적인 논문이나 프로젝트 근거가 약한 사람은 `Medium` 또는 `Partial coverage`로 표시했고, 로보틱스에서는 중요하지만 비디오 출발점이 약한 연구자는 비교군으로 일부 남겼다.

### 인용수는 누적값과 연차 보정값을 같이 봤다

논문을 처음 정리했을 때는 `Landmark`, `Major`처럼 정성적인 등급만 붙였다. 그런데 이 방식은 내가 먼저 떠올린 사람이나 익숙한 논문을 앞에 놓기 쉬웠다. 그래서 논문 순서를 실제 인용수 기준으로 다시 잡았다.

다만 누적 인용수만 쓰면 2016년 논문과 2025년 논문을 같은 조건에서 비교하게 된다. 최신 논문을 보기 위한 보조값으로 다음과 같이 발표 후 연차를 나눈 값도 계산했다.

$$
\text{Citations per year}
= \frac{\text{Observed citations}}
{\max(1,\ 2026-\text{publication year}+1)}
$$

예를 들어 2025년 논문은 2년 차, 2023년 논문은 4년 차로 계산했다. 정확한 월 단위 citation velocity나 분야 보정값은 아니고, 오래된 논문이 무조건 유리해지는 것을 확인하기 위한 단순한 보정이다. 엑셀의 기본 순서는 브리지 논문을 먼저 둔 뒤 누적 인용수로 정렬했고, 바로 옆 열에 `Citations_per_year`를 넣었다.

아래 그림의 왼쪽은 누적 인용수, 오른쪽은 이 연차 보정값이다. 오래된 기반 논문은 왼쪽에서 강하고, Cosmos나 V-JEPA 2처럼 최근 논문은 오른쪽에서 상대적으로 올라온다.

![누적 인용수와 연차 보정 인용수](assets/top_bridge_papers_by_citations.png)

연구자도 전체 커리어 인용수로 줄 세우지는 않았다. 이 글에서 보고 싶은 것은 비디오와 로보틱스 **양쪽**에서 확인되는 영향력이었기 때문이다. 양쪽에서 중요한 작업이 확인된 사람을 먼저 두고, 대표 비디오 논문과 로보틱스 논문의 인용수를 기하평균했다.

$$
\text{Bridge Impact}
= \sqrt{(C_{video}+1)(C_{robotics}+1)} \times w_{evidence}
$$

근거가 `High`이면 1.0, `Medium`이면 0.8을 곱했다. 한쪽 논문만 인용수가 큰 사람이 지나치게 올라가지 않도록 산술평균 대신 기하평균을 썼다. 이 기준에서는 Chelsea Finn, Sergey Levine, Ming-Yu Liu, Oier Mees, Thomas Brox가 앞에 놓였고 Agrim Gupta는 17위였다. Agrim Gupta가 중요하지 않다는 뜻은 아니다. 처음 떠올린 사례라는 이유만으로 1번에 놓였던 순서를 걷어낸 것이다.

### 이 숫자를 그대로 순위표로 보기는 어렵다

이 목록은 전수조사가 아니라 흐름을 보기 위해 고른 표본이다. 대표 논문을 한두 편만 선택하면서 빠지는 기여가 있고, 하나의 bridge paper가 비디오와 로보틱스 양쪽 근거가 되기도 한다. 공동저자의 실제 기여도도 인용수로는 나눌 수 없다.

인용수 자체도 계속 변한다. arXiv와 학회·저널 버전이 따로 잡히면 검색 서비스마다 숫자가 다르고, 2025–2026년 논문은 몇 달 사이 순위가 크게 달라질 수 있다. 연차 보정값도 이런 문제를 해결하는 지표라기보다 오래된 논문과 최신 논문을 한 번 더 나눠 보는 참고값이다.

그래도 생성, 이해, video-language를 한 덩어리로 세지 않고 로봇에서 맡는 역할까지 연결해 보니 처음의 막연한 인상은 조금 달라졌다. 사람의 이동 자체보다, **비디오에서 배운 표현과 예측 구조가 로봇의 world model, planning, policy로 옮겨가는 과정**이 더 큰 흐름에 가까웠다.
