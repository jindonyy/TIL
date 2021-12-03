---
title: "배열의 요소 삭제(pop, shift, splice)"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [js delete element, pop, shift, splice]
date: 2021-12-03
---

## pop 
* 문법: array.pop()  
* 원본 배열의 **맨 끝**에 요소를 삭제하는 메서드이다.
* 삭제된 요소를 반환한다. 빈 배열에 pop을 호출하면 undefined를 반환한다. 

```javascript
const arr = ["a", "b", "c", "d", "e"];
arr.pop(); // "e"
console.log(arr); // ["a", "b", "c", "d"]
```

## shift
* 문법: array.shift()  
* 원본 배열의 **맨 앞**에 요소를 삭제하는 메서드이다.
* 삭제된 요소를 반환한다. 빈 배열에 shift를 호출하면 undefined를 반환한다.   

```javascript
const arr = ["a", "b", "c", "d", "e"];

arr.shift(); // "a"
console.log(arr); // ["b", "c", "d", "e"]
```

## splice
* 문법: array.splice(start[, deleteCount[, item1[, item2[, ...]]]])
* 원본 배열에 기존 요소를 삭제 또는 교체하거나 새 요소를 추가해주는 메서드이다.
* 삭제한 요소를 담은 배열을 반환한다. 아무 값도 삭제하지 않았으면 빈 배열을 반환한다.
* start
  * 배열의 변경을 시작할 인덱스
  * 배열의 길이보다 큰 값일 경우 배열의 길이로 설정된다.
  * 음수인 경우 배열의 끝에서부터 음수의 절대값만큼 거꾸로 계산된다. 음수값의 절대값이 배열의 길이 보다 큰 경우 0으로 설정된다.
* deleteCount
  * 배열에서 삭제할 요소의 수입니다.
  * 생략하거나 값이 array.length - start보다 크면 start부터 모든 요소를 삭제한다.
  * deleteCount가 음수라면 어떤 요소도 삭제하지 않는다. 이 때는 최소한 하나의 새로운 요소(item1)를 지정해야 한다.
* item1, item2, ...
  * 배열에 추가할 요소이다. 아무 요소도 지정하지 않으면 splice()는 요소를 삭제하기만 한다.

```javascript
// 삭제
const arr = ["a", "b", "c", "d", "e"];
arr.splice(1, 3); // ["b", "c", "d"]
console.log(arr); // ["a", "e"]

const arr = ["a", "b", "c", "d", "e"];
arr.splice(2); // ["c", "d", "e"]
console.log(arr); // ["a", "b"]

const arr = ["a", "b", "c", "d", "e"];
arr.splice(-2, 3); // ["d", "e"] ( => arr.splice(-2) )
console.log(arr); // ["a", "b", "c"]

const arr = ["a", "b", "c", "d", "e"];
arr.splice(-6, 3); // ["a", "b", "c"] ( => arr.splice(0, 3) )
console.log(arr); // ["d", "e"]

const arr = ["a", "b", "c", "d", "e"];
arr.splice(1, -3); // [] ( => arr.splice(1, 0) )
console.log(arr); // ["a", "b", "c", "d", "e"]


// 삭제하지 않고, 추가
const arr = ["a", "b", "c", "d", "e"];
arr.splice(1, 0, "aa"); // []
console.log(arr); // ["a", "aa" "b", "c", "d", "e"]


// 삭제하고, 그 자리에 추가
const arr = ["a", "b", "c", "d", "e"];
arr.splice(1, 3, "aa"); // ["b", "c", "d"]
console.log(arr); // ["a", "aa", "e"]
```