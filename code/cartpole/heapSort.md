# What is Heap Sort?

| Keywords |
|:--------:|
| tree / binary tree |
| complete binary tree |
| partial order |

### Binary tree (이진 트리)
<p align="center"><img src="http://ehpub.co.kr/wp-content/uploads/2016/06/2-110.png"></p>

- node(동그라미 한개를 의미), level(동그라미가 쌓인 층을 의미), degree(서브트리의 갯수)
- 위에서 아래로 가지를 뻗어나가는 그림인데, 아래노드를 child node, 윗노드를 parent node라고 한다.
- 이진트리의 레벨 i에서의 최대 노드의 수는 2^(i-1)  (i>=1)이다.
  - 예를 들어, level 1에서 가질수 있는 **최대** 노드의 갯수는 1개(root node)
  - level 2라면, root node로부터 나온 child node 2개 = 2^(2-1)
  - 그래서 위에서부터 차례대로 1-2-4-8-......공비가 2인 등비수열임을 알 수 있다.
- 깊이가 k인 이진트리의 최대 노드 수는 2^k - 1    (k>=1)이다.
  - level이 3까지 있는 깊이 3의 이진 트리가 가질수 있는 최대 노드의 갯수는 8 - 1(root노드만 1개이기때문에)
  
### Complete Binary Tree (완전 이진 트리)
- 위 그림을 보면 바로 알 수 있을 것이다.
- 다만 완전이라고 해서 child node를 무조건 2개를 갖는다는 의미가 아니고,
- 1개의 child node만 가져도 되는데!! 다만, 이때 child는 좌측에 있어야 한다.(**우측에 있으면 완전 이진 트리가 아님**)

### Heap (힙)
<p align="center"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/38/Max-Heap.svg/330px-Max-Heap.svg.png"></p>

- 힙(heap)은 최댓값 및 최솟값을 찾아내는 연산을 빠르게 하기 위해 고안된 
- 완전이진트리(complete binary tree)를 기본으로 한 자료구조(tree-based structure)로서 
- 다음과 같은 힙 속성(property)을 만족한다.
  - A가 B의 부모노드(parent node) 이면, A의 키(key)값과 B의 키값 사이에는 대소관계가 성립한다.
  - 여기서 key값은 Prioritized Experience Replay의 TD error로 보면 될 거 같다.
  - 여기서 우리는 parent node의 key값이 child보다 큰 최대 힙방식을 사용할 것이다.
  
  ##### Partial Order?
  - 말그대로 순서는 순서인데 부분적으로 순서형태를 띈다
  - 즉, A라는 노드가 A보다는 위쪽에 위치한 노드보다 key값이 클 수 있다는 말이다.(직계노드(바로윗노드)와 비교한다는 말이 아님!)
  - 반대로 말하면 직계관계에서만 순서가 성립한다는 의미입니다.
  
### Heap Sort (힙 정렬)
- 


