---
title: C++ 기억할 것들
excerpt: C++ 쓸 때 유용하게 사용되는 것들
categories: [C++]
tags: [C++, tip]
---

### Convert String to Integer

```cpp
#include <string>

// 정의
// int stoi (const string& str [, size_t* idx = 0, int base = 10]) : string to int

int integer = stoi("1234", nullptr, 10); // (문자열, nullptr, 진법) 진법의 기본값은 10
int integer = stoi("1234");

```

### Convert Integer(double, long long...) to String

```cpp
#include <string>

// 정의
// string to_string(int val) : int(double, long long...) to string

string s = to_string(1234);

```

### Delimiter를 기준으로 split한 문자열 입력 받기

```cpp
#include <iostream>
#include <vector>
#include <sstream>
using namespace std;

vector<string> split(string str, char Delimiter){
    istringstream iss(str);
    string buffer;

    vector<string> result;

    while(getline(iss, buffer, Delimiter)){
        result.push_back(buffer);
    }

    return result;
}
```

### bitset 이용하여 2진수 형태로 출력하기

```cpp
#include <iostream>
#include <bitset>
using namespace std;

bitset<8> bit; // 00000000
bitset<8> bit("10101010"); // 문자열 "10101010"로 초기화
bitset<32> bit(127); // 10진수 127로 초기화

bit = 0 // 전체 0
bit = 1 // 전체 1
bit.flip() // 전체 반전

bit[3] = 0; // bit.reset(3);
bit[3] = 1; // bit.set(3, 1);
bit[3] = !bit[3]; // bit.flip(3);

string bit = bit.to_string(); // 문자열로 변환하여 반환

```
<a href="https://notepad96.tistory.com/35" class="btn btn--info">More Info</a>

### vector의 모든 요소 더하기

```cpp
#include <numeric>
using namespace std;

vector<int> numbers = {1, 2, 3};
int sum = accumulate(numbers.begin(), numbers.end(), 0); // 0은 합의 초기값

```