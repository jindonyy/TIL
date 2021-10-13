---
title: "올림, 내림, 반올림, 버림, 정수화"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [javascript, number, ceil, floor, round, parseInt]
date: 2021-10-12
---

X원을 n명이서 나누어 계산하는 프로그램을 만든다고 생각해보자.  
x = 10000, n = 3 값이 입력됐을 때, 10000 / 3 = 3333.33333... 이다.  
소수점들은 송금을 할 수 없다. 소수점을 버려야하는 상황이 생긴 것이다.  
소수점들을 버리고 정수로 바꾸어주어야 할 때 올림할지 내림할지에 따라 사용하는 메서드들이 다르다.  
정수화시켜주는 메서드들을 알아보자.

## ceil
* x가 정수가 아닌 경우 **올림**하여 반환해주는 함수이다.
* 문법: Math.floor(x)
* x가 type이 string인 숫자의 경우 올림하여 type이 Number인 숫자로 반환하지만, 문자가 들어있을 경우엔 NaN을 반환한다.
* 빈문자열인 경우나 공백만 있을 경우, false로 인식하여 0을 반환한다.
* 숫자 앞 뒤에 공백이 있을 경우, 공백을 제거한 뒤 숫자로 반환한다.
* 숫자들 사이에 공백이 있는 경우, 문자열로 인식해 NaN을 반환한다.
* 즉, 숫자 사이에 공백만 문자로 인식한다.

```javascript
Math.ceil(3.95); //  4
Math.ceil(3.05); //  4
Math.ceil(4); //   4
Math.ceil(-3.05); // -3
Math.ceil(-3.95); // -3
Math.ceil('3.95E1'); // 40 
Math.ceil('3.95E-1'); // 1
Math.ceil('3.95abc'); // NaN
Math.ceil(''); // 0
Math.ceil(' '); // 0
Math.ceil(null); // 0
Math.ceil(undefined); // NaN
Math.ceil(  3.95  ); // 4
Math.ceil('  3.95  '); // 4
Math.ceil('  3.9 5  '); // NaN
```

## floor
* x가 정수가 아닌 경우 **내림**하여 반환해주는 함수이다.
* 문법: Math.floor(x)
* x가 type이 string인 숫자의 경우 내림하여 type이 Number인 숫자로 반환하지만, 문자가 들어있을 경우엔 NaN을 반환한다.
* 빈문자열인 경우나 공백만 있을 경우, false로 인식하여 0을 반환한다.
* 숫자 앞 뒤에 공백이 있을 경우, 공백을 제거한 뒤 숫자로 반환한다.
* 숫자들 사이에 공백이 있는 경우, 문자열로 인식해 NaN을 반환한다.
* 즉, 숫자 사이에 공백만 문자로 인식한다.

```javascript
Math.floor(3.05); //  3
Math.floor(3.95); //  3
Math.floor(4); //   4
Math.floor(-3.05); // -4
Math.floor(-3.95); // -4
Math.floor('3.95E1'); // 39 
Math.floor('3.95E-1'); // 0
Math.floor('3.95abc'); // NaN
Math.floor(''); // 0
Math.floor(' '); // 0
Math.floor(null); // 0
Math.floor(undefined); // NaN
Math.floor(  3.95  ); // 3
Math.floor('  3.95  '); // 3
Math.floor('  3.9 5  '); // NaN
```

## round
* x가 정수가 아닌 경우 **반올림**하여 반환해주는 함수이다.
* 문법: Math.round(x)
* x가 type이 string인 숫자의 경우 반올림하여 type이 Number인 숫자로 반환하지만, 문자가 들어있을 경우엔 NaN을 반환한다.
* 빈문자열인 경우나 공백만 있을 경우, false로 인식하여 0을 반환한다.
* 숫자 앞 뒤에 공백이 있을 경우, 공백을 제거한 뒤 숫자로 반환한다.
* 숫자들 사이에 공백이 있는 경우, 문자열로 인식해 NaN을 반환한다.
* 즉, 숫자 사이에 공백만 문자로 인식한다.

```javascript
Math.round(3.05); //  3
Math.round(3.95); //  4
Math.round(4); //   4
Math.round(-3.05); // -3
Math.round(-3.95); // -4
Math.round('3.95E1'); // 40 
Math.round('3.95E-1'); // 0
Math.round('3.95abc'); // NaN
Math.round(''); // 0
Math.round(' '); // 0
Math.round(null); // 0
Math.round(undefined); // NaN
Math.round(  3.95  ); // 4
Math.round('  3.95  '); // 4
Math.round('  3.9 5  '); // NaN
```

## parseInt    
* 문법: parseInt(x[, radix])  
* x를 정수가 아닌 경우 소수점 이하를 버려 반환해주는(**정수화**) 함수이다.  
* radix: 다른 진수의 숫자로 변환하고 싶을 때 사용한다. 2 ~ 36진수까지를 정의할 수 있고, 따로 radix가 0이거나 지정하지 않을 경우 10진수로 변환한다. 0을 제외한 범위를 벗어난 진수를 지정할 경우 NaN을 반환한다.
* <u>x에 문자가 들어있을 경우 중에서 숫자가 먼저 나오는 경우에는 문자열이 나오기 전의 숫자를 반환한다. 문자가 먼저 나오는 경우에는 NaN을 반환한다.</u>
* <u>빈문자열인 경우나 공백만 있을 경우, NaN을 반환한다.</u>
* 숫자 앞 뒤에 공백이 있을 경우, 공백을 제거한 뒤 숫자로 반환한다.
* <u>숫자들 사이에 공백이 있는 경우, 공백 앞에 있는 숫자까지 정수로 반환한다.</u>
* 즉, 숫자 사이에 공백만 문자로 인식한다.

```javascript
parseInt('12.34'); // 12
parseInt(12.34); // 12
parseInt('12.34', 5); // 7
parseInt('12.34E2'); // 12 
parseInt('12.34E-2'); // 12
parseInt('12.34abc'); // 12
parseInt('abc12.34'); // NaN
parseInt(''); // NaN
parseInt(' '); // NaN
parseInt('  12.34  '); // 12.34
parseInt('  12.3 4  '); // 12
```

## 활용
소수점을 n번째 자리까지만 계산하거나 10n자리까지만 계산해야하는 경우도 생긴다.  

### 소수점 n자리까지
실수 x의 소수점 n번째 자리까지 정수화 시켜야할 경우, x에 **10의 n제곱**을 곱한다. 그 다음 정수화 메서드를 사용하여 n+1자리 뒤의 소수점을 버려준 뒤, 다시 10의 n제곱을 나누어준다.

* 소수점 첫째자리만 반올림하기

```javascript
var x = 12.345;
var y = 10
Math.round(x*y) / y; // 12.3
```

### n의 자리까지
정수 x의 n의 자리까지 남겨두고 올리거나 내리는 등을 해야할 경우, x에 **10 * n**을 나누어준다. 그 다음 정수화 메서드를 사용하여 n의 자리부터 뒤의 숫자까지 버려준 뒤, 다시 10 * n을 곱해준다.
* 10의 자리부터 내리기

```javascript
var x = 123.45;
var y = 100;
Math.floor(x/y) * y; // 100
```