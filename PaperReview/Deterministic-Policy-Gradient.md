# Deterministic Policy Gradient

### 요약 정리
- 

### 0. Abstract
- **deterministic policy gradient는 the expected gradient of Q의 형태를 다룬다.**
- 이로써 deterministic policy gradient가 **stochastic policy gradient보다 훨씬 효율적이다!**
- exploration을 위해 off-policy actor critic algorithm을 소개하고
- 이것을 통해 deterministic policy gradient를 학습한다.

| keywords | 읽는 초점 |
|:--------:|:----:|
| deterministic policy | 기존 stochastic policy와 다른점과 의미하는게 뭐지? |
| expected gradient of Q | 기존 policy gradient와 차이가 뭐가 있는거지? |
| off-policy actor-critic algorithm | 이게 어떻게 알고리즘에 녹아 들어가 있지? |

### 1. Introduction
- stochastic policy gradient에서는 policy가 분포형태를 띄게된다.


### 2. Background
- silver 7강의 내용과 일치하는 부분이 대부분이라 넘어간다.
- 자세한 내용은 [여기](https://github.com/Junhojuno/Lets-RL/blob/master/silver%EA%B0%95%EC%9D%98/07_Policy_Gradient.md)

### 3. Gradients of Deterministic Policies
