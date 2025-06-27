---
title: 그래프 이론 내용 정리
categories: [graph]
tags: [graph]
excerpt: 유튜브 강좌를 보고 Graph Algorithm 내용 정리
---

## Graph

다양한 알고리즘 문제를 그래프 문제로 치환하여 풀이할 수 있기에 그래프 이론이 유용하게 활용될 수 있다.

![2025-06-28-000447](\assets\images\2025-06-28-graph-algorithms\2025-06-28-000447.png){: width="70%"}

![2025-06-28-000529](\assets\images\2025-06-28-graph-algorithms\2025-06-28-000529.png)

![2025-06-28-000601](\assets\images\2025-06-28-graph-algorithms\2025-06-28-000601.png){: width="70%"}

![2025-06-28-010511](\assets\images\2025-06-28-graph-algorithms\2025-06-28-010511-1751040531608-7.png) 

graph를 프로그래밍 코드로 다루기 위해서 adjacency list를 만든다. adjacency list는 hash map을 통해 구현된다. key는 모든 노드이고, value는 각 노드와 edge로 연결된 모든 neighbor node다.

## DFT, BFT

![2025-06-28-011420](\assets\images\2025-06-28-graph-algorithms\2025-06-28-011420.png)

**DFT(Depth first traversal)**, **BFT(Breadth first traversal)**은 traversal(순회)하면서 탐색하는 탐색 알고리즘이다. 

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

## 출처
[Graph Algorithms for Technical Interviews - Full Course](https://www.youtube.com/watch?v=tWVWeAqZ0WU)
