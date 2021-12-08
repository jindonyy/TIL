---
title: "this를 바꿔주는 메서드"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [js this method, call, apply, bind]
date: 2021-12-08
---

흔하게 쓰는 경우는 아니지만 함수를 호출할 때 다른 object의 property를 this 사용해야할 때 어떻게 해야할까??  
이럴때 사용하는게 아래의 3가지 메서드이다. 모두 함수 내의 this를 바꿔주는 기능은 같지만 문법 이 다르다.  

## call
* 문법: func.call(thisArg[, arg1[, arg2[, ...]]])
  * thisArg: func 호출에 제공되는 this의 값
  * arg1, arg2, ...: func에 호출되어야 하는 인수
* this 와 arguments 를 매개로 호출된 함수의 결과를 반환한다.

```javascript
var member1 = {
  id: "jenny",
  favorite: function(friend, food) {
    console.log(friend + "와" + this.id + "는" + food + "를 좋아합니다.");
  }
};

var member2 = {
  id: "jisu"
};

member1.favorite("lose", "sandwitch"); // lose와 jenny는 sandwitch를 좋아합니다.
member1.favorite.call(member2, "lose", "sandwitch"); // lose와 jisu는 sandwitch를 좋아합니다.
```

## apply
* 문법: func.apply(thisArg, [argsArray])
  * thisArg: func 호출에 제공되는 this의 값
  * argsArray
    * func에 호출되어야 하는 인수를 지정하는 **유사 배열 객체**
    * 함수에 제공된 인수가 없을 경우 null 또는 undefined이다.
* this 와 arguments 를 매개로 호출된 함수의 결과를 반환한다.
* call()과 다르게 apply()는 두 번째 매개변수를 배열 형태로 넣게된다는 차이점이 있다.(유사 배열)

```javascript
var member1 = {
  id: "jenny",
  favorite: function(friend, food) {
    console.log(friend + "와" + this.id + "는" + food + "를 좋아합니다.");
  }
};

var member2 = {
  id: "jisu"
};

member1.favorite("lose", "sandwitch"); // lose와 jenny는 sandwitch를 좋아합니다.
member1.favorite.apply(member2, ["lose", "sandwitch"]); // lose와 jisu는 sandwitch를 좋아합니다.
```

## bind
* 문법: func.bind(thisArg[, arg1[, arg2[, ...]]])
  * thisArg: 바인딩 함수가 타겟 함수의 this에 전달하는 값
  * arg1, arg2, ...: func에 호출되어야 하는 인수
* bind()는 새롭게 바인딩한 함수를 만든다. 바인딩한 함수는 원본 함수 객체를 감싸는 함수이다. 쉽게 말해 bind()는 call(), apply()와 같이 함수가 가리키고 있는 this를 바꾸지만 **호출되지는 않는다**. 즉, call(this, 1, 2, 3)은 bind(this)(1, 2, 3)과 같다는 말이다.

```javascript
var member1 = {
  id: "jenny",
  favorite: function(friend, food) {
    console.log(friend + "와" + this.id + "는" + food + "를 좋아합니다.");
  }
};

var member2 = {
  id: "jisu"
};

member1.favorite("lose", "sandwitch"); // lose와 jenny는 sandwitch를 좋아합니다.
member1.favorite.bind(member2)("lose", "sandwitch"); // lose와 jisu는 sandwitch를 좋아합니다.
```