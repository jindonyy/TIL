---
title: "<span>프로그래머스</span><span>Lv1</span> 문자열 다루기 기본"
header:
  teaser: /assets/images/algorithm/programmers_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2021-10-16
---

## 문제 설명
문자열 s의 길이가 4 혹은 6이고, 숫자로만 구성돼있는지 확인해주는 함수, solution을 완성하세요.  
예를 들어 s가 "a234"이면 False를 리턴하고 "1234"라면 True를 리턴하면 됩니다.

### 제한 사항
* s는 길이 1 이상, 길이 8 이하인 문자열입니다.

### 입출력 예

|s|return|
|-|-|
|"a234"|false|
|"1234"|true|

## 답안
#### 나의 풀이
```javascript
function solution(s) {
  if(s.length != 4 && s.length != 6) return false;
  return s == parseInt(s) ? true : false;
}
```
parseFloat이나 Number은 문자열 s가 "12.3"인 경우 length는 4이나 문자열이므로 "."은 문자이다.  
문제에서 숫자로만 구성되있는지 확인하라고 하였으므로 실수는 해당 될 수 없다. (테스트 11이 실수인 듯 하다.)
```javascript
function solution(s) {
  return s.length == 4 || s.length == 6 ? (s == parseInt(s) ? true : false) : false);
}
```
이중삼항연산자로 풀어봤지만 가독성과 효율성이 위의 풀이보다 떨어진다.

#### 옛날 풀이
```javascript
function solution(s) {
  var answer = false;

  if(s.length === 4 || s.length === 6){
    answer = true;

    var str = s.split("");
    str.forEach(element => {
      if(isNaN(Number(element))){
        answer = false;
      }
    });
  }
  return answer;
}
```

#### 다른 사람 풀이
```javascript
function alpha_string46(s){
  var regex = /^\d{6}$|^\d{4}$/;
  return regex.test(s);
}
```
정규식 사용