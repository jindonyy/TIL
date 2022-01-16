---
title: "<span>프로그래머스</span><span>Lv1</span> 이상한 문자 만들기"
header:
  teaser: /assets/images/algorithm/programmers_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programmers, Level1]
date: 2022-01-16
---

## 문제 설명
문자열 s는 한 개 이상의 단어로 구성되어 있습니다. 각 단어는 하나 이상의 공백문자로 구분되어 있습니다. 각 단어의 짝수번째 알파벳은 대문자로, 홀수번째 알파벳은 소문자로 바꾼 문자열을 리턴하는 함수, solution을 완성하세요.

### 제한 조건
* 문자열 전체의 짝/홀수 인덱스가 아니라, 단어(공백을 기준)별로 짝/홀수 인덱스를 판단해야합니다.
* 첫 번째 글자는 0번째 인덱스로 보아 짝수번째 알파벳으로 처리해야 합니다.

### 입출력 예
|s|return|
|-|-|
|"try hello world"|"TrY HeLlO WoRlD"|

### 입출력 예 설명
"try hello world"는 세 단어 "try", "hello", "world"로 구성되어 있습니다. 각 단어의 짝수번째 문자를 대문자로, 홀수번째 문자를 소문자로 바꾸면 "TrY", "HeLlO", "WoRlD"입니다. 따라서 "TrY HeLlO WoRlD" 를 리턴합니다.

## 답안
#### 나의 풀이
```javascript
function solution(s) {
  let answer = "";
  let even = true;

  for(const one of s) {
    if(even) {
      answer += one.toUpperCase();
      even = false;
      if(one ===  " ") even = true;
    } else {
      answer += one.toLowerCase();
      even = true;
    }
  }

  return answer;
}
```

### 옛날 풀이
```javascript
function solution(s) {
  var str = s.split("");
  var even = true;

  for(var i = 0; i < str.length; i++) {
    if(str[i] !== " ") {
      if(even) {
        str[i] = str[i].toUpperCase();
        even = false;
      } else {
        str[i] = str[i].toLowerCase();
        even = true;
      }
    } else {
      even = true;
    }
  }

  return str.join("");
}
```

### 다른 사람 풀이
```javascript
function toWeirdCase(s){
  return s.toUpperCase().replace(/(\w)(\w)/g, function(a){return a[0].toUpperCase()+a[1].toLowerCase();})
}
```
정규식을 사용했으나..