---
title: "문자열을 숫자로 변환하기"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [javascript, convert to a number, Number, parseFloat]
date: 2021-10-12
---

## Number  
* 문법: Number(string)  
* 문자열(string)인 숫자를 type이 number인 숫자로 변환시켜 반환해주는 함수이다.
* *문자열에 문자가 들어있을 경우, NaN을 반환한다.*
* *빈문자열인 경우나 공백만 있을 경우, 0을 반환한다.*
* 숫자 앞 뒤에 공백이 있을 경우, 공백을 제거한 뒤 숫자로 반환한다.
* *숫자들 사이에 공백이 있는 경우, 문자열로 인식해 NaN을 반환한다.*
* 즉, 숫자 사이에 공백만 문자로 인식한다.

```javascript
  Number('12.34'); // 12.34
  Number(12.34); // 12.34
  Number('12.34E2'); // 1234
  Number('12.34E-2'); // 0.1234
  Number('12.34abc'); // NaN
  Number('abc12.34'); // NaN
  Number(''); // 0
  Number(' '); // 0
  Number('  12.34  '); // 12.34
  Number('  12. 34'  ); // NaN
```

## parseFloat     
* 문법: parseFloat(string)  
* 문자열(string)인 숫자를 type이 number인 숫자로 변환시켜 반환해주는 함수이다. Number함수와 같아보이지만 문자열이 들어갔을 경우 반환 값이 다르다.
* *문자열에 문자가 들어있을 경우 중에서 숫자가 먼저 나오는 경우에는 문자열이 나오기 전의 숫자를 반환한다. 문자가 먼저 나오는 경우에는 NaN을 반환한다.*
* *빈문자열인 경우나 공백만 있을 경우, NaN을 반환한다.*
* 숫자 앞 뒤에 공백이 있을 경우, 공백을 제거한 뒤 숫자로 반환한다.
* *숫자들 사이에 공백이 있는 경우, 공백 앞에 있는 숫자까지 반환한다.*
* 즉, 숫자 사이에 공백만 문자로 인식한다.

```javascript
  parseFloat('12.34'); // 12.34
  parseFloat(12.34); // 12.34
  parseFloat('12.34E2'); // 1234
  parseFloat('12.34E-2'); // 0.1234
  parseFloat('12.34abc'); // 12.34
  parseFloat('abc12.34'); // NaN
  parseFloat(''); // NaN
  parseFloat(' '); // NaN
  parseFloat('  12.34  '); // 12.34
  parseFloat('  12. 34  '); // 12
```

## 곱셈 이용하기
문자열 * 숫자는 숫자이다.

```javascript
  "12.34" * 1; // 12.34
```