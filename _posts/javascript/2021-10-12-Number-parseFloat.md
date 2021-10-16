---
title: "문자열을 숫자로 변환하기(Number, parseFloat)"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [js number, number, Number, parseFloat]
date: 2021-10-12
---

1과 "1"은 다르다.  
prompt를 통해 입력 받은 숫자로 계산을 해야한다면 어떻게 해야할까? (prompt로 입력 받은 값은 항상 문자열이다.)  
이럴 때 String인 "1"을 Number인 1로 바꿔줘야 한다.  
그럼 String을 Number로 바꾸어주는 메소드를 알아보도록 하자.

## Number  
* 문자열(string)인 숫자를 type이 number인 숫자로 변환시켜 반환해주는 함수이다.
* 문법: Number(string)  
* <u>문자열에 문자가 들어있을 경우, NaN을 반환한다.</u>
* <u>빈문자열인 경우나 공백만 있을 경우, 0을 반환한다.</u>
* 숫자 앞 뒤에 공백이 있을 경우, 공백을 제거한 뒤 숫자로 반환한다.
* <u>숫자들 사이에 공백이 있는 경우, 문자열로 인식해 NaN을 반환한다.</u>
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
* 문자열(string)인 숫자를 type이 number인 숫자로 변환시켜 반환해주는 함수이다.
* 문법: parseFloat(string)  
* Number함수와 같아보이지만 문자열이 들어갔을 경우 반환 값이 다르다.
* <u>문자열에 문자가 들어있을 경우 중에서 숫자가 먼저 나오는 경우에는 문자열이 나오기 전의 숫자를 반환한다. 문자가 먼저 나오는 경우에는 NaN을 반환한다.</u>
* <u>빈문자열인 경우나 공백만 있을 경우, NaN을 반환한다.</u>
* 숫자 앞 뒤에 공백이 있을 경우, 공백을 제거한 뒤 숫자로 반환한다.
* <u>숫자들 사이에 공백이 있는 경우, 공백 앞에 있는 숫자까지 반환한다.</u>
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
숫자 * 숫자 = 숫자  
문자열 * 문자열 = 숫자  
그렇다면 숫자 * 문자열은? 숫자이다.  
문자열에서는 곱셈을 할 일이 없기 때문에 곱셈을 할 경우, 자동으로 숫자로 바꾸어 주는 것이다. (역시 똑똑한 컴퓨터 b)  
그러나 Number메서드와 같이 문자가 들어있는 문자열은 NaN으로 처리되 계산 되지 않는다.
이를 이용해서 메서드를 쓰지 않고, 문자열에 **1**을 곱해서 문자열을 숫자로 바꿀 수 있다.

```javascript
"12.34" * 1; // 12.34
```