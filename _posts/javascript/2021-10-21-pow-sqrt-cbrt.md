---
title: "제곱, 제곱근, 세제곱근 구하기(pow, sprt, cbrt)"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [js number, number, pow, sqrt, cbrt]
date: 2021-10-21
---

##### 제곱(ⁿ)이란?  
- 자신을 곱한 수를 말한다. 자신을 몇번 곱했냐에 따라 몇제곱으로 부른다. 제곱, 세제곱, 네제곱 등등..  
- ex) 2의 제곱은 2 * 2 = 2² = 4이다.  
  
##### 제곱근(√)이란?  
- 제곱해서 x가 되는 수를 x의 제곱근이라고 한다. 이때 제곱근은 양의 제곱과 음의 제곱 두가지가 있다. (0의 제곱근은 0이다. 0은 부호가 없으므로 제곱근이 하나이다.) 이 중 양의 제곱근을 우리는 루트(√)라고 한다.  
- ex) 4의 제곱근은 ±2 이다. √4 = 2 이다.

## Math.pow
* 문법: Math.pow(x, y)
* x의 y 제곱을 반환해주는 메서드이다.
* x가 0인 경우에는 0 * 0은 무한대이므로 Infinity를 반환한다.
* y가 0인 경우에는 x의 값과 상관없이 1을 반환한다.
* x가 음수이면서 y가 정수가 아닌 경우에는 음수는 제곱근이 없으므로 NaN을 반환한다.
  
```javascript
Math.pow(2, 3) // 8
Math.pow(4, 0.5) // 2 (4의 제곱근)
Math.pow(8, 1/3) // 2 (8의 세제곱근)
Math.pow(-0.5, 3) // -0.125
Math.pow(0, 3) // Infinity
Math.pow(-7, 0) // 1
Math.pow(-7, 0.5) // NaN
```

## Math.sqrt
* 문법: Math.sqrt(x)
* x의 제곱근을 반환해주는 메서드이다.
* √x 로 계산하므로 음의 제곱근은 반환되지 않으며 x 또한 음수가 될 수 없다. 음수일 경우 NaN을 반환한다.
  
```javascript
Math.sqrt(9); // 3
Math.sqrt(2); // 1.414213562373095
Math.sqrt(1/4); // 0.5 (1/2)
Math.sqrt(0.5); // 0.7071067811865476
Math.sqrt(1);  // 1
Math.sqrt(0);  // 0
Math.sqrt(-1); // NaN
```

## Math.cbrt
* 문법: Math.cbrt(x)
* x의 세제곱근을 반환해주는 메서드이다.
* **IE에서 작동하지 않는다.** 자주 쓸 일도 없고 IE에서도 안되므로 있구나 정도로만 알면 된다.
  
```javascript
Math.cbrt(27); // 3
Math.cbrt(-27); // -3
Math.cbrt(NaN); // NaN
Math.cbrt(-1); // -1
Math.cbrt(-0); // -0
Math.cbrt(0); // 0
Math.cbrt(-Infinity); // -Infinity
Math.cbrt(null); // 0 (null = 0으로 치환)
Math.cbrt(2);  // 1.2599210498948734
```