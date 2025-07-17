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

### for문 2번 쓰는 대신 쓸 수 있는 코드
```python
result = []
max = 0
for i in range(1, n+1):
    size = Function(i) # 숫자를 return 하는 임의의 함수

    if max < size:
        max = size
        result = [i]
    elif max == size:
        result.append(i)
```

일반적으로는 size를 리스트에 저장한 뒤, max 값 구하는 for문과 max와 일치하는 값을 찾기 위한 for문 두 개를 구현했을 것이다. 하지만 위와 같이 하나의 for문으로 구현할 수도 있고, 이를 통해 시간 복잡도를 줄일 수 있다.

### Memoization을 통해 시간 복잡도 줄이기

**메모이제이션(Memoization)**은 이미 계산한 결과를 저장해 두었다가, 같은 입력이 들어오면 다시 계산하지 않고 저장된 값을 바로 사용하는 기법이다.

코드 실행 시간을 줄이고, 불필요한 중복 계산을 줄일 수 있다.

### C++ 시간 복잡도

백준 1325번 효율적인 해킹을 풀 때 unordered_map으로 했을 때는 시간 초과가 떴지만, 이중 vector로 했을 때는 시간 초과가 뜨지 않았다. unordered_map의 시간 복잡도가 O(1)이기 때문에 당연히 이중 vector보다 빠를 것이라고 단순히 생각한 것이 오류였다.

잘 생각해보면 이중 vector로 구현한 것이 더 빠를 수 밖에 없다.

### 시간 복잡도 면에서 vector VS set

vector<vector<int>>보다는 vector<unordered_set<int>>가 erase에 좋을 수 있다. 하지만 vector의 크기가 작거나 탐색만 한다면 vector가 더 빠르다.