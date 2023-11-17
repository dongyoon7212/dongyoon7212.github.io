---
layout: single
title: 백준 코테 문제 2920번 
categories: 백준
tag: python
toc: true
toc_sticky: true
toc_label: 순간이동
sidebar:
    nav: "counts"
---
# 백준 2920번 : 음계

- - -
##### 문제
다장조는 c d e f g a b C, 총 8개 음으로 이루어져있다. 이 문제에서 8개 음은 다음과 같이 숫자로 바꾸어 표현한다. c는 1로, d는 2로, ..., C를 8로 바꾼다.
1부터 8까지 차례대로 연주한다면 ascending, 8부터 1까지 차례대로 연주한다면 descending, 둘 다 아니라면 mixed 이다.
연주한 순서가 주어졌을 때, 이것이 ascending인지, descending인지, 아니면 mixed인지 판별하는 프로그램을 작성하시오.

- - -
##### 입력
첫째 줄에 8개 숫자가 주어진다. 이 숫자는 문제 설명에서 설명한 음이며, 1부터 8까지 숫자가 한 번씩 등장한다.

- - -
##### 예제 입력1
```python
1 2 3 4 5 6 7 8
```
##### 예제 출력1
```python
ascending
```

##### 예제 입력2
```python
8 7 6 5 4 3 2 1
```
##### 예제 출력2
```python
descending
```

##### 예제 입력3
```python
8 1 7 2 6 3 5 4
```
##### 예제 출력3
```python
mixed
```
- - -
##### 풀이

이 문제는 음계의 개념을 일단 제쳐두고 간단하게 생각해야한다. 숫자의 오름차순, 내림차순에 대한 출력으로 생각해야한다. 먼저 8개의 숫자를 입력 받아야한다.

```python
N=list(map(int,input().split()))
```
N에다가 리스트 형태로 숫자를 입력받는다.

그리고 오름차순인지 내림차순인지에 대한 조건문을 사용한다.
여기서 오름차순 내림차순 판단을 해야하는데 이때는 sorted 함수를 사용한다.
**==sorted는 순서대로 정렬 후 리스트로 반환한다.==**
==**여기서 sorted를 사용할때 기본값은 reverse=False 이다. 바로 오름차순(ASC)으로 출력이 되는것이다.**==
**==반대로 reverse=True라면 내림차순(DESC)가 되는것이다.==**

```python
if N == sorted(N):
    print("ascending")
elif N == sorted(N,reverse=True):
    print("descending")
else:
    print("mixed")
```

- - -
##### 정답
```python
N=list(map(int,input().split()))

if N == sorted(N):
    print("ascending")
elif N == sorted(N,reverse=True):
    print("descending")
else:
    print("mixed")
```
