---
layout: single
title: 백준 코테 문제 10951번 
categories: 백준
tag: python
toc: true
toc_sticky: true
toc_label: 목차
sidebar:
    nav: "counts"
---
# 2023-08-11
# 코딩테스트 준비
백준 10951번


- - -
##### 문제
두 정수 A와 B를 입력받은 다음, A+B를 출력하는 프로그램을 작성하시오.

- - -
##### 입력
입력은 여러 개의 테스트 케이스로 이루어져 있다.
각 테스트 케이스는 한 줄로 이루어져 있으며, 각 줄에 A와 B가 주어진다. (0 < A, B < 10)

- - -
##### 출력
각 테스트 케이스마다 A+B를 출력한다.

- - -
##### 예제 입력
```
1 1
2 3
3 4
9 8
5 2
```

- - -
##### 예제 출력
```
2
5
7
17
7
```

- - -
##### 풀이

이 문제의 경우 몇번의 입력을 받아서 실행해야하는지 명시 되어있지 않다. 그렇기 때문에 while문을 이용해 문제를 풀어본다.
여기서 while문과 try-expept문을 활용한다.
try-except문은 오류를 처리하기 위해 사용한다. try-except문의 기본구조이다.

```python
try:
    ~~~
except [발생오류 [as 오류변수]]:
    ~~~
```

하지만 이 문제에서는 try-except만 사용한다.

```python
while True:
```

먼저 while문의 조건이 참이 되게 한 후 try-except문을 사용한다.

##### 정답

```python
while True:
    try:
        a,b=map(int,input().split())
        print(a+b)
    except:
        break

```

a와 b에 입력값을 받고 더한 값을 출력한다. 여기서 예외로 break를 넣어줬다.
여러번의 입력과 출력을 한 다음 break를 입력하면 멈추게 된다.

결과

```python
1 1
2
2 3
5
3 4
7
9 8
17
5 2
7
break
```
