---
layout: single
title: 백준 코테 문제 25304번 
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
백준 3단계 반복문 25304번 영수증


- - -
#### 문제
준원이는 저번 주에 살면서 처음으로 코스트코를 가 봤다. 정말 멋졌다. 그런데, 몇 개 담지도 않았는데 수상하게 높은 금액이 나오는 것이다! 준원이는 영수증을 보면서 정확하게 계산된 것이 맞는지 확인해보려 한다.
영수증에 적힌,
* 구매한 각 물건의 가격과 개수
* 구매한 물건들의 총 금액

⠀을 보고, 구매한 물건의 가격과 개수로 계산한 총 금액이 영수증에 적힌 총 금액과 일치하는지 검사해보자.
- - -
#### 입력
첫째 줄에는 영수증에 적힌 총 금액 X가 주어진다.
둘째 줄에는 영수증에 적힌 구매한 물건의 종류의 수 N이 주어진다.
이후 N개의 줄에는 각 물건의 가격 a와 개수 b가 공백을 사이에 두고 주어진다.
- - -
#### 출력
구매한 물건의 가격과 개수로 계산한 총 금액이 영수증에 적힌 총 금액과 일치하면 Yes를 출력한다. 일치하지 않는다면 No를 출력한다.
- - -
#### 제한
* 1 ≤ X ≤ 1 000 000 000
* 1 ≤ N ≤ 100
* 1 ≤ a ≤ 1 000 000
* 1 ≤ b ≤ 10

- - -
#### 예제 입력1
```
260000
4
20000 5
30000 2
10000 6
5000 8
```

- - -
#### 예제 출력1
```
Yes
```

영수증에 적힌 구매할 물건들의 목록으로 계산한 총 금액은 20000 × 5 + 30000 × 2 + 10000 × 6 + 5000 × 8 = 260000원이다. 이는 영수증에 적힌 총 금액인 260000원과 일치한다. 
- - -
#### 예제 입력2
```
250000
4
20000 5
30000 2
10000 6
5000 8
```

- - -
#### 예제 출력2
```
No
```

- - -
#### 풀이
먼저 영수증에 적힌 총 금액은 total, 구입한 물건의 총 개수는 things, 실제 물건의 총 가격은 sum으로 변수를 지정하고 입력값을 받는다.

```
total = int(input())
things = int(input())
sum = 0
```

그리고 물건의 개수인 things만큼 물건의 가격과 개수를 입력값을 받는다.

이때 for문을 이용하고 range는 things로 한다. 또 물건의 가격은 price, 해당 물건의 개수는 count로 변수를 지정하고 things만큼 입력값을 받는다.

여기서 입력한 물건의 가격과 해당 물건의 개수를 입력받은 후 실제 물건의 총 가격인 sum에 더해준다.

```
for i in range(things):
    price,count=map(int,input().split())
    sum += price*count
```

그리고 total의 값과 sum의 값이 일치할 경우 “Yes”를 출력하고 일치하지 않을 경우 “No”라고 출력을 해야한다.

이것은 if문을 이용해 조건을 설정한다. 그리고 조건이 참이라면 “Yes”를 출력하고 거짓이라면 “No”를 출력한다.

```
if total == sum:
    print("Yes")
else:
    print("No")
```
#### **정답**
총 정리를 하면
```
total = int(input())
things = int(input())
sum = 0

for i in range(things):
    price,count=map(int,input().split())
    sum += price*count

if total == sum:
    print("Yes")
else:
    print("No")
```

예제 입력1을 해본다.
```
/usr/local/bin/python3.11 /Users/dongyoon/Desktop/Python/practice2.py 
260000
4
20000 5
30000 2
10000 6
5000 8
Yes

Process finished with exit code 0
```
값이 일치하여 정상적으로 “Yes”가 출력되는 것을 볼 수 있다.

예제 입력2를 해본다.
```
/usr/local/bin/python3.11 /Users/dongyoon/Desktop/Python/practice2.py 
250000
4
20000 5
30000 2
10000 6
5000 8
No

Process finished with exit code 0
```
값이 일치하지 않아 “No”가 출력되는 것을 볼 수 있다.
