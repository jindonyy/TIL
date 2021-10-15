---
title: "부분 문자열 위치 가져오기"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [js string, string, indexOf, lastIndexOf]
date: 2021-10-15
---

"abcdefghi"에서 "abc"의 위치는 어떻게 알 수 있을까?
오늘은 문자열에서 일부 문자의 위치를 알 수 있는 메서드에 대해 알아보도록 하자.

## indexOf
* 문자열에서 찾고자 하는 문자를 지정한 위치부터 탐색하여, 일치하는 **첫 번째 인덱스**를 반환한다.
* 문법: str.indexOf(searchValue[, fromIndex])
  * searchValue: 위치를 찾고자 하는 문자
  * fromIndex: 생략했거나 음수인 경우 0부터 탐색하며, str.length보다 크거나 같을 경우 -1을 반환한다.
* 일치하는 값이 없으면 -1을 반환한다.

```javascript
var str = "abcdabc";

str.indexOf('ab'); // 0
str.indexOf('ab', -1); // 0
str.indexOf('ab', 4); // 4
str.indexOf('ab', 5); // -1
str.indexOf('c', 1); // 2
str.indexOf('ac'); // -1
str.indexOf(''); // 0
```

## lastIndexOf
* 문자열에서 찾고자 하는 문자를 지정한 위치부터 **역순**으로 탐색하여, 일치하는 첫 번째 인덱스를 반환한다.
* 문법: str.lastIndexOf(searchValue[, fromIndex])
  * searchValue: 위치를 찾고자 하는 문자
  * fromIndex: 생략했거나 str.length보다 크거나 같을 경우 str.length-1 부터, 음수인 경우 0부터 탐색한다.
* 일치하는 값이 없으면 -1을 반환한다.

```javascript
var str = "abcdabc";

str.lastIndexOf('ab'); // 4
str.lastIndexOf('b', -1); // -1
str.lastIndexOf('ab', 4); // 4
str.lastIndexOf('ab', 5); // 4
str.lastIndexOf('c', 1); // -1
str.lastIndexOf('ac'); // -1
str.lastIndexOf(''); // 7
```