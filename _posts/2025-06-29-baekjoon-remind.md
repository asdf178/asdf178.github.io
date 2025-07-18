---
title: "기억해 둘 백준 문제들"
categories: [baekjoon]
tags: [baekjoon]
excerpt: "해결 과정에서 많은 것을 배운 백준 문제들"
---

### 1325번

- python보다 PyPy3가 더 효율적이다.
- 최댓값 또는 최솟값과 관련된 탐색을 할 때, 2개의 for문을 1개로 [대체할 수 있는 방법](/baekjoon/baekjoon-tip/#for%EB%AC%B8-2%EB%B2%88-%EC%93%B0%EB%8A%94-%EB%8C%80%EC%8B%A0-%EC%93%B8-%EC%88%98-%EC%9E%88%EB%8A%94-%EC%BD%94%EB%93%9C)을 찾음.
- memoization에 대해 알게 됨.
- iterative한 방식이 백준에서는 recursive한 방식보다 항상 더 유리한 줄 알았는데, memoization과 recursive한 방식을 결합하면 recursive를 보다 효율적으로 수행할 수 있음을 알게 됨.
- C++에서 시간복잡도를 줄이기 위해서 무조건적으로 unordered_map을 쓸 것이 아니라, 정해진 index를 통해서 데이터에 접근할 수 있다면 이중 vector를 사용하는 것이 더 빠를 수 있다.

### 28245번

- 최솟값, 최댓값 찾을 때 배열을 활용하는 것보다 크기 비교를 위한 변수를 몇 개 선언해서 이를 통해 비교하는 것이 더 효율적이다.
- 시간 초과 걱정한다고 조심스럽게 코딩하지 말고, 일단 가장 간단한 초기 아이디어부터 실현시켜본다. 그 후에 코드를 최적화해도 늦지 않다.