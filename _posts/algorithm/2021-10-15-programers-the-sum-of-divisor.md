---
title: "<span>프로그래머스</span><span>Lv1</span> 약수의 합"
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2021-10-15
---

## 문제 설명
정수 n을 입력받아 n의 약수를 모두 더한 값을 리턴하는 함수, solution을 완성해주세요.

### 제한 조건
* n은 0 이상 3000이하인 정수입니다.

### 입출력 예

|n|return|
|-|-|
|12|28|
|5|6|

### 입출력 예 설명
#### 입출력 예 #1
12의 약수는 1, 2, 3, 4, 6, 12입니다. 이를 모두 더하면 28입니다.

### 입출력 예 #2
5의 약수는 1, 5입니다. 이를 모두 더하면 6입니다.

## 답안
#### 나의 풀이
```javascript
function solution(n) {
  var answer = 0;
  
  for(var i = 1; i <= n; i++) {
    if(n % i == 0) answer += i;
  }
  
  return answer;
}
```

#### 옛날 풀이
```javascript
function solution(n) {
  var answer = 0;

  for( var i = 1; i <= n; i++ ){
    if (n/i === parseInt(n/i, 10)){
      answer += n/i;
    }
  }

  return answer;
}
```