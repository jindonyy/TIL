---
title: "<span>프로그래머스</span><span>Lv1</span> 두 정수 사이의 합"
header:
  teaser: /assets/images/algorithm/programmers_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2021-10-20
---

## 문제 설명
두 정수 a, b가 주어졌을 때 a와 b 사이에 속한 모든 정수의 합을 리턴하는 함수, solution을 완성하세요.  
예를 들어 a = 3, b = 5인 경우, 3 + 4 + 5 = 12이므로 12를 리턴합니다.

### 제한 사항
* a와 b가 같은 경우는 둘 중 아무 수나 리턴하세요.
* a와 b는 -10,000,000 이상 10,000,000 이하인 정수입니다.
* a와 b의 대소관계는 정해져있지 않습니다.

### 입출력 예

|a|b|return|
|-|-|-|
|3|5|12|
|3|3|3|
|5|3|12|

## 답안
#### 나의 풀이
```javascript
function sumFun(min, max) {
  var sum = 0;
  while(min <= max) {
    sum += min;
    min++;
  }
  return sum;
}

function solution(a, b) {
  if(a == b) return a;
  return a < b ? sumFun(a, b) : sumFun(b, a);
}
```
a와 b가 같을 경우 sumFun을 타지않고 바로 return해주려고 if절을 넣었는데 효율성은 비슷한 듯 하다.

```javascript
function sumFun(min, max) {
  var sum = 0;
  while(min <= max) {
    sum += min;
    min++;
  }
  return sum;
}

function solution(a, b) {
  if(a == b) return a;
  var min = Math.min(a, b);
  var max = Math.max(a, b);
  return sumFun(min, max);
}
```
min, max로도 풀어보기  
효율성은 더 떨어지는 듯하다.

#### 옛날 풀이
```javascript
function sumFun(v1, v2) {
  var sum = 0;
  while(v1 <= v2) {
    sum += v1;
    v1++;
  }
  return sum;
}

function solution(a, b) {
  return a < b ? sumFun(a, b) : sumFun(b, a);
}
```

#### 다른 사람 풀이
```javascript
function adder(a, b){
  var result = 0

  return (a+b)*(Math.abs(b-a)+1)/2;
}
```
가우스 재림

```javascript
function adder(a, b, s = 0){
  for (var i = Math.min(a, b); i <= Math.max(a, b); i++) s += i;
  return s;
}
```
min, max를 생각했으나 for문 안에 넣을 생각을 못했다.

