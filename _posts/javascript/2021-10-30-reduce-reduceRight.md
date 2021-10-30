---
title: "배열의 요소 누적하기(reduce, reduceRight)"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [js array, array, reduce, reduceRight]
date: 2021-10-30
---

## reduce
* 배열의 각 요소에 대해 주어진 callback 함수를 실행하고, 실행한 내용을 accumulator에 저장하여 최종 accumulator를 반환한다.
* 문법: array.reduce(callback(accumulator, currentValue[, currentIndex, array])[, initialValue])
  * callback: 배열의 각 요소에 대해 실행할 함수로 다음 네 가지 인수를 받는다.
  * accumulator: callback 함수를 실행하고, 실행한 내용을 누적한다. initialValue가 있을 경우 initialValue가 초기값으로, 없을 경우 array의 0번째 요소가 초기값으로 설정된다.
  * currentValue: 처리할 현재 요소이다. initialValue가 있을 경우 0번째 요소부터, 없을 경우 1번째 요소부터 시작된다.
  * currentIndex: 처리할 현재 요소의 인덱스이다. initialValue가 있을 경우 0부터, 없을 경우 1부터 시작된다.
  * array: reduce()를 호출한 배열이다.
  * initialValue: accumulator의 초기값으로 설정할 타입. 초기값을 제공하지 않으면 배열의 첫 번째 요소를 사용한다. 빈 배열에서 초기값 없이 reduce()를 호출하면 오류가 발생한다.

```javascript
var arr = [1, 2, 3, 4]
arr.reduce(function(accumulator, currentValue, currentIndex, array) {
    console.log(accumulator, currentValue, currentIndex, array, accumulator + currentValue);
    return accumulator + currentValue;
});
// 1 2 1 [1, 2, 3, 4] 3
// 3 3 2 [1, 2, 3, 4] 6
// 6 4 3 [1, 2, 3, 4] 10

// 초기값(initialValue)를 설정한 경우
arr.reduce(function(accumulator, currentValue, currentIndex, array) {
    console.log(accumulator, currentValue, currentIndex, array, accumulator + currentValue);
    return accumulator + currentValue;
}, 10);
// 10 1 0 [1, 2, 3, 4] 11
// 11 2 1 [1, 2, 3, 4] 13
// 13 3 2 [1, 2, 3, 4] 16
// 16 4 3 [1, 2, 3, 4] 20
```

#### reduce vs map

```javascript
var data = [1, 2, 3];

var result1 = data.reduce((accumulator, value) => {
    accumulator.push(value * 2);
    return accumulator;
}, []);
console.log(result1); // [2, 4, 6]

var result2 = data.map(x => x * 2);
console.log(result2); // [2, 4, 6]
```
reduce를 이용하면 map의 기능도 구현할 수 있다. 그러나 reduce에 비해 map이 짧고 직관적이다. 반환하는 값이 배열이며 배열의 요소 전체를 반환해야 한다면 map을 사용하는 것이 훨씬 효율적이다.

### reduce vs filter
```javascript
var data = [1, 2, 3, 4, 5, 6];

var result1 = data.reduce((accumulator, value) => {
    if (value % 2 != 0) accumulator.push(value);
    return accumulator;
}, []);
console.log(result1); // [1, 3, 5]

var result2 = data.filter(x => x % 2 != 0);
console.log(result2); // [1, 3, 5]
```
reduce로 filter도 구현할 수 있다. 그러나 filter 또한 reduce보다 짧고 직관적이다. 반환할 타입을 설정할 수 있는 것이 reduce의 장점이지만 반환하는 값이 배열일 때는 filter를 사용하는 것이 훨씬 효율적이다.

### reduce vs filter + map  
reduce가 구현할 수 있는 메서드들을 여러 개 사용해야 한다면 어떨까?
```javascript
var data = [1, 2, 3, 4, 5, 6];

var result1 = data.reduce((accumulator, value) => {
    if (value % 2 != 0) accumulator.push(value * 2);
    return accumulator;
}, []);
console.log(result1); // [2, 6, 10]

var result2 = data.filter(x => x % 2 != 0).map(x => x * 2);
console.log(result2); // [2, 6, 10]
```
위의 소스를 보면 result1에서는 reduce가 한번의 배열 반복을 통해 filter와 map에서 하는 기능을 하지만 result2에서는 filter로 인해 한번, map으로 인해 한번 총 두번의 반복을 돌게 된다. 배열의 갯수가 많아진다면 reduce가 훨씬 효율적이고 함수로 로직이 따로 빠져있어 재사용할 수 있다.

### reduce의 활용
* 배열의 요소 갯수 세기

```javascript
var names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice'];

var countedNames = names.reduce(function (allNames, name) {
    if (name in allNames) allNames[name]++;
    else allNames[name] = 1;
    return allNames;
}, {});

console.log(countedNames); // { 'Alice': 2, 'Bob': 1, 'Tiff': 1, 'Bruce': 1 }
```

* 배열의 중복 요소 제거하기

```javascript
var arr = [1, 2, 1, 2, 3, 5, 4, 5, 3, 4, 4, 4, 4];

var result = arr.sort().reduce((accumulator, current) => {
    var length = accumulator.length;
    if (length === 0 || accumulator[length - 1] !== current) accumulator.push(current);
    return accumulator;
}, []);

console.log(result); // [1, 2, 3, 4, 5]
```
  
* 평균 구하기

```javascript
var data = [1, 2, 3, 4, 5, 6, 1];
var reducer = (accumulator, value, index, array) => {
    var sumOfAccAndVal = accumulator + value;
    if (index === array.length - 1) return (sumOfAccAndVal) / array.length;
    return sumOfAccAndVal;
};

var getMean = data.reduce(reducer, 0);
console.log(getMean); // 3.142857142857143
```

* 다중 배열 합치기

```javascript
var data = [[1, 2, 3], [4, 5, 6], [7, 8, 9]];
var flatArrayReducer = (accumulator, value, index, array) => {
    return accumulator.concat(value);
};
var flattenedData = data.reduce(flatArrayReducer, []); 
console.log(flattenedData) // [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```


## reduceRight
* reduce와 기능은 같지만 배열의 역순으로 currentValue와 currentIndex를 받는다.
* 문법: array.reduce(callback(accumulator, currentValue[, currentIndex, array])[, initialValue])
  * callback: 배열의 각 요소에 대해 실행할 함수로 다음 네 가지 인수를 받는다.
  * accumulator: callback 함수를 실행하고, 실행한 내용을 누적한다. initialValue가 있을 경우 initialValue가 초기값으로, 없을 경우 array의 length-1번째 요소가 초기값으로 설정된다.
  * currentValue: 처리할 현재 요소이다. initialValue가 있을 경우 length-1번째 요소부터, 없을 경우 length-2번째 요소부터 시작된다.
  * currentIndex: 처리할 현재 요소의 인덱스이다. initialValue가 있을 경우 length-1부터, 없을 경우 length-2부터 시작된다.
  * array: reduce()를 호출한 배열이다.
  * initialValue: accumulator의 초기값으로 설정할 타입. 초기값을 제공하지 않으면 배열의 첫 번째 요소를 사용한다. 빈 배열에서 초기값 없이 reduce()를 호출하면 오류가 발생한다.

```javascript
var arr = [1, 2, 3, 4]
arr.reduceRight(function(accumulator, currentValue, currentIndex, array) {
    console.log(accumulator, currentValue, currentIndex, array, accumulator + currentValue);
    return accumulator + currentValue;
});
// 4 3 2 [1, 2, 3, 4] 7
// 7 2 1 [1, 2, 3, 4] 9
// 9 1 0 [1, 2, 3, 4] 10

// 초기값(initialValue)를 설정한 경우
arr.reduce(function(accumulator, currentValue, currentIndex, array) {
    console.log(accumulator, currentValue, currentIndex, array, accumulator + currentValue);
    return accumulator + currentValue;
}, 10);
// 10 4 3 [1, 2, 3, 4] 14
// 14 3 2 [1, 2, 3, 4] 17
// 17 2 1 [1, 2, 3, 4] 19
// 19 1 0 [1, 2, 3, 4] 20

// 이중 배열일 경우
var flattened = [[0, 1], [2, 3], [4, 5]].reduceRight(function(a, b) {
    return a.concat(b);
}, []);
console.log(flattened); // [4, 5, 2, 3, 0, 1]
// 배열 안의 배열 안까지 역순으로 받지 않는다.
```