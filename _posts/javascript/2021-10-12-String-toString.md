---
title: "숫자를 문자열로 변환하기(String, toString)"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [js string, string, String, toString]
date: 2021-10-12
---

1과 "1"은 다르다.  
배열에 있는 숫자들을 이어적어야하는 상황이 생긴다면 어떻게 해야할까?  
이럴 때 Number인 1을 String인 "1"로 바꿔줘야 한다.  
그럼 Number를 String으로 바꾸어주는 메소드를 알아보도록 하자.

## String  
* type이 Number인 숫자를 문자열로 변환시켜 반환해주는 함수이다.
* 문법: String(value)  
* ``value + ""`` 의 동작을 해주는 함수이므로 undefined나 null을 입력해도 문자로 바꿔준다.

```javascript
String(12.34); // '12.34'
String(12.34 + 'abc'); // '12.34abc'
String('abc' + 12.34); // 'abc12.34'
String(undefined); // 'undefined'
String(null); // 'null'
```

## toString  
* type이 Number인 숫자를 문자열로 변환시켜 반환해주는 메서드이다.
* 문법: (value).toString([radix]) 
* undefined나 null과 같이 값이 없을 경우 Error가 뜬다.
* radix: value를 다른 진수로 바꾸어 문자로 바꾸고싶을 때 사용한다. 2 ~ 36진수까지를 정의할 수 있고, 따로 radix를 지정하지 않을 경우 value 그대로 문자로 변환한다. 범위를 벗어난 진수를 지정할 경우 Error가 뜬다.

```javascript
(12.34).toString(); // '12.34'
(12.34).toString(5); // '22.1322222222222222222222'
(12.34 + 'abc').toString(); // '12.34abc'
('abc' + 12.34).toString(); // 'abc12.34'
(undefined).toString(); // Error
(null).toString(); // Error
```

## 덧셈 이용하기
숫자 + 숫자 = 숫자  
문자열 + 문자열 = 문자열  
그렇다면 숫자 + 문자열은? 문자열이다.  
이를 이용해서 메서드를 쓰지 않고, 숫자에 **빈문자열**을 더해서 숫자를 문자열로 바꿀 수 있다.

```javascript
12.34 + ""; // '12.34'
```