---
title: "<span>프로그래머스</span><span>Lv1</span> 완주하지 못한 선수"
header:
  teaser: /assets/images/algorithm/programmers_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2021-10-22
---

## 문제 설명
수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.  
마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

### 제한 사항
* 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
* completion의 길이는 participant의 길이보다 1 작습니다.
* 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
* 참가자 중에는 동명이인이 있을 수 있습니다.

### 입출력 예

|participant|completion|return|
|-|-|-|
|["leo", "kiki", "eden"]|["eden", "kiki"]|"leo"|
|["marina", "josipa", "nikola", "vinko", "filipa"]|["josipa", "filipa", "marina", "nikola"]|"vinko"|
|["mislav", "stanko", "mislav", "ana"]|["stanko", "ana", "mislav"]|"mislav"|

## 답안
#### 나의 풀이
```javascript
function solution(participant, completion) {
  participant.sort();
  completion.sort();
    
  for(var i = 0; participant.length; i++) {
    if(participant[i] != completion[i]) return participant[i];
  }
}
```
옛날에 푼 것과 같다..

#### 옛날 풀이
```javascript
function solution(participant, completion) {
  participant.sort();
  completion.sort();

  for(var i = 0; i < participant.length; i++){
    if(completion[i] !== participant[i]){
      return participant[i]
    }
  }
}
```

#### 다른 사람 풀이
```javascript
function solution(participant, completion) {
  participant.sort();
  completion.sort();

  for(let i in participant) {
    if(participant[i] !== completion[i]) return participant[i];
  }
}
```
for...in을 쓸 수 있다.  
그러나 일반 for문을 사용하는 것이 더 적합하다고 한다. for (let i = 0; i < arr.length; i++)  
가장 베스트는 for (let i = 0, len = arr.length; i < len; i++) 이다. 반복문을 돌 때마다 length를 계산하므로 초기문에서 변수에 저장해놓는 것이 가장 좋다.

