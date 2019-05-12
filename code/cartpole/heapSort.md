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

- 힙(heap)은 **최댓값 및 최솟값을 찾아내는 연산을 빠르게** 하기 위해 고안된 
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
- [여기](https://zeddios.tistory.com/56)를 참고하여 작성하였습니다.

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory&fname=http%3A%2F%2Fcfile25.uf.tistory.com%2Fimage%2F21762B3F58FCBCFC2D0B7D">
</p>

  ##### 특성
  - 노드 i의 부모 노드 인덱스 :   i/2, (단, i > 1)
  - 노드 i의 왼쪽 자식 노드 인덱스 : 2 x i
  - 노드 i의 오른쪽 자식 노드 인덱스 : (2 x i) + 1 (= 왼쪽 자식 노드 인덱스 + 1)
  
  ##### 정렬 과정 (위키피디아 방식)
  1) n개의 노드에 대한 완전 이진 트리를 구성한다. 이때 루트 노드부터 부모노드, 왼쪽 자식노드, 오른쪽 자식노드 순으로 구성한다.
  2) 최대 힙을 구성한다. 단말 노드를 자식노드로 가진 부모노드부터 구성하며 아래부터 루트까지 올라오며 순차적으로 만들어 갈 수 있다.
  3) 가장 큰 수(루트에 위치)를 가장 작은 수와 교환한다.
  4) 2와 3을 반복한다.
  
  ##### 정렬 과정 (내가 이해한 방식)
  <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory&fname=http%3A%2F%2Fcfile29.uf.tistory.com%2Fimage%2F2768113358FED94306C2B3">
  </p>

  - 최대힙 : parent node의 key값은 무조건 child node보다 커야한다.(직계관계임을 유의하자)
  1) 정렬이 안된 배열을 받아 heap(=완전이진트리)을 구성하고, 최대 힙을 구성한다.
  <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory&fname=http%3A%2F%2Fcfile10.uf.tistory.com%2Fimage%2F2209203B58FEDB65151D4D">
  </p>

    1-1) 최대 힙을 구성할때, 맨 아랫단의 parent-child key값을 비교한다.(빨간 세모)
    1-2) 7,15,14 --> 9,12,10이후에 11,8,6이 아닌 3이 parent node의 key값인 빨간세모의 key값을 비교한다.
  <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory&fname=http%3A%2F%2Fcfile5.uf.tistory.com%2Fimage%2F2235814058FEDFAC115B3A">
  </p>
  
  <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory&fname=http%3A%2F%2Fcfile26.uf.tistory.com%2Fimage%2F267C604E58FEE0BA065B77">
  </p>
    
    1-3) 위 그림과 같이 3이 맨 아래 노드로 내려가고(;재귀방식) 최대 힙을 만족하면 11,8,6으로 넘어갑니다.
  <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory&fname=http%3A%2F%2Fcfile8.uf.tistory.com%2Fimage%2F225FFA4C58FEE1870319E4">
  </p>
  
  <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory&fname=http%3A%2F%2Fcfile8.uf.tistory.com%2Fimage%2F21223E4D58FEE27E139E74">
  </p>
  
  <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory&fname=http%3A%2F%2Fcfile30.uf.tistory.com%2Fimage%2F2711413458FEE3272F9AB7">
  </p>
  
  <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory&fname=http%3A%2F%2Fcfile10.uf.tistory.com%2Fimage%2F27450A3958FEE37720BE12">
  </p>
  
    1-4) 위와 같이 오른쪽 sub tree도 진행해줍니다.
    
  <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory&fname=http%3A%2F%2Fcfile7.uf.tistory.com%2Fimage%2F2723984558FEE6382794C6">
  </p>
  
  <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory&fname=http%3A%2F%2Fcfile3.uf.tistory.com%2Fimage%2F23278C4658FEE68511CF5F">
  </p>
  
  <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory&fname=http%3A%2F%2Fcfile21.uf.tistory.com%2Fimage%2F25704B3D58FEE6B21BDAEE">
  </p>
  
  <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory&fname=http%3A%2F%2Fcfile26.uf.tistory.com%2Fimage%2F2572874158FEE6DE0E718F">
  </p>
  
  <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory&fname=http%3A%2F%2Fcfile29.uf.tistory.com%2Fimage%2F215A8C3858FEE82E184967">
  </p>
  
     1-5) 결과적으로 위와 같이 정렬되고, root node였던 1이 leaf까지 내려왔다.
     1-6) root-->leaf까지 내려온 최악의 경우, O(logN)만큼 내려올 수 있다.(; N : 데이터수) 

  2) delete로 정렬한다. delete자체에 큰 의미를 두지 말고 순서는 다음과 같다.
  
    2-1) root 노드와 인덱스가 맨 마지막인 노드(우측 맨아래)를 바꿔준다.(값 change)
    2-2) 우측 맨아래로 간 이전 root 노드는 없는셈쳐라. 그리고 바뀐 root 노드를 가지고 최대힙을 다시 구성해라
   
   <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory&fname=http%3A%2F%2Fcfile9.uf.tistory.com%2Fimage%2F2636945058FF07F52D1E9D">
  </p>
  
    2-3) 이렇게 하면 위 그림과 같이 정렬이 된다고 한다..(짱신기?!)
    
