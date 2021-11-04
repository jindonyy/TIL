---
title: "배열의 요소 위치 가져오기(indexOf, lastIndexOf, findIndex)"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [js array, array, indexOf, lastIndexOf, findIndex]
date: 2021-10-24
---

## indexOf
* 문법: arr.indexOf(searchElement[, fromIndex])
* 배열에서 searchElement를 검색하여 첫 번째로 발견한 인덱스를 반환하고, 존재하지 않으면 -1을 반환한다.
* fromIndex를 지정하면 검색을 시작할 위치를 정할 수 있다. 음수일 경우 배열의 끝에서 음수의 절대값만큼 거꾸로 계산된다.

```javascript
var array = ["a", "b", "c", "c", "b", "a"];
array.indexOf("b"); // 1
array.indexOf("e"); // -1
array.indexOf("a", 2); // 5
array.indexOf("c", -2); // -1
array.indexOf("b", -7); // -1

// 요소의 모든 항목 찾기
var indices = [];
var array = ["a", "b", "a", "c", "a", "d"];
var element = "a";
var idx = array.indexOf(element);
while (idx != -1) {
  indices.push(idx);
  idx = array.indexOf(element, idx + 1);
}
console.log(indices); // [0, 2, 4]
```

## lastIndexOf
* 문법: arr.lastIndexOf(searchElement[, fromIndex])
* 배열의 끝에서 **역순으로** searchElement를 검색하여 첫 번째로 발견한 인덱스를 반환하고, 존재하지 않으면 -1을 반환한다.
* fromIndex를 지정하면 역으로 검색을 시작할 위치를 정할 수 있다. 음수일 경우 배열의 끝에서 음수의 절대값만큼 거꾸로 계산된다.

```javascript
var array = ["a", "b", "c", "c", "b", "a"];
array.lastIndexOf("b"); // 4
array.lastIndexOf("e"); // -1
array.lastIndexOf("a", 2); // 0
array.lastIndexOf("c", -2); // 3
array.lastIndexOf("b", -7); // -1

// 요소의 모든 항목 찾기
var indices = [];
var array = ["a", "b", "a", "c", "a", "d"];
var element = "a";
var idx = array.lastIndexOf(element);
while (idx != -1) {
  indices.push(idx);
  idx = (idx > 0 ? array.lastIndexOf(element, idx - 1) : -1);
}
console.log(indices); // [4, 2, 0]
```

## findIndex
* 문법: arr.findIndex(callback(element[, index[, array]])[, thisArg])
  * callback: 3개의 인수를 취하여 배열의 각 값에 대해 실행할 함수이다.
  * element: 배열에서 처리중인 현재 요소이다.
  * index: 배열에서 처리중인 현재 요소의 인덱스이다.
  * array: findIndex 함수가 호출된 배열이다.
  * thisArg: 콜백을 실행할 때 this로 사용할 객체이다. 
* callback의 조건에 맞는 최초의 요소를 찾으면 해당 요소의 위치를, 찾지 못하면 -1을 반환하고 즉시 종료된다.
* **IE에서 작동하지 않는다.**

```javascript
var arr = [1, 5, 6, 3, 4, 7];
var find1 = arr.findIndex((element) => element % 2 === 0);
var find2 = arr.findIndex((element) => element < 0);
console.log(find1); // 2 (6의 위치)
console.log(find2); // -1

var objArr = [{alphabet: "a", index: 1},{alphabet: "b", index: 2}, {alphabet: "c", index: 3}];
var find3 = objArr.findIndex((element)=> element.index === 2);
console.log(find3) // 1 ({alphabet: "b", index: 2}의 위치)
```
  
## []
* 문법: array[index] = element  
* 대괄호를 이용하여 배열의 index 위치에 element를 추가하거나 수정할 수 있다. 
 
```javascript
var arr = ["a", "b", "c"];
arr[5] = "f";
console.log(arr); // ["a", "b", "c", empty x 2, "f"]
console.log(arr[3]); // undefined
arr[3] = "d";
console.log(arr); // ["a", "b", "c", "d", empty, "f"]
console.log(arr[3]); // "d"
```