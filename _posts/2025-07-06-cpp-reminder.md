---
title: C++ 기억할 것들
excerpt: C++ 쓸 때 유용하게 사용되는 것들
categories: [C++]
tags: [C++, tip]
---

### 입출력 빠르게 하기

```cpp
ios_base::sync_with_stdio(false);
cin.tie(0); cout.tie(0);

cout << endl; // 대신에
cout << '\n'; // 이거 쓰기. 훨씬 빠름
```

### Convert String to Integer(float, double...)

```cpp
#include <string>

// 정의
// int stoi (const string& str [, size_t* idx = 0, int base = 10]) : string to int

int integer = stoi("1234", nullptr, 10); // (문자열, nullptr, 진법) 진법의 기본값은 10
int integer = stoi("1234");

// stof, stod 등도 같은 방식으로 사용할 수 있음

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


### vector

```cpp
#include <vector>

// vector 정의
vector<int> v = {2, 4, 7, 9};

// 삭제
#include <algorithm> // remove 쓰기 위해 필요

v.erase(v.begin() + i); // i번째 인덱스의 원소 제거
v.erase(remove(v.begin(), v.end(), 3), v.end()); // 원소 7 제거(값이 7인 모든 요소를 제거)
v.erase(v.begin() + 1, v.begin() + 3); // 인덱스 1부터 인덱스 3까지의 원소 제거

// 할당
vector<int> v; // 함수 밖에서 정의
v.assign(n, 0); // 함수 안에서 n개의 0으로 초기화

// 찾기
cout << find(v.begin(), v.end(), 7) - v.begin(); // 7의 index 반환

if(find(v.begin(), v.end(), 5) == v.end()){ // vector 내에 존재하지 않으면 v.end() 반환
    cout << "not exist";
}

// 모든 요소 더하기
#include <numeric>
int sum = accumulate(v.begin(), v.end(), 0); // 0은 합의 초기값

// pop
int last_element = v.back(); // vector의 마지막 원소 반환
v.pop_back(); // vector의 마지막 원소 제거. 반환 값 없음

// 정렬
#include <algorithm>

// 오름차순 정렬
sort(v.begin(), v.end()); 

// 내림차순 정렬
sort(v.rbegin(), v.rend()); 

bool comp(int a, int b){
    return a > b;
}
sort(v.begin(), v.end(), comp); // false일 경우 swap

```

### set

```cpp
#include <set> // #include <unordered_set>

set<int> s;

// 삽입
s.insert(1);
s.insert(3);
s.insert(7);

// 제거
s.erase(7); 
s.clear(); // set에 있는 모든 원소 삭제

// 찾기
s.find(3); // 원소 7에 해당하는 iterator 반환

// 기타
s.count(1); // set 내에서 원소 1의 개수 반환
s.empty(); // 비어있으면 true, 아니면 false 반환
s.size(); // 세트에 들어있는 원소으 수 반환

// 특징
// 1. 중복을 허용하지 않음
// 2. 삽입과 제거를 O(log(n))로 실행

```

### map

```cpp
#include <ordered_map> // #include <unordred_map>

// map 정의
ordered_map<int, char> m;

// 삽입
m.insert({1, 'a'}); // {key, value}
m.insert({3, 'b'});
m.insert({6, 'c'});

// key로 value 얻기
cout << m[1] << endl; // 'a' 출력

// key로 삭제
m.erase(3); // key로 제거

// key로 탐색
cout << (m.find(1)) -> first << endl; // key 값 반환 = 1
cout << (m.find(1)) -> second << endl; // value 값 반환 = 'a'

if(m.find(2) == m.end()){
    cout << "Not Found" << endl; // 값이 존재하지 않는 경우 m.end() 반환
}

// map의 value가 vector인 경우
unordered_map<int, vector<int>> tree;

tree[1].emplace_back(2);
tree[2].emplace_back(3);
tree[3].emplace_back(4);
```

### queue
![](\assets\images\2025-07-06-cpp-reminder\image1.png)
```cpp
#include <queue>

// queue 정의
queue<int> q;

// 데이터 추가
q.push(element);

// 데이터 제거
q.pop(); // return 값 없음

// 제일 앞 데이터 반환
q.front();

// 제일 뒤 데이터 반환
q.back();

// 크기 반환
q.size();

// 비었는지 확인
q.empty(); 

// priority queue
priority_queue<int> pq; // max heap
pq.push(4);
pq.push(7);
pq.size();
pq.top();
pq.pop();

priority_queue<int, vector<int>, greater<int>> pq; // min heap
```

### pair

```cpp
#include <vector>

pair<int, int> a;
a=make_pair(2,4);
cout<< a.first;  // 2 출력
cout<< a.second; // 4 출력 
```

### 수학 기호(절댓값, 반올림, 올림, 내림)

```cpp
#include <cmath>

abs(-1); // 절댓값
double ceil(double x); // 올림(double, float, long double)
double floor(double x); // 내림(double, float, long double)
round(3.5); // 반올림

```

### max_element(min_element)

```cpp
#include <algorithm>

vector<int> v = {1, 2, 3, 4};
cout << *max_element(v.begin(), v.end()); // iterator 형태로 반환되므로 * 붙여야 함
cout << *min_element(v.begin(), v.end());
```

### string

```cpp
#include <string>

// 빈 문자열 str 생성
string str; 

// 문자열 str 생성 방식 1
string str = "abc";

// 문자열 str 생성 방식 2
string str;
str = "abc";

// 문자열 str 생성 방식 3
string str("abc");

// str2에 str1 복사
string str2(str1);

// new를 이용해 동적할당
string *str = new string("abc");

// <, >, ==를 통해 문자열끼리 비교할 수 있다
string str1 = "abc";
string str2 = "bcd";
// str1 < str2 은 true
// str1 + "A" 은 "abcA"
// str1 == "abc" 는 true

// 특정 원소에 접근
str.at(index); // index 위치의 문자 반환. 유효한 범위인지 체크함
str[index]; // index 위치의 문자 반환. 유효한 범위인지 체크 안 함. 따라서 접근 더 빠름.
str.front(); // 문자열의 가장 앞 문자 반환
str.back(); // 문자열의 가장 뒤 문자 반환

// 추가, 삭제
str1.append(str2); // str1 뒤에 str2 이어 붙여줌('+'와 같은 역할)
str1.append(str2, n, m); // str1 뒤에 str2의 n번째 인덱스부터 m개의 문자를 이어 붙여줌
str.append(n, 'a'); // str 뒤에 n 개의 'a'를 이어 붙여줌
str1.insert(n, str2); // n번째 index 앞에 str2 문자열을 삽입함
str.clear(); // 저장된 문자열을 모두 지움
str.erase(n, m); // n번째 index부터 m개의 문자를 지움
str.pop_back(); // str 맨 뒤의 문자 제거

// 유용한 멤버 함수
str.find("abc"); // "abc"가 str에 포함되어있는지를 확인. 찾으면 해당 부분의 첫번째 index를 반환
str.find("abc", n); // 위와 비슷하지만, n번째 index부터 "abc"를 find함
str.substr(n); // n번째 index부터 끝까지의 문자를 부분문자열로 반환
str.substr(n, k); // n번째 index부터 k개의 문자를 부분문자열로 반환
swap(str1, str2); // str1과 str2를 바꿔줌. reference를 교환하는 방식
isdigit(c); // c가 숫자면 true, 아니면 false 반환
isalpha(c); // c가 영어면 true, 아니면 false 반환
toupper(c); // c를 대문자로 변환
tolower(c); // c를 소문자로 변환


// string의 크기
str.size(); // 문자열 길이 반환
str.capacity(); // 문자열이 사용 중인 메모리 크기 반환
str.resize(n); // str의 크기를 n으로 만듦. 기존의 문자열 길이가 n보다 크다면 초과하는 부분은 삭제하고, 작다면 빈공간으로 채움.
str.resize(n, 'a'); // 위와 비슷하지만, 빈 공간을 'a'로 채움.
str.shrink_to_fit(); // capacity가 실제 사용하는 메모리보다 큰 경우 낭비되는 메모리가 없도록 메모리를 줄여줌.
str.reserve(n); // str에 n만큼 메모리를 미리 할당해 줌.
str.empty(); // str이 빈 문자열인지 확인




```

### binary search
```cpp
// 반복문으로 구현
bool binary_search(vector<int>& arr, int len, int target){
	int low = 0, high = len - 1;
    
    while(low <= high){
    	int mid = (low + high) / 2;
        
        //원하는 값을 찾았다면 true 반환
        if(target == arr[mid])	return true;
        
        // 원하는 값이 더 작다면 검사 범위를 더 낮게 잡아야 한다.
        if(target < arr[mid]){
        	high = mid - 1;
        }
        // 원하는 값이 더 크다면 검사 범위를 더 크게 잡아야 한다.
        else if(target > arr[mid]){
        	low = mid + 1;
        }
    }
    return false; // 마지막까지 못찾는다면 false 반환
}

// 재귀적으로 구현
bool binary_search(vector<int>& arr, int low, int high, int target){
    if(low > high)	return false;
    int mid = (low + high) / 2;
    
    if(arr[mid] == target)	return true;
    
    // 찾는 수가 더 작다면, 검사 범위를 더 작게 잡아야 한다.
    if(arr[mid] > target)
    	return binary_search(arr, low, mid - 1, target);
        
    // 찾는 수가 더 크가면, 검사 범위를 더 크게 잡아야 한다.
    else
    	return binary_search(arr, mid + 1, high, target);
}

// STL 이용
vector<int> nums;
int target = 3;
bool isFound = binary_search(nums.begin(), nums.end(), target);
// binary_search(반복자.시작점, 반복자.끝점, 찾고자 하는 값);
// 은 찾고자 하는 값을 찾으면 true를, 찾지 못하면 false를 반환한다.
```

### 테스트 케이스 개수 주어지지 않을 때

```cpp
int t;
while(cin >> t){
    cout << t << endl;
}
```

### 무한대

```cpp
// int 타입 무한대
#include <climits>

int inf = INT_MAX;

// float 타입 무한대
#incude <cmath>

float inf = INFINITY;
```