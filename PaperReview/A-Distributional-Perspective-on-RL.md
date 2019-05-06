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
  
### Setting
- 기존 방법론들과 같이 environment와 상호작용하는 것을 모델링한다.
- 다만 여기서 바뀐건 State를 의미하는게 S가 아닌 X라는 점.

  ##### 2.1 Bellman Equations
  - Z의 기댓값은 Q가 된다.
  - 조금 생소한(?) notation이 등장한다.
  - figure 1에서 (d) Projection step과 여기서 등장하는 대문자 Tau(타우)가 Bellman Operator로 등장한다.
  - 해당 내용과 관련하여 David Silver의 RL 3강 DP를 참고하자.
  - 정리하면, figure 1과 거기서 나온 Bellman operator T(tau)...이게 contraction/mapping개념과 맞물린다.
  
### The Distributional Bellman Operators
- 이 논문에서 우리가 기존에 알던 Bellman Expectation Equation에서 Expectation부분을 없앴다.
- 대신 full distribution을 고려하여, random variable Z를 다룬다.
- 이번 절에서는 distributional한 operator의 이론적인 내용과 control setting에 대한 이해를 다룬다.
- 알고리즘에 관심이 많은 독자에게 skip을 권유하는데...나는 도전!

  ##### 3.1 Distributional Equations
  - 확률공간(probability space)을 사용하는데 유용한 점이 있다고 한다.(뭐지?)
  - 뭐 cdf에 대한 내용과 norm에 대한 얘기가 나온다.(Random variable U를 가지고 이야기한다.)
  - U와 V는 서로 독립인 확률변수이지만 동일한 분포를 띈다는 것 같다.(i.i.d..?)
  
  ##### 3.2 The Wasserstein Metric
  - 이 논문의 가장 핵심이 Wasserstein Metric이다.(두 cdf사이에서의 Wasserstein Metric)
  - **두 cdf F,G의 Wasserstein Metric은 U-V의 norm이다?!**
  - 여기서 inverse cdf의 개념이 나오고 이것이 quantile function이라고 한다.
