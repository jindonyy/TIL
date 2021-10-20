---
title: "깊은 복사 VS 얕은 복사"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [js copy, type, deep copy, shallow copy]
date: 2021-10-09
---

## 깊은 복사 (deep copy)
* 데이터 **값 자체**를 복사해오는 것이다.
* 원시타입을 복사할 때 얕은 복사가 이루어진다. 원시 타입은 변수에 할당될 때, 독립적인 메모리에 값 자체를 할당하여 생성한다. 때문에 원시 타입의 복사는 원시타입이 가지고 있는 값 자체를 복사해온다.

```javascript
var a = 10;
var b = a;
a = 20;

console.log(a)); // 20
console.log(b); // 10
console.log(a === b); // false
```


## 얕은 복사 (shallow copy)
* 참조(주소)값을 복사해오는 것이다. 참조 할당이라고도 한다.
* 참조타입을 복사할 때 얕은 복사가 이루어진다. 참조 타입은 변수의 크기가 동적으로 변한다. 이러한 특징 때문에 Object의 데이터 자체는 별도의 메모리 공간(heap)에 저장되며, 변수에 할당 시 데이터 값이 아닌 메모리의 주소값(참조)이 저장되기 때문에 자바스크립트 엔진이 변수가 가지고 있는 메모리 주소를 이용해서 변수의 값에 접근하게 되는것이다. 이로 인해 복사를 할 때 또한 메모리 주소가 복사 되는 것이다.

```javascript
var arr = ["a"];
var copyArr = arr;

arr.push("b");
console.log(arr); // ["a", "b"]
console.log(copyArr); // ["a", "b"]
console.log(arr === copyArr); // true

var obj = {
  a: 1
}
var copyObj = obj;

copyObj.a = 2;
console.log(obj.a); // 2
console.log(obj === copyObj); // true
```


## 객체의 깊은 복사
객체의 원본을 그대로 유지하고 복사하여 수정하고 싶을 때는 어떻게 해야할까?

### slice
* 문법: array.slice(start[, end])
* 배열열의 start부터 end 전까지 배열의 부분 새로운 문자열을 반환해주는 메서드이다. <u>객체가 아닌 배열의 복사만 사용할 수 있다.</u>
* 그러나 slice를 활용한 복사는 완벽한 깊은 복사가 아니다. 배열 안의 배열인 2중 배열일 경우, *안의 하위 배열까지는 깊은 복사가 이루어지지 않는다.*

```javascript
var arr = [1, 2, 3, 4];
var copyArr = arr.slice();
console.log(arr === copyArr); // false

copyArr[0] = 0;
console.log(arr); // [1, 2, 3, 4]

// 2중 배열
var arr = [[1, 2], [3, 4]];
var copyArr = arr.slice();
console.log(arr[0]=== copyArr[0]); // true

copyArr[0][0] = 'a';
console.log(arr); // [['a', 2], [3, 4]]
```

### assign
* 문법: Object.assign(target, ...sources)
* 깊은 복사를 위해서는 메서드의 첫번째 인수로 빈 객체를 넣어주며, 두번째 인수로 할당할 객체를 넣으면 된다.
* 그러나 Object.assign()를 활용한 복사 또한 완벽한 깊은 복사가 아니다. 객체 안의 객체인 2중 객체일 경우, *안의 하위 객체까지는 깊은 복사가 이루어지지 않는다.*

```javascript
var obj = {
  a: 1
};
var copyObj = Object.assign({}, obj);
console.log(obj === copyObj); // false

copyObj.a = 2;
console.log(obj); // {a: 1}

// 2중 객체
var obj = {
  a: 1,
  b: {
    c: 2,
  },
};
var copyObj = Object.assign({}, obj);
console.log(obj.b === copyObj.b); // true

copyObj.b.c = 3;
console.log(obj); // {a: 1, b: {c: 3}}
```

### 전개 연산자(Spread Operator)
* 문법: { ...target }
* Object.assign()과 마찬가지로 완벽한 깊은 복사가 아니다. 객체 안의 객체인 2중 객체일 경우, *안의 하위 객체까지는 깊은 복사가 이루어지지 않는다.*

```javascript
var obj = {
  a: 1,
    b: {
      c: 2,
    },
  };
  
var copyObj = { ...obj };
console.log(obj.b === copyObj.b); // true

copyObj.b.c = 3;
console.log(obj); // {a: 1, b: {c: 3}}
```

### JSON 객체 메소드
* 문법  
  * JSON.stringify(target)  
  인수로 객체를 받으며, 받은 객체를 문자열로 치환시켜준다.
  * JSON.parse(target)
  인수로 문자열을 받으며, 받은 문자열을 객체로 치환시켜준다.
* 먼저, obj 객체를 JSON.stringify() 메소드를 이용하여 문자열로 변환한 뒤, 다시 JSON.parse() 메소드로 객체로 변환하는 방법이다. 문자열로 변환한 뒤 다시 객체로 변환하였기에 2차원 객체에 대한 참조가 사라지는 원리이다.
* 하지만, 이 방법도 2가지 문제가 있는데, 다른 방법에 비해 성능이 느린 점과 JSON.stringify() 메소드는 함수를 만났을 때 undefined로 처리한다는 점이다.

```javascript
var obj = {
  a: 1,
  b: {
    c: 2,
  },
};
var copyObj = JSON.parse(JSON.stringify(obj));
console.log(obj.b === copyObj.b); // false

copyObj.b.c = 3;
console.log(obj); // {a: 1, b: {c: 2}}
```