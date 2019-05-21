# Twin Delayed Deep Deterministic policy gradient (TD3)
## Addressing Function Approximation Error in Actor-Critic Methods

| Keywords |
|:--------:|
| Overestimation problem in actor-critic |
| Double Q-learning |
| connection between target network and overestimation |

### Motivation
- value-based RL의 DQN에서 overestimation문제가 있었는데, actor-critic에서도 이러한 문제 발생.

### Methods
- 

##### Pseudo Code
![TD3 Pseudo code](http://spinningup.openai.com/en/latest/_images/math/52d3d2df4225f9fec06156d6e1d3da26c8b27bc5.svg)
