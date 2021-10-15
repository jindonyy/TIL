---
title: "원시타입과 참조타입"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [js type, type]
date: 2021-10-08
---

## 원시타입(primitive type)
* Number, String, boolean, undefined, null, symbol (Object를 제외한 전부) 이 원시타입에 해당된다.
* 원시 타입은 변수에 할당될 때, **메모리의 고정 크기**로 원시 값을 저장하고 해당 저장된 값을 변수가 직접적으로 가리키는 형태를 띈다.
* 값이 절대 변하지않는 **불변성**을 갖고있기때문에 때문에 재할당 시 기존 값이 변하는것 처럼 보일지 몰라도 사실 새로운 메모리에 재할당한 값이 저장되고 변수가 가리키는 메모리가 달라졌을 뿐이다.

```javascript
var a = 10;
var b = a;
a = 20;

console.log(b); // 10
```


## 참조타입(reference type)
* 원시 타입을 제외한 나머지는 참조타입(객체(Object))이다. 대표적으로 배열, 객체, 함수가 있다.
* 참조타입은 변수의 크기가 **동적으로 변한다**. 때문에 Object의 데이터 자체는 별도의 메모리 공간(참조)에 저장된다.
* 변수에 할당 시 데이터에 대한 주소(참조)가 저장되기 때문에 자바스크립트 엔진이 변수가 가지고 있는 메모리 주소를 이용해서 변수의 값에 접근하게 되는것이다.

```javascript
var arr = ["a"];
var copyArr = arr;

arr.push("b");
console.log(copyArr); // ["a", "b"]
```