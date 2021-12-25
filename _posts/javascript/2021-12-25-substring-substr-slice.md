---
title: "부분 문자열 가져오기(substring, substr, slice)"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [js this method, substring, substr, slice]
date: 2021-12-25
---

## substring 
  * 문법: str.substring(start[, end])  
  * 문자열의 start부터 end 전까지 문자열의 부분 문자열을 반환하는 메서드이다.

## substr 
  * 문법: str.substr(start[, length])  
  * 문자열에서 start에서 시작하여 length 갯수 만큼의 문자들을 반환한다.

## slice  
  * 문법: str.slice(start[, end])  
  * 문자열의 start부터 end 전까지 문자열의 부분  새로운 문자열을 반환한다.

```javascript
const str = "abcdefghi";

str.substring(1, 3); // "bc"
str.substr(1, 3); // "bcd"
str.slice(1, 3) // "bc"

str.substring(3); // "defghi" (end가 생략될 경우, 끝까지 반환)
str.substr(3); // "defghi" (length가 생략될 경우, 끝까지 반환)
str.slice(3); // "defghi" (end가 생략될 경우, 끝까지 반환)

str.substring(-4); // "fghi" (음수를 입력할 경우, 뒤에서부터 음수의 절대값만큼 거꾸로 계산하여 반환)
str.subslice(-4); // "fghi" (음수를 입력할 경우, 뒤에서부터 음수의 절대값만큼 거꾸로 계산하여 반환)
```

## ⭐️ substring과 slice의 차이점
#### start가 end보다 클 경우
* substring은 start 값과 end 값을 바꾸어서 처리한다.
* slice는 빈문자열을 반환한다.

```javascript
const str = "abcdefghi";

str.substring(3, 1); // "bc" (substring(1, 3))
str.slice(3, 1) // ""
```

#### start 또는 end가 음수일 경우  
* substring은 음수는 0으로 계산한다.  
* slice는 string의 가장 뒤에서 음수의 절대값만큼 거꾸로 계산하여 반환한다.

```javascript
const str = "abcdefghi";

str.substring(-4); // "abcdefghi" (str.substring(0))
str.substring(-4, -2); // "" (str.substring(0, 0))
str.substring(0, -2); // "" (str.substring(0, 0))
str.substring(-4); // "abcdefghi" (str.substring(0))

str.slice(-4); // "fg"
str.slice(-4, -2); // "fghi"
str.slice(0, -2); // "abcdefg"
```