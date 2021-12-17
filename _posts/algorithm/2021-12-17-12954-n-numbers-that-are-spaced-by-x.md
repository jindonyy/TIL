---
title: "<span>프로그래머스</span><span>Lv1</span> x만큼 간격이 있는 n개의 숫자"
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2021-12-17
---

### 문제 설명
함수 solution은 정수 x와 자연수 n을 입력 받아, x부터 시작해 x씩 증가하는 숫자를 n개 지니는 리스트를 리턴해야 합니다. 다음 제한 조건을 보고, 조건을 만족하는 함수, solution을 완성해주세요.

### 제한 조건
* x는 -10000000 이상, 10000000 이하인 정수입니다.
* n은 1000 이하인 자연수입니다.

### 입출력 예
|x|n|return|
|-|-|-|
|2|5|[2,4,6,8,10]|
|4|3|[4,8,12]|
|-4|2|[-4, -8]|

## 답안
#### 나의 풀이
```javascript
function old(x, n) {
  var answer = [];

  for(var i = 1; i <= n; i++){
    answer.push(x * i);
  }

  return answer;
}
```

#### 다른 사람 풀이
```javascript
function solution1(x, n) {
  var answer = [];

  for(var i = 1; i <= n; i++){
    answer[i-1] = x * i;
  }

  return answer;
}
```

```javascript
function solution2(x, n) {
  return Array(n).fill(x).map((v, i) => (i + 1) * v);
}
```