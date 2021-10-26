---
title: "조건에 맞는 배열의 요소 찾기(find(IE❌), filter)"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [js array, array, find, filter]
date: 2021-10-26
---

## find
* callback의 조건에 맞는 **최초의 요소**를 찾으면 <u>해당 요소</u>를, 찾지 못하면 undefined를 반환하고 즉시 종료된다.
* 문법: array.find(callback(element[, index[, array]])[, thisArg])
  * callback: array에서 찾고싶은 요소를 가지고 있는 함수이다.
  * element: 배열에서 처리중인 현재 요소이다.
  * index: 배열에서 처리중인 현재 요소의 인덱스이다.
  * array: find 함수가 호출된 배열이다.
  * thisArg: callback을 실행할 때 this로 사용할 객체이다.
* **IE에서 작동하지 않는다.**

```javascript
var arr = [1, 5, 6, 3, 4];

arr.find((num, index, arr) => console.log(num, index, arr));
// 1 0 [1, 5, 6, 3, 4]
// 5 1 [1, 5, 6, 3, 4]
// 6 2 [1, 5, 6, 3, 4]
// 3 3 [1, 5, 6, 3, 4]
// 4 4 [1, 5, 6, 3, 4]

var find1 = arr.find(el => el % 2 === 0);
var find2 = arr.find(el => el < 0);
console.log(find1); // 6
console.log(find2); // undefined

var objArr = [{alphabet: "a", index: 1},{alphabet: "b", index: 2}, {alphabet: "c", index: 3}];
var find3 = objArr.find(el=> el.index === 2);
console.log(find3) // {alphabet: "b", index: 2}
```

## filter
* callback의 조건에 맞는 **모든 요소**를 찾아 <u>새로운 배열</u>로 반환한다. 조건에 맞는 요소가 없을 경우 빈 배열을 반환한다.
* 문법: array.filter(callback(element[, index[, array]])[, thisArg])
  * callback: array에서 찾고 싶은 요소의 조건을 가진 함수이다. true를 반환하면 요소를 유지하고, false를 반환하면 버린다.
  * element: 배열에서 처리중인 현재 요소이다.
  * index: 배열에서 처리중인 현재 요소의 인덱스이다.
  * array: filter 함수가 호출된 배열이다.
  * thisArg: callback을 실행할 때 this로 사용할 객체이다. 

```javascript
var arr1 = [1, 5, 6, 3, 4];

arr1.filter((num, index, arr1) => console.log(num, index, arr1));
// 1 0 [1, 5, 6, 3, 4]
// 5 1 [1, 5, 6, 3, 4]
// 6 2 [1, 5, 6, 3, 4]
// 3 3 [1, 5, 6, 3, 4]
// 4 4 [1, 5, 6, 3, 4]

var filter1 = arr1.filter(function(el) {
  return el % 2 === 0;
});
var filter2 = arr1.filter(function(el) {
  return el < 0;
});
console.log(filter1); // [6, 4]
console.log(filter2); // []
```
  
ES2015(화살표 함수) 사용
```javascript
var filter1 = arr1.filter(el => el % 2 === 0);
var filter2 = arr1.filter(el => el < 0);
console.log(filter1); // [6, 4]
console.log(filter2); // []
```