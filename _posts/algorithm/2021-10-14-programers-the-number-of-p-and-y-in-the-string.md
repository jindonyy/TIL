---
title: "<span>프로그래머스</span><span>Lv1</span> 문자열 내 p와 y의 개수"
header:
  teaser: /assets/images/algorithm/programmers_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2021-10-14
---

## 문제 설명
대문자와 소문자가 섞여있는 문자열 s가 주어집니다. s에 'p'의 개수와 'y'의 개수를 비교해 같으면 True, 다르면 False를 return 하는 solution를 완성하세요. 'p', 'y' 모두 하나도 없는 경우는 항상 True를 리턴합니다. 단, 개수를 비교할 때 대문자와 소문자는 구별하지 않습니다.

예를 들어 s가 "pPoooyY"면 true를 return하고 "Pyy"라면 false를 return합니다.

### 제한사항
* 문자열 s의 길이 : 50 이하의 자연수
* 문자열 s는 알파벳으로만 이루어져 있습니다.

### 입출력 예

|s|answer|
|-|-|
|"pPoooyY"|true|
|"Pyy"|false|

### 입출력 예 설명
#### 입출력 예 #1
'p'의 개수 2개, 'y'의 개수 2개로 같으므로 true를 return 합니다.

#### 입출력 예 #2
'p'의 개수 1개, 'y'의 개수 2개로 다르므로 false를 return 합니다.

## 답안
#### 나의 풀이
```javascript
function solution(s){
  s = s.toUpperCase();
  var strNum = [0, 0];
  
  for(var i = 0; i < s.length; i++) {
    if(s[i] == "P") strNum[0]++;
    if(s[i] == "Y") strNum[1]++;
  }
  
  return strNum[0] == strNum[1] ? true : false;
}
```

#### 옛날 풀이
```javascript
function solution(s){
  var answer = false;

  s = s.toLowerCase();
  
  var length_p = 0,
    length_y = 0;

  for(var i = 0; i < s.length; i++){
    if(s[i] === "p"){
      length_p++;
    } else if(s[i] === "y"){
      length_y++;
    }
  }

  if(length_p !== 0 && length_p === length_y){
    answer = true;
  }

  return answer;
}
```

#### 다른사람 풀이
```javascript
function numPY(s){
  return s.toUpperCase().split("P").length === s.toUpperCase().split("Y").length;
}
```
좋았던 점
1. split 사용
2. ? true : false를 안해도 비교식에서는 항상 boolean값이 나온다.

```javascript
function numPY(s) {
  return s.match(/p/ig).length == s.match(/y/ig).length;
}
```
좋았던 점
1. 정규식 사용