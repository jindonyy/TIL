---
title: "<span>프로그래머스</span><span>Lv1</span> 시저 암호
"
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2021-10-19
---

## 문제 설명
어떤 문장의 각 알파벳을 일정한 거리만큼 밀어서 다른 알파벳으로 바꾸는 암호화 방식을 시저 암호라고 합니다. 예를 들어 "AB"는 1만큼 밀면 "BC"가 되고, 3만큼 밀면 "DE"가 됩니다. "z"는 1만큼 밀면 "a"가 됩니다. 문자열 s와 거리 n을 입력받아 s를 n만큼 민 암호문을 만드는 함수, solution을 완성해 보세요.

### 제한 사항
* 공백은 아무리 밀어도 공백입니다.
* s는 알파벳 소문자, 대문자, 공백으로만 이루어져 있습니다.
* s의 길이는 8000이하입니다.
* n은 1 이상, 25이하인 자연수입니다.

### 입출력 예

|s|n|return|
|-|-|-|
|"AB"|1|"BC"|
|"z"|1|"a"|
|"a B z"|4|"e F d"|

## 답안
#### 나의 풀이
```javascript
function solution(s, n) {
  var answer = "";
  for(var i = 0; i < s.length; i++) {
    if (s[i] == " ") answer += " ";
    else {
      var code = s.charCodeAt(i) + n;
      if(code - n <= 90 && code > 90) code = code - 26;
      else if(code - n >= 97 && code > 122) code = code - 26;
      answer += String.fromCharCode(code);
    }
  }
  return answer;
}
```
charCode를 이용
code - n <= 90인 경우가 대문자, code - n >= 97인 경우가 소문자이다.
```javascript
function solution(s, n) {
  var answer = "";
  var upperArr = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'];
  var lowerArr = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'];
  
  for(var i = 0; i < s.length; i++) {
    if(s[i] == " ") answer += " ";
    else if(upperArr.indexOf(s[i]) != -1) {
    var add = upperArr.indexOf(s[i]) + n;
    if(add > 25) add -= 26;
    answer += upperArr[add];
    } else if(lowerArr.indexOf(s[i]) != -1) {
    var add = lowerArr.indexOf(s[i]) + n;
    if(add > 25) add -= 26;
    answer += lowerArr[add];
    }
  }
    
  return answer;
}
```
노가다로 해보니 효율성은 더 좋다..

#### 옛날 풀이
```javascript
function solution(s, n) {
  var answer = '';

  for(var i = 0; i < s.length; i++){
    var code = s.charCodeAt(i);
    if(code === 32)	code -= n; // 공백
    else if(code <= 90 && code + n > 90) code -= 26; // 대문자이면서 n만큼 민 값이 Z를 넘을 때
    else if(code >= 97 && code + n > 122) code -= 26; // 소문자이면서 n만큼 민 값이 z를 넘을 때
    code += n;
    answer += String.fromCharCode(code); 
  }

  return answer;
}
```

#### 다른 사람 풀이
```javascript
function solution(s, n) {
  var upper = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
  var lower = "abcdefghijklmnopqrstuvwxyz";
  var answer= '';

  for(var i =0; i <s.length; i++){
    var text = s[i];
    if(text == ' ') {
      answer += ' '; 
      continue;
    }
    var textArr = upper.includes(text) ? upper : lower;
    var index = textArr.indexOf(text)+n;
    if(index >= textArr.length) index -= textArr.length;
    answer += textArr[index];
  }
  return answer;
}
```
* 배열 쓰지않고 노가다  
* 효율성을 높이기 위해 변수에 많이 저장해서 사용하였다.  
* 그러나 incluedes는 IE에서 작동X

