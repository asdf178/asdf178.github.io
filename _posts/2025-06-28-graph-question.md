---
title: 그래프 이론에 대한 고민들
categories: [graph]
tags: [graph, question]
excerpt: 그래프 이론을 공부하며 느낀 고민들과 해결 과정
# show_nav: false
---

## undirected graph traversal에 대한 의문점
### 의문

![](\assets\images\2025-06-28-graph-algorithms\result.gif){: width="90%"}

<figure>
  <img src="\assets\images\2025-06-28-graph-algorithms\2025-06-28 171006.png">
  <figcaption>undirected graph에서 DFT의 방식으로 순회하여 connected components 개수를 세는 코드</figcaption>
</figure>

Undirected graph에서 한 번 방문한 node를 표시해서 infinite loop를 피할 수 있다.

그런데 위의 gif에서 볼 수 있듯이 방문하지 못하는 node가 생길 가능성이 다분하지 않은가?


### 해결

undirected graph인데 directed graph로 오해한 것이 첫 번째 오류였고, DFT임을 간과한 것이 두 번째 오류였다.

```javascript
for (let neighbor of graph[current]){
    explore(graph, neighbor, visited);
}
```

위의 코드에서 모든 neighbor node를 explore한 뒤, recursive한 방식으로 구현된 DFT 알고리즘을 통해 모든 node를 순회할 수 있다.

## DFT를 recursive하게 구현할 때의 의문점
### 의문

방문한 node를 표시하는 visited 리스트가 recursive DFT 함수에서 파라미터로 전달된다. recursive의 층위가 깊어짐에 따라 visited에 추가된 node는 점점 많아진다. 그런데 함수가 return된 후, 상위 함수로 다시 돌아왔을 때 visited에 node가 추가되지 않은 상태이지 않은가?

즉, recursive한 함수를 거치면서 파라미터로 전달되는 visited라는 list에 node가 추가될텐데 하위 함수에서 추가된 node들이 상위 함수의 visited에도 존재하는가?

### 해결

```python
def Recursive(li, n):
    if n == 3:
        return
    n += 1
    li.append(n)
    Recursive(li, n)
    print(li, n)

Recursive([],0)

# 출력 결과
# [1, 2, 3] 3
# [1, 2, 3] 2
# [1, 2, 3] 1
```

위의 코드를 실행한 뒤에 재귀 함수와 리스트의 관계를 확실히 이해할 수 있었다.

파이썬에서 리스트는 참조(reference)로 전달되기 때문에 리스트 같은 mutable한 객체는 함수에 인자로 넘겨질 때 값이 복사되는 것이 아니라, 참조(주소)가 전달된다.

따라서 재귀 함수에서 리스트를 인자로 넘길 때도 계속 같은 리스트를 공유한다. 따라서 visited에 추가된 node는 상위 호출 함수의 visited에서도 추가된 상태가 유지된다.

<div class="notice">
  <h4 style="font-size: 1.2em;">파이썬 리스트 copy</h4><br>
  <strong>shallow copy</strong>: 리스트 자체의 메모리 주소만 복사<br>
  <strong>deep copy</strong>: 리스트의 모든 요소들을 새롭게 복사
</div> 


## DFT, BFT를 iterative하게 구현할 때의 궁금점
### 궁금한 점

stack, queue의 length가 0 이상일 동안 traversal을 함으로써 각 알고리즘을 구현할 수 있는 이유는 무엇일까? 

### 해결

사실 이 궁금증은 DFT, BFT가 코드로 구현되는 과정을 완벽히 이해하지 못해서 생기는 궁금증이기에 알고리즘 구현 코드를 이해하기만 하면 된다. 

알고리즘을 직관적으로 파악하는 것은 매우 힘들다.

 다양한 graph 예제를 통해 알고리즘 작동 과정을 차근차근 따라가면서 곱씹어 보는 것이 이론과 구현을 완전히 습득하는 데에 도움이 된다.

## 왜 visited_global를 사용하는 전략이 틀렸는가
### 의문점

```python
import sys
from collections import deque

def infectedSize(graph, node, visited_global):
    queue = deque()
    queue.appendleft(node)

    visited = set()
    visited.add(node)
    visited_global.add(node)

    size = 0

    while len(queue) > 0:
        current = queue.pop()
        size += 1

        for neighbor in graph[current]:
            if neighbor not in visited:
                queue.appendleft(neighbor)
                visited.add(neighbor)
                visited_global.add(neighbor)
    
    return size

input = sys.stdin.readline
n, m = map(int, input().split())
graph = {}
for i in range(1, n+1):
    graph[i] = []

for _ in range(m):
    a, b = map(int, input().split())
    graph[b].append(a)

counts = []
max = 0
visited_global = set()
for i in range(1, n+1):
    if i in visited_global:
        continue
    size = infectedSize(graph, i, visited_global)
    counts.append((i, size))

    if max < size:
        max = size

most = []
for i in range(len(counts)):
    if counts[i][1] == max:
        most.append(counts[i][0])

print(*sorted(most))
```
[효율적인 해킹](https://www.acmicpc.net/problem/1325) &larr; 백준 1325번 문제

해당 백준 문제를 풀면서 수많은 시간 초과와 메모리 초과를 겪었기에 코드의 비효율성을 해결하기 위해서 visited_global을 도입했다.

이미 방문한 노드를 infectedSize 함수에 넣는 것은 의미가 없다고 생각했다. 왜냐하면 그 노드의 이웃 노드가 감염시킨 컴퓨터의 수(connected component)가 당연히 더 많을 것이고 생각했기 때문이다.

### 해결

![](\assets\images\2025-06-28-graph-question\KakaoTalk_20250630_020310923.jpg){: width="50%"}{: .align-center}

위의 예시에서 노드 1에서 출발하면 모든 노드를 거칠 수 있다. 그러면 visited_global에 모든 노드가 들어가게 된다.

하지만 다른 모든 노드에서 출발해도 모든 노드를 거칠 수 있다는 것이 핵심이다. 즉 위의 예시에서 출력값은 1 2 3 4 5 6이 되어야 하지만 위의 코드에서는 1만 출력된다.

이것이 바로 visited_global을 도입할 때의 문제점이다. 노드 A의 connected component가 n일 때, 노드 A에서 시작된 순회 과정에서 거쳐 지나갔던 노드 B 역시 connected component가 n일 때 수 있으며, n이 모든 connected component 값들 중 가장 클 때 이러한 문제가 생기게 된다.