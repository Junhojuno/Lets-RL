# Deterministic Policy Gradient

| keywords |
|:--------:|
| expected gradient of Q |
| off-policy actor-critic algorithm |

### 요약 정리
- 

### 0. Abstract
- **deterministic policy gradient는 the expected gradient of Q의 형태를 다룬다.**
- 이로써 deterministic policy gradient가 **stochastic policy gradient보다 훨씬 효율적이다!**
- exploration을 위해 off-policy actor critic algorithm을 소개하고
- 이것을 통해 deterministic policy gradient를 학습한다.

### 1. Introduction
- stochastic policy gradient에서는 policy가 분포형태를 띄게된다.
