---
layout: single
title: (프로그래머스)최빈값 구하기
categories: 프로그래머스
tag: [알고리즘, JavaScript]
toc: true
toc_sticky: true
toc_label: 순간이동
sidebar:
    nav: "counts"
---

- - -
#### 문제
최빈값은 주어진 값 중에서 가장 자주 나오는 값을 의미합니다. 정수 배열 array가 매개변수로 주어질 때, 최빈값을 return 하도록 solution 함수를 완성해보세요. 최빈값이 여러 개면 -1을 return 합니다.
- - -

#### 제한사항
* 0 < array의 길이 < 100
* 0 ≤ array의 원소 < 1000

- - -

#### 입출력 예
|array|result|
|-----------|--------|
|[1, 2, 3, 3, 3, 4]|3|
|[1, 1, 2, 2]|-1|
|[1]|1|

- - -

#### 입출력 예 설명
입출력 예 #1
- [1, 2, 3, 3, 3, 4]에서 1은 1개 2는 1개 3은 3개 4는 1개로 최빈값은 3입니다.
입출력 예 #2
- [1, 1, 2, 2]에서 1은 2개 2는 2개로 최빈값이 1, 2입니다. 최빈값이 여러 개이므로 -1을 return 합니다.
입출력 예 #3
- [1]에는 1만 있으므로 최빈값은 1입니다.
- - -

먼저 정답을 맞춘 코드이다.

```
function solution(array) {
    let map = new Map()
    
    if(array.length === 1){
        return array[0]
    } 
    
    for(let i=0; i<=Math.max(...array); i++){
        map.set(i,0)
    }
    
    for(let i=0; i<array.length; i++){
        map.set(array[i], map.get(array[i])+1)
    }
    
    const arr = Array.from(map.values())
    const max = Math.max(...arr)
    
    if(arr.indexOf(max) !== arr.lastIndexOf(max)){
        return -1
    }else{
        return arr.indexOf(max)
    }
    
}
```

하나씩 뜯어서 보자

```
let map = new Map()
    
    if(array.length === 1){
        return array[0]
    } 
```
먼저 Map()함수를 이용하여 key-value로 이루어진 map을 선언한다.

그리고 if문을 사용해 array의 배열 길이가 1인 경우 그 배열을 출력하도록 한다.

여기 까지는 어려운게 없었다…

```
for(let i=0; i<=Math.max(...array); i++){
        map.set(i,0)
    }
```
여기부터가 문제였다.

for문을 이용하여 루프를 위하여 카운터 변수 i를 0으로 초기화 하고 
i<=Math.max(...array) : 배열 array의 최대값을 구하고 범위로 지정한다.
map.set(i,0) : 앞에 선언했던 key-value으로 이루어진 map에 추가한다.

map.set(i,0)은 아래와 같이 추가되게 된다.
```
map.set(0, 0);
map.set(1, 0);
map.set(2, 0);
map.set(3, 0);
```

다음으로 두번째 루프이다.
```
for(let i=0; i<array.length; i++){
        map.set(array[i], map.get(array[i])+1)
    }
```
똑같이 카운터 변수 i를 0으로 초기화 하고 범위를 array.length로 array의 길이로 지정한다.
map.set(array[i], map.get(array[i])+1) : map.set으로 (array[i], map.get(array[i])+1)을 다시 추가하게 된다.

map.set(array[i], map.get(array[i])+1) 을 풀어서 보자면
```
i = 0일때 array[i] = 1

map.set(1, map.get(1) + 1);
```

```
map: {
  0 => 0,
  1 => 1,
  2 => 0,
  3 => 0
}
```

```
i = 1일때 array[i] = 2
map.set(2, map.get(2) + 1);
```

```
map: {
  0 => 0,
  1 => 1,
  2 => 1,
  3 => 0
}
```
이런식으로 순환을 하면서 숫자를 카운트하여 숫자의 빈도값을 저장하게 된다.

최종적으로는
```
map: {
  0 => 0,
  1 => 2,
  2 => 2,
  3 => 1
}
```

마지막으로
```
const arr = Array.from(map.values())
const max = Math.max(...arr)
    
if(arr.indexOf(max) !== arr.lastIndexOf(max)){
    return -1
}else{
    return arr.indexOf(max)
}
```
Array.from()을 사용해 map.values() 즉 map의 값들을 불러와 arr에 선언한다.
Math.max(…arr)는 arr의 최대값을 구한다.

if문을 사용해 arr.indexOf(max) 즉 arr의 최대값을 찾아내 arr.LastIndexOf(max)와 비교하여 같지 않다면 -1을 출력하게 된다. 이 의미는 처음 찾은 최대값과 마지막 최대값을 비교하게 되는데 만약 같지 않다면 최대값이 1개 이상 존재하게 되는 것으로 같지 않다면 -1을 출력하게 되는 것이다.

나머지는 arr.indexOf(max)로 최대값이 한개만 존재할때 해당하는 숫자를 출력하게 되는것이다.
- - -
#### 새로 알게 된 점

이번 문제를 풀면서 많은 걸 알게 되었다. 먼저 map.set과 map.get함수에 대해 더 자세히 알게되었다.
map.set(key, value) : key를 이용해 value를 저장하는것으로 key-value형태이다.
map.get(key) : key에 해당하는 value를 반환하는것으로, key가 존재하지 않으면 undefined를 반환하게 된다.

또 Array.from()함수는 다른 배열로부터 새로운 배열을 생성하는것을 의미한다.
