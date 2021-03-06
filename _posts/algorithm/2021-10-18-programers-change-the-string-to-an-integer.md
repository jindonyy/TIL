---
title: "<span>프로그래머스</span><span>Lv1</span> 문자열을 정수로 바꾸기"
header:
  teaser: /assets/images/algorithm/programmers_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2021-10-18
---

## 문제 설명
문자열 s를 숫자로 변환한 결과를 반환하는 함수, solution을 완성하세요.

### 제한 조건
* s의 길이는 1 이상 5이하입니다.
* s의 맨앞에는 부호(+, -)가 올 수 있습니다.
* s는 부호와 숫자로만 이루어져있습니다.
* s는 "0"으로 시작하지 않습니다.

### 입출력 예
예를들어 str이 "1234"이면 1234를 반환하고, "-1234"이면 -1234를 반환하면 됩니다.
str은 부호(+,-)와 숫자로만 구성되어 있고, 잘못된 값이 입력되는 경우는 없습니다.

## 답안
#### 나의 풀이
```javascript
function solution(s) {
  return Number(s);
}
```
아래 풀이보다 더 효율성과 가독성이 좋다.
```javascript
function solution(s) {
  return s*1;
}
```
간단하게 쓸 수 있으나 repeat은 IE에서 작동되지 않는다.

#### 옛날 풀이
```javascript
function solution(s) {
  var answer = 0;

  answer = parseInt(s);

  return answer;
}
```

#### 다른 사람 풀이
```javascript
function solution(s) {
  return +s;
}
```