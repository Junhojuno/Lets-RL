# Prioritized Experience Replay

### 0. Abstract
- 이전 연구들이 experience transition을 uniform하게 sampling하였다.
- 하지만, 이러한 uniform sampling은 각 transition의 중요도를 반영하지 않았다.
- 이 논문에서는 **중요한 transition은 더 자주 sampling되도록(더 자주 replay) 만들었다.**
- 기존 DQN 알고리즘 + Prioritized Experience Replay를 사용한 새로운 알고리즘이다.
- 그냥 uniform하게 experience sampling한 DQN보다 41/49 게임에서 높은 점수를 기록하였다.
- 어떻게 Experience에 중요도를 부여하였는가?

### 1. Introduction
- Experience를 통해 parameter업데이트를 진행할 때, P(y|D)의 i.i.d조건이 파괴됨.
- 그래서 나온게 Experience Replay Memory
- Replay Memory에 experience를 저장하므로써, 일시적으로 correlation을 끊을 수 있다.\
(희귀한 experience 여러번 업데이트에 사용가능)
- Experience Replay는 일반적으로 학습에 필요한 Experience의 양을 줄일 수 있다.\
(계산량은 증가하지만, env와 상호작용하는 것보다 저비용)
<br><br>
- 학습을 효과적으로 하기위해 transition에 우선순위를 둔다.
- **TD Error의 크기를 가지고 중요도를 부여하자!** (error가 크면 중요도도 크다!)
- 이러한 우선순위부여가 다양성의 감소를 가져올 수 있지만, stochastic prioritization으로 이를 줄일 수 있다.
- 이러한 우선순위부여가 bias를 야기할수 있지만, 이건 importance sampling으로 개선하자.

### 2. Background
- 이 부분에서는 TD error가 Prioritization의 척도가 될 수 있음을 말하고 있다.
- 그리고 stochastic prioritization을 사용하는데, 이것이 sample로 근사하여 학습할때 robust하다고 한다.(왜...?)
- 이러한 prioritization을 Supervised Learning의 class imbalance문제에 적용할 수 있다.
- 자세한건 부속 논문 참고

### 3. Prioritized Replay
- replay memory는 보통 2 Levels로 진행 : 어떤 experience를 저장할거냐, 어떤 experience를 replay할거냐
- 여기선 어떤 experience를 replay할거냐를 다룬다.
  ##### 3.1 A Motivating Example
  - 여기선 uniform sampling한 agent와 그렇지 않은 agent 둘 사이의 학습속도를 비교한다.
