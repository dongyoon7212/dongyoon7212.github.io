---
layout: single
title: 백준 코테 문제 8393번 
categories: 백준
tag: python
toc: true
toc_sticky: true
toc_label: 목차
sidebar:
    nav: "counts"
---
2023-07-28
# 코딩테스트 준비
백준 3단계 반복문 8393번


#### 문제
n이 주어졌을 때, 1부터 n까지 합을 구하는 프로그램을 작성하시오.

#### 입력
첫째 줄에 n (1 ≤ n ≤ 10,000)이 주어진다.

#### 출력
1부터 n까지 합을 출력한다.

#### 예제 입력1
`3`

#### 예제 출력1
`6`

먼저 출력을 위한 입력 코드를 적는다.
```python
A=int(input())
```
A에 정수로 입력값을 받는다.

그리고 합을 출력하기 위해 total이라는 변수를 만든다.
```python
total = 0
```

이제 1부터 A만큼의 합을 출력하기 위해 for문을 사용한다.
```python
for i in range(A+1):
    total = total + i
```

여기서 `range(A+1)`을 한 이유는 변수A의 직전까지만 범위가 적용되기 때문에 변수A만큼의 범위를 지정하려면 +1을 해주어야 한다.

결과적으로
```python
A=int(input())
total = 0

for i in range(A+1):
    total = total + i

print(total)
```
이러한 코드가 나온다.

예제 입력1을 넣었을때 결과로
```python
/usr/local/bin/python3.11 /Users/dongyoon/Desktop/Python/practice2.py 
3
6

Process finished with exit code 0
```
결과값으로 6이 나오므로 예제는 정상적으로 출력되는것을 볼 수 있다.

임의로 다른 값을 넣어본다.

6을 넣었을때 결과로
```python
/usr/local/bin/python3.11 /Users/dongyoon/Desktop/Python/practice2.py 
6
21

Process finished with exit code 0
```
결과값 21이 정상적으로 나온다.

이렇게 8393번을 풀게 되었다.
