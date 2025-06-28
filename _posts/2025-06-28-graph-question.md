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

