---
title: "<span>프로그래머스</span><span>Lv1</span> 소수 찾기"
header:
  teaser: /assets/images/algorithm/programmers_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2022-01-02
---

## 문제 설명
1부터 입력받은 숫자 n 사이에 있는 소수의 개수를 반환하는 함수, solution을 만들어 보세요.  
소수는 1과 자기 자신으로만 나누어지는 수를 의미합니다.  
(1은 소수가 아닙니다.)

### 제한 조건
* n은 2이상 1000000이하의 자연수입니다.

### 입출력 예

|n|result|
|-|-|
|10|4|
|5|3|

### 입출력 예제
##### 입출력 예 #1
1부터 10 사이의 소수는 [2,3,5,7] 4개가 존재하므로 4를 반환

##### 입출력 예 #2
1부터 5 사이의 소수는 [2,3,5] 3개가 존재하므로 3를 반환

## 답안
#### 나의 풀이
```javascript
function solution(n) {
  const answer = [];

  for(let i = 0; i <= n; i++) answer.push(i);

  for(let j = 2; j <= Math.sqrt(n); j++) { // 아래에서 배수는 제외되므로 제곱근까지만 확인하면 된다.
    if(!answer[j]) continue;
    for(let k = Math.pow(j, 2); k <= n; k += j) answer[k] = false; // 소수인 수의 배수는 모두 제외
  }

  return answer.filter(num => num !== false).length - 2; // 0, 1 제외하기 위해 -2
}
```
시간 초과가 계속 떠서 검색해보니 에라토스테네스의 체라는 수학적 원리를 이용해야 했다. 😇

#### 다른 사람 풀이
```javascript
function solution(n) {
  const s = new Set();
  for (let i = 1; i <= n; i += 2) {
    s.add(i);
  }
  s.delete(1);
  s.add(2);
  for (let j = 3; j < Math.sqrt(n); j++) {
    if (s.has(j)) {
      for (let k = j * 2; k <= n; k += j) {
        s.delete(k);
      }
    }
  }
  return s.size;
}
```
* set사용 (그러나 효율성은 더 느리다. has메서드도 loop이기 때문에 O(N<sup>3</sup>)이라 그렇지 않을까 추측해본다.)