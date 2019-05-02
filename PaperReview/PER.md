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
  - Figure 1을 보면, 파란선이 샘플수가 커질수록 필요로되는 학습량이 exponential하게 감소하는 것을 볼 수 있다.
  - 물론 이는 oracle이기에 현실적이지는 않지만, uniform하게 sampling했을때와의 큰차이가 연구동기가 되었다고 한다.
  
  ##### 3.2 Prioritizeing with TD-error
  - prioritized replay의 핵심은 transition의 중요도를 측정하는 기준이 될텐데, 그걸 무엇으로 삼을 것이냐?!
  - 이걸 TD-error로 놓겠다.(**TD-error는 해당 transition이 얼마나 예상치 못한 transition인가를 의미**)
  - reward가 noisy한 경우(reward의 분포가 넓게퍼진 경우), TD error는 제대로된 추정치로 작동하지 않을 수 있다.
  - 한번도 가보지 않아 TD error가 없는 것들은 최우선순위로 둔다.
  
  ##### 3.3 Stochastic Prioritization
  - TD error를 가지고 prioritization시 몇가지 문제가 있다.
  - 먼저, first visit에서 TD error가 작으면 오랫동안 replay되지 않을 것이다.
  - 또한, noisy spike에 민감하다. (noisy spike는 reward가 stochatic할때 나오는 일종의 uncertainty? error?)
  - 이 noisy spike가 bootstrapping으로 더 심해지게 된다.(bootstrapping도 approximation error를 가지고 있기 때문)
  - 간단히 말해, noisy spike는 error/uncertainty를 의미하는 것 같다.(학습의 불안정한 상태를 가중시킨가?)
  - 마지막으로, greedy prioritization으로 몇몇 experiences에만 업데이트가 집중되고, 결국 overfitting될 수 있다.
  - 즉, 다양성의 부족을 야기한다.
  - 이러한 3가지 문제를 극복하기위해 **stochastic sampling method**를 활용한다.
    - 낮은 priority를 가진 transition이라도 뽑힐 확률이 0보다 크게 만들어 준다.
  - stochastic prioritization은 alpha를 조절하여 uniform/greedy sampling을 조절한다.
  - prioritization의 measure방식엔 proportional과 rank-based 두가지 방식이 있다.(rank-based가 robust함)
  
  ##### 3.4 Annealing The Bias
  - 첫 문장의 의미가 직관적으로 이해가 되지 않는다.(same distribution의 의미가 iid조건을 말하는건지...뭔지...)
    - 현재 이해한걸 바탕으로 써보면, value의 분포가 있고 우리는 value 분포의 기댓값을 estimate하고 있다.
    - 업데이트를 하는 sample들의 value는 기댓값이 같은 분포에서 나왔다는 가정하에 value를 구한다.
    - 하지만, prioritized replay가 분포를 변화시키고 결국엔 estimation이 수렴점을 변화시킨다.
  - 무튼 prioritized replay가 bias를 만들어내는데, 이러한 bias를 잡기위해 weighted importance sampling을 사용하는데..
  - 여기서 사용한 weighted importance sampling은 non-uniform sampling에 대한 보상개념으로 사용된다.(+bias 잡고)
  - weighted importance sampling으로 구한 w에 max w로 나눠주어 안정성을 확보한다.
    - 스케일링은 자료 집합에 적용되는 전처리 과정으로 
    - 모든 자료에 선형 변환을 적용하여 전체 자료의 분포를 평균 0, 분산 1이 되도록 만드는 과정이다.
    - 스케일링은 자료의 오버플로우(overflow)나 언더플로우(underflow)를 방지하고 
    - 독립 변수의 공분산 행렬의 조건수(condition number)를 감소시켜 최적화 과정에서의 안정성 및 수렴 속도를 향상시킨다.
