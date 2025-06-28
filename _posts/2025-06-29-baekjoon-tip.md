---
title: "백준 팁들"
categories: [baekjoon]
tags: [baekjoon, tip]
excerpt: baekjoon 문제를 풀며 얻은 다양한 팁들
---

### input 느려서 시간 초과날 때

```python
import sys

input = sys.stdin.readline

```

### list 대신 set

list에서 search 할 때의 시간 복잡도는 O(n)이지만,<br>
set에서 search 할 때의 시간 복잡도는 O(1)이므로 더 빠르고 효율적으로 검색할 수 있다.

```python
li = []
st = set()
```

### deque

```python
from collections import deque

q = deque([1, 2, 3])
q.append(4) # [1, 2, 3, 4]

q.appendleft(0) # [0, 1, 2, 3, 4]

q.pop() # 4, q = [0, 1, 2, 3]

q.popleft() # 0, q = [1, 2, 3]

```