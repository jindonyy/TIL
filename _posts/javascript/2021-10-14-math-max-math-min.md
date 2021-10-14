---
title: "최댓값, 최솟값 구하기"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [javascript, Math, Math.max, Math.min]
date: 2021-10-14
---

사용자들이 입력한 값들 중에 최솟값과 최댓값을 구해야하는 상황이 생긴다.
for문을 돌려서 비교할 수도 있겠지만 간편하게 사용할 수 있는 함수(메서드)가 있다.

## Math.max
* 문법: Math.max([value1[, value2[, ...]]])
* 입력값으로 받은 0개 이상의 숫자 중 **가장 큰** 숫자를 반환해주는 함수이다.
* value: 입력받은 값들은 <a href="https://jindonyy.github.io/TIL/javascript/converting-a-string-to-a-number/#number">Number</a>함수처럼 type이 string인 숫자로 바꾸어 계산해주지만 문자가 포함된 문자열은 NaN으로 처리하여 NaN을 반환한다. value를 입력하지 않았을 때는 -Infinity를 반환한다.

```javascript
Math.max(1, 2, 3) // 3
Math.max(-1, -2, -3) // -1
Math.max("-1", "-2", -3) // -1
Math.max("-1a", "-2", -3) // NaN
Math.max() // -Infinity
```

## Math.min
* 문법: Math.min([value1[, value2[, ...]]])
* 입력값으로 받은 0개 이상의 숫자 중 **가장 작은** 숫자를 반환해주는 함수이다.
* value: 입력받은 값들은 <a href="https://jindonyy.github.io/TIL/javascript/converting-a-string-to-a-number/#number">Number</a>함수처럼 type이 string인 숫자로 바꾸어 계산해주지만 문자가 포함된 문자열은 NaN으로 처리하여 NaN을 반환한다. value를 입력하지 않았을 때는 Infinity를 반환한다.

```javascript
Math.min(1, 2, 3) // 1
Math.min(-1, -2, -3) // -3
Math.min("-1", "-2", -3) // -3
Math.min("-1a", "-2", -3) // NaN
Math.min() // Infinity
```

## 활용
max와 min의 인자값으로는 원시값만 들어갈 수 있다. 때문에 배열을 인자로 넣으면 숫자가 아니므로 NaN을 반환한다.
배열에서 최댓값과 최솟값을 구하기 위해서는 배열을 요소를 하나하나 넣어주어야한다.

```javascript
var arr = [1, 2, 3];
var min = Math.min(arr) // NaN
```

* reduce 사용하기
```javascript
var arr = [1, 2, 3];
var max = arr.reduce((a, b => Math.max(a, b))); // 3
```

* apply 사용하기
```javascript
var arr = [1, 2, 3];
var min = Math.min.apply(null, arr);
```

* ...(spread operator) 사용하기
```javascript
var arr = [1, 2, 3];
var max = Math.max(...arr);
```