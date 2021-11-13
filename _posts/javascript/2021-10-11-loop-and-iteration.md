---
title: "반복문(for, for...in, while, do...while)"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [js loop, loop, for, for...in, while, do...while]
date: 2021-10-11
---

개발자마다 주로 사용하는 반복문이 있을 것이다.  
가장 기본인 for문을 주로 많이 사용할텐데 for문 외에도 다양한 반복문이 있지만 조금씩 기능이 다르다.  
그 차이점을 비교해보도록 하자.

## for
* 문법

```javascript
for (초기문; 조건문; 증감문){
  실행문;
} // 실행문이 한 줄인 경우 중괄호 생략 가능
```
* 조건문이 falsy로 판별될 때까지 실행문을 반복한다.
* for문이 실행되는 순서
  1. 초기화 구문인 초기문이 존재한다면 for문이 실행될 때 제일 처음으로 한번만 실행된다. 이 표현은 보통 변수로 선언되어 0이나 반복문 카운터로 초기 설정이 된다.
  2. 조건문은 조건을 검사한다. 만약 조건문이 truthy라면 실행문으로 넘어가게 되고, 만약 조건문이 falsy라면 그 for문은 여기서 종결된다. 만약 그 조건문이 생략된다면, 그 조건문은 truthy로 추정한다.
  3. 실행문이 실행된다. 많은 문장을 실행할 경우엔, { } 를 써서 문장들을 묶어준다.
  4. 갱신 구문인 증감문이 존재한다면 실행되고, 2번째 단계로 돌아가 falsy가 반환될 때까지 계속 반복 된다.

```javascript
var i;
function init () {
  console.log('A');
  i = 0;
}
function condition () {
  console.log('B');
  // if(i < 2){
  // 	return true;
  // }
  return i < 2; // 위의 if문과 동일
}
function update () {
  console.log('C');
  i++;
}

for (init(); condition(); update()) {
}

// A > B > C > B > C > B
```
* 앞의 초기문, 조건문, 증감문은 모두 생략이 가능하다. (반복문 이전의 코드에서 변수를 선언했을 경우나 실행문에서 증감을 할 경우 등등)

## for ... in
* 문법

```javascript
for (변수 in 객체){
  실행문;
}
```
* for문과 달리 객체의 갯수만큼 반복문을 돈다.
* 지정한 변수는 key(또는 index)를 나타낸다.

```javascript
let obj = { a: 1, b: 2, c: 3 };
for (let i in obj) {
  console.log(i, object[i]);
}
// a 1
// b 2
// c 3

let arr = [1, 2, 3];
for (let i in arr) {
  console.log(i, arr[i]);
}
// 0 1
// 1 2
// 2 3
```

## while
* 문법

```javascript
while (조건문;){
  실행문;
}
``` 
* 조건문이 falsy로 판별될 때까지 실행문을 반복한다.
* for문과 달리 조건문만 들어가므로 초기문이 반복문 밖에 있을 때 주로 사용한다.

```javascript
var i = 0;
while (i < 3) {
  console.log(i); // 0, 1, 2
  i++;
}

var i = 2;
while (i >= 0) {
  console.log(i); // 2, 1, 0
  i--;
}
```

## do ... while
* 문법

```javascript
do {
  실행문
}
while (조건문);
```
* 조건문이 falsy로 판별될 때까지 실행문을 반복한다.
* while문과 달리 구문이 실행된 뒤에 테스트 조건이 평가됨으로 구문은 무조건 한 번은 실행된다.

```javascript
let result = '';
let i = 0;
do {
  i++;
  result += i;
} while (i < 5);

console.log(result); // "12345"
```

## break문
* 반복문이나 switch문, label문에서 어떤 조건에 해당될 때 반복문을 멈추어 준다.
* break문을 만나는 즉시 반복문은 종료된다.

```javascript
let result = '';
let i = 0;
while(i < 5) {
  i++;
  if(i == 3) break;
  result += i;
}

console.log(result); // "12"
```

## continue문
* 반복문이나 switch문, label문에서 어떤 조건에 해당될 때 해당 반복문을 넘겨준다.
* break문과 달리 continue문은 해당 반복문만을 종료시키기 때문에 반복문이 종료되기 전까지 여러번 사용할 수 있다.

```javascript
let result = '';
let i = 0;
while(i < 8) {
  i++;
  if(i == 3) continue;
  if(i == 7) continue;
  result += i;
}

console.log(result.length); // "124568"
```