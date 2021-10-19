---
title: "아스키코드 변환하기(charCodeAt, fromCharCode)"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [js string, string, charCodeAt, fromCharCode]
date: 2021-10-20
---

아스키코드란?  
-미국정보교환표준부호(영어: American Standard Code for Information Interchange), 또는 줄여서 ASCII( /ˈæski/, 아스키)는 영문 알파벳을 사용하는 대표적인 문자 인코딩이다.
<img src="/assets/images/2021-10-20-post-img1.png" style="margin-top: 10px;" title="아스키코드 표" alt="아스키코드 표"/> 

## charCodeAt
* 문자열 중 지정한 인덱스의 문자를 아스키코드 번호로 반환해주는 메서드이다.
* 문법: str.charCodeAt(index)
* index
  * 문자열 중 바꾸고 싶은 문자의 index
  * 0 이상이고 문자열의 길이보다 작은 정수이여야 한다. 음수이거나 문자열의 길이보다 클 경우 NaN을, 정수가 아닐 경우 parseInt하여 계산된다.
  * 생략하거나 숫자가 아니라면 0을 기본값으로 사용한다.
  
```javascript
var str = "a A";
str.charCodeAt(0); // 97
str.charCodeAt(1); // 32
str.charCodeAt(2); // 65
str.charCodeAt(-1); // NaN
str.charCodeAt(100); // NaN
str.charCodeAt(1.9); // 32
str.charCodeAt(); // 97
```

## fromCharCode
* 아스키코드 번호를 받아 문자열을 구성하여 반환해주는 메서드이다.
* 문법: String.fromCharCode(num1[, ...[, numN]])
* num1 ...
  * 문자열로 바꾸고자 하는 아스키코드 번호
  * 가능한 값의 범위는 0부터 65535(0xFFFF)까지이다.
  * 여러 개를 입력할 경우 문자열로 반환해준다.
  
```javascript
String.fromCharCode(122); // 'z'
String.fromCharCode(88, 89, 90); // 'XYZ'
```