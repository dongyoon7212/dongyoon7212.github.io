---
layout: single
title: (알고리즘)선형검색 이해하기
categories: 공부노트
tag: 알고리즘
toc: true
toc_sticky: true
toc_label: 순간이동
sidebar:
    nav: "counts"
---

# 선형검색(Linear Search)란?

- - -

배열이나 리스트의 처음부터 끝까지 하나씩 값을 비교하면서 찾고자 하는 값을 찾을 때까지 탐색하는 방법

### 선형검색의 원리
1. 배열 또는 리스트를 순환한다.
2. 순환하면서 찾고자 하는 값을 하나씩 비교한다.
3. 찾고자 하는 값을 찾게 된다면 순환을 멈추고 값을 반환한다.

### 선형검색의 특징
- 선형검색은 리스트나 배열이 정렬되어 있지 않은 상태에서만 사용된다.
- 탐색속도가 느리다
- 탐색범위가 처음부터 끝이다.
- for/while 루프를 사용한다.
- 입력 크기와 비례하는 실행 시간

### 선형검색의 시간 복잡도
O(N)

예를들어 100개 중 1개를 찾는거라면
N=100 K=1
K * O(N) = O(K*N) = O(100)

### 선형검색을 사용하기 좋을때
- 데이터의 크기가 크지 않거나 정렬되어 있지 않은 경우

### 선형검색 코드 만들어보기
JavaScript의 indexOf함수를 쓰지않고 배열을 중 원하는 값 찾기
값을 찾으면 인덱스 값을 출력하고 못 찾으면 -1을 출력

```javascript
function linearSearch(arr, val){
    for(var i = 0; i < arr.length; i++){
        if(arr[i] === val) return i;
    }
    return -1;
}
linearSearch([34,56,1,2],1)
```
결과
`2`

여기서 시간 복잡도는 O(4)가 된다.
