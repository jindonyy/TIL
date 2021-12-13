---
title: "정렬 알고리즘"
layout: single
classes: wide
categories:
  - data structure
tags:
  - [data structure, sort]
date: 2021-12-12
---

## 정렬 알고리즘이란?
정렬 알고리즘은 어떤 집합(예를 들어 배열)의 항목을 정렬하여 안의 요소들이 정렬되도록 하는 과정이다.  
<p style="margin-bottom: 0.5em;">예시)</p>  
* 가장 작은 숫자에서 가장 큰 숫자 순으로 정렬
* 알파벳 순으로 이름 정렬
* 제작 연도에 따른 동영상 정렬
  
정렬 알고리즘의 종류는 매우 많지만 대표적인 7가지 버블, 선택, 삽입, 셸, 합병, 퀵, 기수 정렬에 대해 다뤄볼 것이다.  
   
정렬 알고리즘 속도 시각화 사이트: [https://www.toptal.com/developers/sorting-algorithms](https://www.toptal.com/developers/sorting-algorithms)

## 정렬 알고리즘을 배워야하는 이유
* 정렬은 매우 일반적인 작업이므로 어떻게 작동하는지 아는 것이 좋다.  
* 정렬하는 방법에는 여러 가지가 있고, 그 방법 마다 장단점이 있다.  
  \- 예를 들어, 데이터가 거의 정렬되어 있지만 한 두 개가 삐져나와 있는 경우에는 특정 알고리즘이 더 빠르다.  
    이런 알고리즘들은 다른 경우에는 느린 편이지만 이 경우에서는 아주 빠르다.
* 정렬은 가끔식 특이한 점이 있으므로, 탐색하는 방법을 이해하는 것이 좋다.

## 자바스크립트에서 정렬 메서드(sort)
자바스크립트 배열에서는 이미 정렬 기능이 있는 내장 메서드가 있다.  
하지만 이 메서드는 언제나 정확하지 않다.
```javascript
[ "Steele", "Colt", "Data Structures", "Algorithms" ].sort();
// [ "Algorithms", "Colt", "Data Structures", "Steele" ]
```
위와 같이 문자열 배열을 알파벳의 오름차순으로 정렬하기 위해 사용하기 위해서는 sort메서드가 유용하다.  
```javascript
[ 6, 4, 15, 10 ].sort();
// [ 10, 15, 4, 6 ]
```
그러나 위와 같이 두자리 이상의 숫자가 포함된 배열을 정렬할 떄는 올바르지 않다.  
왜냐하면 sort 메서드는 정렬 순서는 유니코드 값을 가지고 결정된다.  
그 말은 유니코드라는 녀석이 이 값들을 표현하게 된다는 것이다.  
그러면 배열에 있는 것들이 다 문자열로 바뀌어서 유니코드 값으로 변환된 다음에 그 값들이 정렬된 것이라는 말이다.  
숫자도 문자열로 바뀌었기 때문에 앞의 한글자씩 비교를 하게 되므로 1이 앞글자인 10과 15가 먼저 오게되는 것이다.  
  
이런 문제를 없애기 위해 sort안에 callback 함수를 넣어주어야 한다.  
콜백 함수에는 두 가지 매개 변수를 넣을 수 있다. 흔히들 a, b로 많이 넣는다.  
sort는 음수 값이 return 되면, a가 b보다 먼저 오도록 한다.  
반대로 양수 값이 return 되면 b가 a보다 먼저 오도록, 0이 return 되면 a와 b를 같은 값으로 정렬하게 된다.
```javascript
function numberCompare(a, b) {
  return a - b;
}

[ 6, 4, 15, 10 ].sort(numberCompare);
// [ 4, 6, 10, 15 ]

function compareByLen(str1, str2) {
  return str1.length - str2.length;
}

[ "Steele", "Colt", "Data Structures", "Algorithms" ].sort(compareByLen);
// [ "Colt", "Steele", "Algorithms", "Data Structures" ]
```

## 정렬하기 전, swap 하기
내장 메서드인 sort가 아닌 정렬 알고리즘의 종류들을 다음 포스트들에서 다룰 건데,  
해당 정렬들을 하기 전에 swap 기능을 먼저 이해해야 한다.  
많은 정렬 알고리즘은 특정 유형의 스와핑 기능(예를 들어 숫자로 스와핑하여 순서대로 배열)을 포함한다.  
```javascript
// ES5
function swap(arr, idx1, idx2) {
  var temp = arr[idx1];
  arr[idx1] = arr[idx2];
  arr[idx2] = temp;
}
```
swap라 적으니 어려워보이지만 말그대로 두가지 항목을 정렬을 위해 바꾸어 주는 것이다.  
전체 배열과 바꾸어주려는 두 인덱스를 매개 변수로 받고 두 위치를 바꾸어준다.
```javascript
// ES2015
const swap = (arr, idx1, idx2) => {
  [arr[idx1],arr[idx2]] = [arr[idx2],arr[idx1]];
}
```
ES2015로 넘어오면서 구조 분해 할당 기능이 추가 되었다.  
해당 기능은 아래의 사이트를 참고하자.  
[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#array_destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#array_destructuring)