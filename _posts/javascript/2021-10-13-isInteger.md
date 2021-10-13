---
title: "정수인지 판별하기"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [javascript, integer, isInteger]
date: 2021-10-13
---

<a href="https://jindonyy.github.io/TIL/javascript/ceil-floor-round-parseInt/">앞의 글</a>에서 정수로 바꿔주는 메서드인 parseInt를 통해 정수인지 아닌지 판별을 해왔었다.  
그러다 어느 날 알고리즘 풀이를 보던 중 발견한 새로운 메서드!  
바로 정수를 판별해주는 기능의 메서드가 따로 있었던 것이였다.  
이렇게 편리한 메서드가 있었다니! 그러나 자주 보지 못했던 이유가 있었다..  
한번 보도록 하자.

## isInteger
* 문법: Number.isInteger(value)
* value가 정수인지 아닌지 판별하여 boolean값으로 반환한다.
* value가 NaN이나 Infinity인 경우 false를 반환한다.
* **IE에선 작동하지 않는다.** (한국에선 아직 사용하기 이른것인가..)
```javascript
  // parseInt를 사용한 방식
  1234 == parseInt(1234) // true
  12.34 == parseInt(12.34) // false

  Number.isInteger(1234); // true
  Number.isInteger(12.34); // false
  Number.isInteger(-10); // true
  Number.isInteger(9999999999); // true
  Number.isInteger(NaN); // false
  Number.isInteger(Infinity); // false
  Number.isInteger('ab'); // false
  Number.isInteger(true); // false
```