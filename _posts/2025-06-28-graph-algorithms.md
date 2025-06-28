---
title: 그래프 이론 내용 정리
categories: [graph]
tags: [graph]
excerpt: 유튜브 강좌를 보고 Graph Algorithm 내용 정리
---

# Graph

다양한 알고리즘 문제를 그래프 문제로 치환하여 풀이할 수 있기에 그래프 이론이 유용하게 활용될 수 있다.

![2025-06-28-000447](\assets\images\2025-06-28-graph-algorithms\2025-06-28-000447.png){: width="70%"}{: .align-center}

![2025-06-28-000529](\assets\images\2025-06-28-graph-algorithms\2025-06-28-000529.png)

![2025-06-28-000601](\assets\images\2025-06-28-graph-algorithms\2025-06-28-000601.png){: width="70%"}{: .align-center}

![2025-06-28-010511](\assets\images\2025-06-28-graph-algorithms\2025-06-28-010511-1751040531608-7.png) 

graph를 프로그래밍 코드로 다루기 위해서 adjacency list를 만든다. adjacency list는 hash map을 통해 구현된다. key는 모든 노드이고, value는 각 노드와 edge로 연결된 모든 neighbor node다.

## Directed graph

![2025-06-28-011420](\assets\images\2025-06-28-graph-algorithms\2025-06-28-011420.png)

**DFT(Depth first traversal)**, **BFT(Breadth first traversal)**은 Directed graph를  traversal(순회)하면서 탐색하는 탐색 알고리즘이다. 

(traversal은 그래프나 트리와 같은 연결 구조에서 노드를 방문하는 데 활용된다.)

**DFT**은 **깊이 우선 탐색**으로 **Stack** 구조가 사용된다.

**BFT**은 **너비 우선 탐색**으로 **Queue** 구조가 사용된다.

<div class="notice">
  <ul>
    <li>
      <strong>Stack</strong>: Last in First Out(LIFO)<br>
      push를 통해 data가 top에 쌓이고, pop을 통해 data를 top에서 제거<br>
      한쪽에서 데이터가 들어오고 제거됨<br><br>
    </li>
    <li>
      <strong>Queue</strong>: First in First Out(FIFO)<br>
      push 또는 Enqueue를 통해 data가 들어오고, pop을 통해 data를 제거<br>
      한쪽에서는 데이터가 들어오고, 다른 쪽에서는 데이터가 제거됨<br>
    </li>
  </ul>
</div>

### DFT 구현

<figure>
  <img src="\assets\images\2025-06-28-graph-algorithms\2025-06-28-125710.png">
  <figcaption>iterative한 방식으로 DFT 구현</figcaption>
</figure>

출력 결과: a c e b d f

neighbor node들의 순서에 따라 출력 결과가 달라질 수 있지만, 여전히 BFT 탐색이다.

<figure>
  <img src="\assets\images\2025-06-28-graph-algorithms\2025-06-28-130607.png">
  <figcaption>recursive한 방식으로 DFT를 구현</figcaption>
</figure>

neighbor가 없는 node들이 base case 역할을 한다.

출력 결과: a c e b d f

### BFT 구현

<figure>
  <img src="\assets\images\2025-06-28-graph-algorithms\2025-06-28-134616.png">
  <figcaption>iterative 방식으로 BFT를 구현</figcaption>
</figure>

BFT는 iterative 방식으로만 구현할 수 있다.

출력 결과: a c b e d f

<div class="notice">
  <h4 class="" style="font-size: 1.2em;">In JavaScript</h4><br>
  <strong>shift</strong>: remove the first element<br>
  <strong>push</strong>: add element at the end
</div>

DFT와 BFT를 iterative하게 구현한 코드는 거의 동일하다.<br>
딱 한 가지 다른 점은 DFT는 pop()을 통해 node를 제거하고, BFT는 shift()를 통해 node를 제거하는 것이다.

### 그래프로 문제 해결

### Has Path
![asdf](\assets\images\2025-06-28-graph-algorithms\2025-06-28 135459.png)

cycle은 node 간의 연결이 끊임없이 이어지는 것을 의미하고, infinity loop를 이룬다.<br>
acycle은 cycle이 존재하지 않는다는 의미이다.

![asdf](\assets\images\2025-06-28-graph-algorithms\2025-06-28 140224.png){: width="70%"}{: .align-center}

source node가 f, destination node가 k일 때 f에서 출발해서 k까지 도달할 수 있는 경로가 있는지 판단하는 문제를 **has path**라고 한다.

![asdf](\assets\images\2025-06-28-graph-algorithms\2025-06-28 140632.png)

src node에서 dst node로 도달할 수 있을 때 True다.

![asdf](\assets\images\2025-06-28-graph-algorithms\2025-06-28 140617.png)

src node에서 dst node로 도달할 수 없을 때 False다.

**n = node의 개수**, **e = edge의 개수**라고 할 때, 시간 복잡도와 공간 복잡도는 아래의 두 방식으로 계산할 수 있다.

<p align="center">
  <img src="\assets\images\2025-06-28-graph-algorithms\2025-06-28 141336.png" width="40%">
  <img src="\assets\images\2025-06-28-graph-algorithms\2025-06-28 141342.png" width="40%">
</p>

#### 구현

![asdf](\assets\images\2025-06-28-graph-algorithms\2025-06-28 140224.png){: width="40%"}{: .align-center}
<figure>
  <img src="\assets\images\2025-06-28-graph-algorithms\2025-06-28 144933.png">
  <figcaption>DFT을 recursive하게 구현해서 해결</figcaption>
</figure>

<figure>
  <img src="\assets\images\2025-06-28-graph-algorithms\2025-06-28 150527.png">
  <figcaption>BFT을 iterative하게 구현해서 해결</figcaption>
</figure>

## Undirected graph

![asdf](\assets\images\2025-06-28-graph-algorithms\2025-06-28 150839.png)

undirected graph를 왼쪽과 같이 나타낼 때는 두 node가 서로 연결되어 있음을 나타낸다.<br>
프로그래밍할 때의 편의를 위해서 왼쪽 표현을 오른쪽과 같은 adjacency list로 변환한다.

### traversal 구현

<figure>
  <img src="\assets\images\2025-06-28-graph-algorithms\2025-06-28 163701.png">
  <figcaption>edges를 adjacency list로 변환하는 함수</figcaption>
</figure>

![](\assets\images\2025-06-28-graph-algorithms\2025-06-28 164557.png)

undirected graph에서 nodeA부터 nodeB까지의 has Path를 문제하는 코드다.

### connected components count 구현

![](\assets\images\2025-06-28-graph-algorithms\2025-06-28 165702.png)

서로 연결되지 않아 독립되어 있는 node의 집합이 총 몇 개인지 세는 것이 connected components count다. 

![](\assets\images\2025-06-28-graph-algorithms\2025-06-28 171006.png)

위의 코드를 통해 구현할 수 있다.























# 출처

[Graph Algorithms for Technical Interviews - Full Course](https://www.youtube.com/watch?v=tWVWeAqZ0WU)
