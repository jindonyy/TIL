---
title: "해시 테이블(Hash table)"
header:
  teaser: /assets/images/data-structure/2021-12-22-hash-table_teaser.png
layout: single
classes: wide
categories:
  - data structure
tags:
  - [data structure, hash table, tree travers]
date: 2021-12-22
---

## 해시 테이블
* 해시 테이블은 key-value 쌍으로 데이터를 저장하는 자료구조
* 배열과 비슷하지만 키는 순서를 가리키지 않는다. 
* 때문에 접근과 탐색, 추가, 제거 모두 빠르다. 때문에 해시 테이블은 모든 언어에서 자주 사용된다.
* 거의 모든 프로그래밍 언어에는 일종의 해시 테이블 데이터 구조가 있다.  
js에서는 객체와 Map이 해시 테이블 역할을 한다. (객체에는 몇 가지 제한 사항이 있지만 기본적으로 해시 테이블이다.)
* 해시 테이블은 각각의 key값에 **해시 함수**를 적용해 배열의 고유한 index를 생성하고, 이 index를 활용해 값을 저장하거나 검색하게 된다.
<img src='{{ "/assets/images/2021-12-22-hash-table_1.png" | relative_url }}' style="width:450px;" /> 



#### 해시 테이블이 필요한 이유
배열에서는 key로 숫자를 사용한다. 그러나 우리는 숫자만으로 어떤 value가 나올건지 예측할 수 없다.  
즉, 문자열처럼 사람이 읽을 수 있는 값을 key로 사용하여 value를 얻을 수 있다면 좋을 것이다.  
color[2] 보다 color["cyan"]가 사용하기 수월하다.

#### 구현 조건
* 배열을 사용해 저장한다.
* key로 문자열을 사용한다.

## 해시 함수
* key로 value를 얻으려면 배열에서 사용할 index로 바꿔줘야한다.  
이렇게 key를 숫자로 바꿔주는 함수를 해시 함수라 한다.
<img src='{{ "/assets/images/2021-12-22-hash-table_2.png" | relative_url }}' style="width:750px;" /> 

* 단방향 함수이기 때문에 반대로 인덱스를 넣어서 key값을 얻을 수는 없다.
* 해시 함수는 비밀번호, 암호화폐, 사이트 로그인 인증 등 암호화 기능에 많이 사용된다.  
해시 함수의 종류는 많은데, 그 중 암호화 해시 함수를 사용한다.

### 좋은 해시란?
* 빨라야한다.(일정한 시간)  
해시함수는 접근, 삭제, 추가 등을 할 때 항상 사용해야하므로 빨라야 한다.  
  
**< 좋지 않은 해시 함수 예>**
```javascript
function hash(key, arrayLen) {
  let total = 0;
  for (let char of key) {
    let value = char.charCodeAt(0) - 96;
    total = (total + value) % arrayLen;
  }
  return total;
}
```
문자열의 길이만큼 순회를 하는 함수이다.  
때문에 긴문자열에서는 느릴 수 밖에 없는 O(N)이다.
* 일관된 방식으로 분배를 해서 최대한 다른 것들과 겹치지 않게 고루분배 되도록 해야 한다.  
  
**< 좋지 않은 해시 함수 예>**
```javascript
function sameHashedValue(key) {
  return 0;
}
```
어떤 키를 넣든 항상 0을 반환하는 함수이다.  
길이가 100인 배열에 500개의 요소를 넣는다고 한다면 모두 0번째 인덱스에 들어가게 된다.
* 특정 값을 입력할 때마다 항상 같은 출력값이 나와야 한다.  
꼭 문자열이 아니라 사진, PDF, 영상 등 타입이 어떻든, 문자열이라면 그 길이가 어떻든 한 값을 넣었을 떄 항상 같은 숫자를 반환해야 한다.  
  
**< 좋지 않은 해시 함수 예>**
```javascript
function randomHash(key) {
  return Math.floor(Math.random() * 1000)
}
```
동일한 값을 넣어도 항상 다른 인덱스를 반환하므로 좋지 않은 해시 함수이다.

### 해시 함수 구현
⚠️예시에선 key값으로 문자열만 사용하여 구현

1. key값과 저장할 배열의 길이를 매개변수로 받는다.
2. 문자열의 길이를 index로 사용한다면 충돌나는 부분이 많을 것이다. 때문에 `charCodeAt`(UTF 16 글자 코드)를 사용할 것이다.
3. `Math.min`을 사용하여 배열이 너무 많이 돌지 않도록 문자열의 길이와 key로 들어올 문자열들의 평균적 길이를 고려한 값(예시에서는 100 사용) 중에 작은 값만큼 순회한다.  
(문자열로 어떤 값들이 들어오는지를 보고 for문의 시작점과 종료점을 조정해야한다. 예를 들면 앞의 두글자가 항상 같은 값들이 들어온다고 하면 3번째 글자부터 순회할 수 있도록 조정해야 한다.)
4. 충돌을 줄이기 위해선 배열의 길이가 크고, `소수`를 이용하는 것이 좋다.(배열의 길이는 예제에서 저장할 값이 별로 없으므로 크지 않은 값을 사용) 소수를 사용해야하는 이유는 수학적 원리이므로 깊게 파고들지 않겠다..  
<img src='{{ "/assets/images/2021-12-22-hash-table_3.png" | relative_url }}' style="width:600px;" />
사용할 배열의 길이와 해시 함수의 충돌 수를 나타낸 표이다.  
표를 보면, 소수인 8191, 8209 등과 같은 소수가 짝수인 값들에 비해 충돌 횟수가 현저히 적은 것을 볼 수 있다.<br>
<br>
이유가 궁금하신 분들을 위해 링크 첨부  
<a href="https://computinglife.wordpress.com/2008/11/20/why-do-hash-functions-use-prime-numbers/">해시 함수에서 소수를 사용하는 이유</a>  
<a href="https://www.quora.com/Does-making-array-size-a-prime-number-help-in-hash-table-implementation-Why">배열의 크기를 소수로 만드는 것이 도움이 될까?</a>

```javascript
function hash(key, arrayLen) {
  let total = 0;
  let WEIRD_PRIME = 31;
  // 문자열의 길이가 30이면 30만큼, 200이면 100만큼 순회
  for (let i = 0; i < Math.min(key.length, 100); i++) {
    let char = key[i];
    // "a"의 코드는 97이므로 96을 빼주어 "a"가 1이 되도록 한다. (b => 2, c => 3, ...)
    let value = char.charCodeAt(0) - 96
    // 소수인 31을 사용하는 것은 수학적 원리..!
    // 문자열이 길어지면 값이 커지므로 배열의 길이만큼 나누어 준다.
    total = (total * WEIRD_PRIME + value) % arrayLen;
  }
  return total;
}

hash("pink", 13); // 5
```
<br>
⭐️ key로 들어올 값들을 고려해서 유동적으로 해시 함수를 구현해야 한다! ⭐️

## 해시 충돌
해시 함수를 아무리 잘 구현해도 배열의 길이를 들어오는 값만큼 늘리지 않는한 언제가는 해시끼리 충돌이 나는 경우가 생긴다.
떄문에 충돌을 해결해주어야 하는데 이 방법도 여러 가지가 있다.  
그 중에서 우리는 `개별 체이닝`과 `직선 탐색법`을 보도록 하겠다.

### 개별 체이닝(Separate Chaining)
충돌이 일어났을 경우 한 인덱스에 함께 저장하는 방법이다.
이때 저장은 여러 값이 들어갈 수 있도록 배열 또는 연결 리스트와 같은 데이터 구조를 사용하여야 한다.
<img src='{{ "/assets/images/2021-12-22-hash-table_4.png" | relative_url }}' style="width:600px;" />
충돌이 났을 경우 이중 배열로 저장한다.

### 선형 탐색(Linear Probing)
충돌을 발견하면 배열을 검색하여 다음(앞으로 가든 뒤로 가든 자유) 빈 슬롯을 찾는 방법이다.  
<img src='{{ "/assets/images/2021-12-22-hash-table_5.png" | relative_url }}' style="width:600px;" />
한 위치에 하나의 요소만 저장한다는 규칙을 지키는 방법이다.  
이 방식이 조금 더 복잡하지만, 데이터가 같은 인덱스에 저장되는 것을 막을 수 있다.  
즉, 중첩 구조의 데이터를 저장할 필요가 없다.  
하지만, 배열이 금방 차게 될것이고, 그럼 배열의 길이를 늘려주거나 개별 체이닝 방식을 사용해야 한다.  
  
때문에 다음 구현에서는 개별 체이닝을 사용하도록 하겠다.

## 해시 테이블의 구현
1. 배열의 길이만큼 빈 배열을 만든다.
1. 해당 배열의 길이를 해시 함수에서 사용한다.

```javascript
class HashTable {
  constructor(size=53){
    this.buckets = new Array(size);
  }

  // 해시 함수
  _hash(key) {
    let total = 0;
    let WEIRD_PRIME = 31;
    for (let i = 0; i < Math.min(key.length, 100); i++) {
      let char = key[i];
      let value = char.charCodeAt(0) - 96
      total = (total * WEIRD_PRIME + value) % this.buckets.length;
    }
    return total;
  }
}

let hashTable = new HashTable(17);
```

### set
해시 테이블에 값을 추가해주는 메서드
1. 키와 값을 매개 변수로 받는다.
1. 해시 함수를 이용해 키를 해시로 바꿔준다.
1. 해시를 인덱스로 사용하여 해시 테이블에서 해당 인덱스로 이동한다.
1. 개별 체이닝을 이용하여 해당 인덱스에 값이 없으면 중첩 구조로 사용할 빈 배열을 만들어 준다.
1. 중첩 구조에 키-값 쌍을 push한다.

```javascript
set(key, value) {
  let index = this._hash(key);
  const dataArr = this.buckets[index];
  if(!this.dataArr) { // 해당 인덱스에 값이 없으면
    this.dataArr = [[key, value]]; // 중첩구조로 사용한 빈 배열
    return;
  }
   this.dataArr.forEach((data, i) => {
    if(data[0] === key) { // 해당 인덱스에 추가하려는 키가 있으면
      this.dataArr[i][1] = value;
    } else { // 해당 인덱스에 추가하려는 키가 없으면
      this.dataArr.push([key, value]);
    }
  });
}
```

### get
해시 테이블에서 키를 이용해 값을 가져오는 메서드
1. 키를 매개 변수로 받는다.
1. 해시 함수를 이용해 키를 해시로 바꿔준다.
1. 해시를 인덱스로 사용하여 해시 테이블에서 해당 인덱스로 이동한다.
1. 중첩 구조이므로 해당 인덱스 안에서 루프를 돌아 해당 키에 맞는 값을 찾는다.
1. 키를 찾을 수 없으면 undefined, 찾았으면 값을 반환한다.

```javascript
get(key) {
  let index = this._hash(key);
  if(this.buckets[index]) { // 해당 인덱스에 값이 있으면
    this.buckets[index].forEach(data => {
      if(this.data[0] === key) { // 해당 인덱스에 찾던 키가 있으면
        return this.data[1];
      }
    });
  }
  return undefined;
}
```

### keys
해시 테이블에 있는 모든 키를 반환하는 메서드
1. 해시 테이블 배열을 순회한다.
1. 중복된 값이 있을 시, 추가하지 않는다.
1. 값들을 담은 배열을 반환한다.

```javascript
keys() {
  let keysArr = [];
  this.buckets.forEach(dataArr => { // 첫번 째 배열 순회
    if(this.dataArr) { // 해당 인덱스에 값이 있으면
      this.dataArr.forEach(data => { // 그 안 두번 째 배열 순회 // data는 [key, value]의 배열
        keysArr.push(this.data[0])
      });
    }
  });
  return keysArr;
}
```

### values
해시 테이블에 있는 모든 값을 반환하는 메서드
1. 해시 테이블 배열을 순회한다.
1. 중복된 값이 있을 시, 추가하지 않는다.
1. 값들을 담은 배열을 반환한다.

```javascript
values() {
  let valuesArr = [];
  this.buckets.forEach(dataArr => { // 첫번 째 배열 순회
    if(this.dataArr) { // 해당 인덱스에 값이 있으면
      this.dataArr.forEach(data => { // 그 안 두번 째 배열 순회 // data는 [key, value]의 배열
        if(!valuesArr.includes(this.data[1])) { // 키 배열에 해당 value가 없으면
          valuesArr.push(this.data[1])
        }
      });
    }
  });
  return valuesArr;
}
```

## 해시 테이블의 Big O
* 삽입
  * 중복 값이 허용되는 경우
    * 최고, 보통의 경우: `O(1)`  
      \- 좋은 해시 함수를 이용해 고르게 분배 됐을 경우
    * 최악의 경우: `O(N)`  
      \- 나쁜해시 함수를 이용해 한 인덱스에 몰렸을 경우
  * 중복 값이 허용되지 않는 경우
    \- 추가할 때 항상 중복 값을 체크해줘야하므로 항상 `O(N)` 이 된다.
  * set 메서드
* 삭제
  * 최고, 보통의 경우: `O(1)`  
    \- 좋은 해시 함수를 이용해 고르게 분배 됐을 경우
  * 최악의 경우: `O(N)`  
    \- 나쁜해시 함수를 이용해 한 인덱스에 몰렸을 경우
* 접근
  * 최고, 보통의 경우: `O(1)`  
    \- 좋은 해시 함수를 이용해 고르게 분배 됐을 경우
  * 최악의 경우: `O(N)`  
    \- 나쁜해시 함수를 이용해 한 인덱스에 몰렸을 경우
  * get 메서드
* 탐색
  * 최고, 보통의 경우: `O(1)`  
    \- 좋은 해시 함수를 이용해 고르게 분배 됐을 경우
  * 최악의 경우: `O(N)`  
    \- 나쁜해시 함수를 이용해 한 인덱스에 몰렸을 경우
  * keys, values 메서드