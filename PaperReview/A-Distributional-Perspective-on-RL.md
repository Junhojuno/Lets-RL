# A Distributional Perspective on Reinforcement Learning

| Keywords |
|:-----------:|
| Value Distribution |
| Distributional Bellman Equation |
| Wasserstein Metric |
| Non-stationary |

### Abstract
- importance of the value distribution : the distribution of the random return received by RL agent
- **value 혹은 return의 분포를 다룬다.** (이는 기존의 expected return/value을 뽑아내던 것과 대조적이다.)
- 이 distributional perspective(관점)를 Bellman Equation에 접목시킬거라고 한다.


### Introduction
- 기존의 `Bellman (Expectation) Equation : Q(s,a) = E[R + gamma * Q(s',a') | s, a]`
- 여기서 더 나아가 **Q를 기댓값으로 갖는 random return Z**가 등장한다.
- Z도 Q와 똑같은 Bellman Equation형식을 띈다.(다만 E가 빠진다.)
  - `Z(s,a) = R(s,a) + gamma * Z(s',a')`
- Z는 **3개의 Random Variables**와 관계를 맺는데...R, (s',a'), Z(s',a')
- 다음은 value distribution의 역할을 나타낸다.
  ##### Contraction of the policy evaluation Bellman operator
  - Distributional Bellman Operator가 Wasserstein Metric에서 contraction이라는데...뭔말인지;;
  - KL Divergence를 쓰지 않고 Wasserstein Metric을 쓰는 이유를 말하는 내용인가??
  
  ##### Instability in the control setting
  - Bellman Optimality Equation의 distributional version의 불안정성을 증명한다고 한다.
  - Optimality operator가 expected value의 contraction이지만,
  - distribution관점의 metric에서는 contraction이 아니란다...느낌이 올듯말듯..
  - 이것이 **non-stationary policy를 모델링하는데 근거를 제공**한다고 한다.
  
  ##### Better Approximations
  - 알고리즘 관점에서 expectation하나를 근사하는것보다 distribution을 근사하는 것이 더 이롭다.
  - Distributional Bellman operator가 **multimodality를 보존하여 이것이 학습에 안정성을 준다.**
  - 분포를 근사시키는게 policy를 학습시키면서 오는 non-stationary한 효과를 감소시킨다.(안정성이 올라간다는 소리인듯)
  - 
