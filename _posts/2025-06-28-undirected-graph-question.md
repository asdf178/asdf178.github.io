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

directed graph처럼 생각한 것이 첫 번째 오류였고, DFT임을 간과한 것이 두 번째 오류였다.

```javascript
for (let neighbor of graph[current]){
    explore(graph, neighbor, visited);
}
```

위의 코드에서 모든 neighbor node를 explore한 뒤, recursive한 방식으로 구현된 DFT 알고리즘을 통해 모든 node를 순회할 수 있다.