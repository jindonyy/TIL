---
title: "<span>프로그래머스</span><span>Lv1</span> 문자열 내림차순으로 배치하기"
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2021-10-16
---

## 문제 설명
문자열 s에 나타나는 문자를 큰것부터 작은 순으로 정렬해 새로운 문자열을 리턴하는 함수, solution을 완성해주세요.  
s는 영문 대소문자로만 구성되어 있으며, 대문자는 소문자보다 작은 것으로 간주합니다.

### 제한 사항
* str은 길이 1 이상인 문자열입니다.

### 입출력 예

|s|return|
|-|-|
|"Zbcdefg"|"gfedcbZ"|

## 답안
#### 나의 풀이
```javascript
function solution(s) {
	return s.split("").sort().reverse().join("");
}
```

#### 옛날 풀이
```javascript
function solution(s) {
  let arr = s.split("");
  arr.sort();
  arr.reverse();
  return arr.join("");
}
```