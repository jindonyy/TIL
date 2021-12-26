---
title: "<span>프로그래머스</span><span>Lv1</span> 가운데 글자 가져오기"
header:
  teaser: /assets/images/algorithm/programmers_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2021-12-17
---

### 문제 설명
단어 s의 가운데 글자를 반환하는 함수, solution을 만들어 보세요. 단어의 길이가 짝수라면 가운데 두글자를 반환하면 됩니다.

### 제한 조건
* s는 길이가 1 이상, 100이하인 스트링입니다.

### 입출력 예
|s|return|
|-|-|
|"abcde"|"c"|
|"qwer"|"we"|

## 답안
#### 나의 풀이
```javascript
function solution(s) {
  var length = s.length;
  return (length % 2 == 0) ? s.substr(length/2-1, 2) : s.substr(length/2, 1);
}
```

#### 옛날 풀이
```javascript
function solution(s) {
  if(s.length % 2){ //홀수
    return s.substr(s.length/2, 1);
  } else{ //짝수
    return s.substr(s.length/2-1, 2);
  }
}
```

#### 다른 사람 풀이
```javascript
function solution(s) {
  return s.substr(Math.ceil(s.length / 2) - 1, s.length % 2 === 0 ? 2 : 1);
}
```

```javascript
function solution(s) {
  const mid = Math.floor(s.length/2);
  return s.length %2 === 1 ? s[mid] : s[mid-1]+s[mid];
}
```