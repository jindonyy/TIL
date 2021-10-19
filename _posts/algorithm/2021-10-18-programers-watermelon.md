---
title: "<span>프로그래머스</span><span>Lv1</span> 수박수박수박수박수박수?"
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2021-10-18
---

## 문제 설명
길이가 n이고, "수박수박수박수...."와 같은 패턴을 유지하는 문자열을 리턴하는 함수, solution을 완성하세요. 예를들어 n이 4이면 "수박수박"을 리턴하고 3이라면 "수박수"를 리턴하면 됩니다.

### 제한 사항
* n은 길이 10,000이하인 자연수입니다.

### 입출력 예

|n|return|
|-|-|
|3|"수박수"|
|4|"수박수박"|

## 답안
#### 나의 풀이
```javascript
function solution(n) {    
  var answer = "수박".repeat(n/2);
  return n % 2 ? answer + "수" : answer;
}
```
간단하게 쓸 수 있으나 repeat은 IE에서 작동되지 않는다.
```javascript
function solution(n) {
  var answer = "";
  for(var i = 1; i <= n; i++) {
    i % 2 ? answer += "수" : answer += "박";
  }
  return answer;
}
```
IE에서 사용할 때 코드. for문 사용.
효율성은 repeat보다 조금 떨어진다.

#### 옛날 풀이
```javascript
function solution(n) {
  var answer = '수박';
  
  answer = answer.repeat(n/2);
  
  if(n%2 == 1){ //홀수
    answer += "수";
  }
  
  return answer;
}
```

#### 다른 사람 풀이
```javascript
function waterMelon(n){
  return ("수박").repeat(n/2) + ((n%2) ? '수' : '');
}
```
나의 풀이 1번을 한줄로 바꿀 수 있다.