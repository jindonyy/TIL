---
title: "이중 연결 리스트(doubly linked list)"
layout: single
classes: wide
categories:
  - data structure
tags:
  - [data structure, doubly linked list, linked list]
date: 2021-12-19
---

## 이중 연결 리스트란?
* <a href="https://jindonyy.github.io/TIL/data%20structure/single-linked-list/">단일 연결 목록</a>과 거의 동일하나 단일 연결 리스트와 달리 모든 노드에 이전 포인터가 있다.
<img src='{{ "/assets/images/2021-12-18-doubly-linked-list_1.png" | relativec_url }}' style="width:650px;" title="기수 정렬 설명" alt="기수 정렬 설명"/>

* 다른 데이터 구조 및 특정 유형의 캐시를 구현하는 데 주로 사용된다.

## 이중 연결리스트의 장점
* 양방향으로 연결되어 있기 때문에 노드를 탐색하는 방향이 양쪽으로 가능하다는 것이 큰 장점이다.
* 딘일 연결 리스트가 최악의 경우(가장 마지막 요소를 탐색)일 때, 모든 노드를 탐색해야했던 것에 반해  
이중 연결리스트는 탐색하려는 인덱스가 길이의 중간 이하냐 이상이냐에 따라 앞 또는 뒤에서 탐색하면 되므로  
단일 연결 리스트보다 탐색 속도가 1/2 횟수가 줄어든다.

## 이중 연결리스트의 장점
* 이전 노드를 지정하기 위한 변수를 하나 더 사용해야 한다. 즉, 메모리를 더 많이 사용해야 한다.
* 양방향이기 때문에 구현이 조금 더 복잡해진다.
* 하지만 장점이 크기 때문에 실제로 사용하는 연결 리스트는 대부분 이중 연결 리스트이다. 

## 이중 연결 리스트를 구현하기 위해 필요한 메서드
### push
* 연결 목록 끝에 새로운 노드 추가해주는 메서드

```javascript
class Node {
  constructor(val){
    this.val = val;
    this.next = null;
    this.prev = null;
  }
}

class SingleLinkedList {
  constroctor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  push(val){
    const newNode = new Node(val); // 새로 추가할 노드
    if(this.length === 0) { // 기존에 노드가 없으면
      this.head = newNode; // 추가한 노드가 head이자
      this.tail = newNode; // tail이다.
    } else { // 기존에 노드가 있으면
      this.tail.next = newNode; // 기존의 tail의 next를 추가할 노드로
      newNode.prev = this.tail; // 추가할 노드의 prev를 기존의 tail노드로
      this.tail = newNode; // 추가한 노드가 새로운 tail이 된다.
    }
    this.length++; // 추가했으므로 갯수 +1
    return this; // 연결 리스트를 반환
  }
}

const list = new doublyLinkedList();
list.push("HELLO");
```
<ol>
  <li>매개 변수로 value가 들어와야한다.</li>
  <li>함수에 전달된 값을 사용하여 새 노드를 만든다.</li>
  <li>목록에 노드가 없으면 head와 tail을 추가할 노드로 설정한다.</li>
  <li>목록에 노드가 있으면
    <ol>
      <li>기존 tail의 다음 포인터를 추가할 노드로 설정하한다.</li>
      <li>추가할 노드의 이전 포인터를 기존의 tail로 설정한다.</li>
      <li>목록의 tail 속성을 새 노드로 설정한다.</li>
    </ol>
  </li>
  <li>목록의 길이를 1만큼 늘린다.</li>
  <li>연결 리스트를 반환한다.</li>
</ol>

### pop
* 연결 목록의 끝에서 노드 제거해주는 메서드

```javascript
class doublyLinkedList {
  constroctor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
  pop() {
    if(!this.head) return undefined; // 리스트가 비었을 시
    const poppedNode = this.tail; // 삭제할 노드
    if(this.length === 1) { // 기존에 노드가 1개이면
      this.head = null; // head와
      this.tail = null; // tail이 비었음으로 표시
    } else { // 2개 이상의 노드가 있을 시
      this.tail = poppedNode.prev; // 삭제할 노드의 이전 노드를 tail로
      this.tail.next = null; // 새로운 tail의 다음 노드가 비었음으로
      poppedNode.prev = null; // 삭제할 노드의 이전 노드를 비었음으로
    }
    this.length--; // 삭제했으므로 갯수 -1
    return poppedNode; // 삭제한 노드를 반환
  }
}

const list = new doublyLinkedList();
list.pop();
```
<ol>
  <li>목록에 노드가 없으면 undefined를 반환한다.</li>
  <li>목록에 노드가 1개일 시, head와 tail이 null(비었음)로 표시해 삭제한다.</li>
  <li>목록에 노드가 2개 이상일 시
    <ol>
      <li>목록의 tail 속성을 기존 tail의 이전 노드로 설정한다.</li>
      <li>뒤에서 두 번째였던 노드가 tail이 됐으므로 next를 null로 설정한다.</li>
      <li>삭제할 노드의 prev를 null로 설정한다.</li>
    </ol>
  </li>
  <li>목록의 길이를 1만큼 감소한다.</li>
  <li>제거된 노드의 값을 반환한다.</li>
</ol>

### shift
* 연결 목록의 시작 부분(head) 노드를 제거해주는 메서드

```javascript
class doublyLinkedList {
  constroctor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  shift() {
    if(this.length === 0) return undefined; // 리스트가 비었을 시
    const oldHead = this.head; // 현재 head를 저장
    if(this.length === 1) { // 기존에 노드가 1개이면
      this.head = null; // head와
      this.tail = null; // tail이 비었음으로 표시
    } else { // 2개 이상의 노드가 있을 시
      this.head = oldHead.next; // 현재 head의 다음 노드를 head로 변경
      this.head.prev = null; // 새로운 head의 prev를 비었음으로
      oldHead.next = null; // 삭제할 노드의 next를 비었음으로
    }
    this.length--; // 삭제했으므로 갯수 -1
    return oldHead; // 삭제한 노드를 반환
  }
}

const list = new doublyLinkedList();
list.shift();
```
<ol>
  <li>목록에 노드가 없으면 undefined를 반환한다.</li>
  <li>목록에 노드가 1개일 시, head와 tail이 null(비었음)로 표시해 삭제한다.</li>
  <li>목록에 노드가 2개 이상일 시
    <ol>
      <li>목록의 head 속성을 기존 head의 다음 노드로 설정한다.</li>
      <li>앞에서 두 번째였던 노드가 head가 됐으므로 prev를 null로 설정한다.</li>
      <li>삭제할 노드의 next를 null로 설정한다.</li>
    </ol>
  </li>
  <li>목록의 길이를 1만큼 감소한다.</li>
  <li>제거된 노드의 값을 반환한다.</li>
</ol>

### unshift
* 연결 목록의 시작 부분에 새로운 노드 추가해주는 메서드

```javascript
class Node {
  constructor(val){
    this.val = val;
    this.next = null;
    this.prev = null;
  }
}

class doublyLinkedList {
  constroctor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
  unshift(val) {
    const newNode = new Node(val); // 새로 추가할 노드
    if(this.length === 0) { // 기존에 노드가 없으면
      this.head = newNode; // head와
      this.tail = newNode; // tail을 새로운 노드로 지정
    } else { // 기존에 노드가 있으면
      this.head.prev = newNode; // 기존의 head에 prev를 추가할 노드로 지정
      newNode.next = this.head; // 추가할 노드의 next를 기존의 head로 지정
      this.head = newNode; // head를 추가할 노드로 지정
    }
    this.length++; // 추가했으므로 갯수 +1
    return this; // 연결 리스트를 반환
  }
}

const list = new doublyLinkedList();
list.unshift("HELLO");
```
<ol>
  <li>매개 변수로 value가 들어와야한다.</li>
  <li>함수에 전달된 값을 사용하여 새 노드를 만든다.</li>
  <li>목록에 노드가 없으면 head와 tail을 추가할 노드로 설정한다.</li>
  <li>목록에 노드가 있으면
    <ol>
      <li>기존 head의 이전 포인터를 추가할 노드로 설정한다.</li>
      <li>추가할 노드의 다음 포인터를 기존의 head로 설정한다.</li>
      <li>목록의 head 속성을 새 노드로 설정한다.</li>
    </ol>
  </li>
  <li>목록의 길이를 1만큼 늘린다.</li>
  <li>연결 리스트를 반환한다.</li>
</ol>

### get
* 연결 목록에서 얻고자 하는 위치의 노드를 검색해주는 메서드

```javascript
class doublyLinkedList {
  constroctor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
  get(index) {
    if(index < 0 || index >= this.length) return null; // index가 0보다 작거나 목록의 길이보다 크거나 같으면
    let current;
    if(index <= this.length / 2) { // index가 리스트 길이의 반보다 크거나 같을 때
      current = this.head; // head부터 시작해서 순회
      for(let j = 0; j < index; j++) { // index와 같아지기 전까지 순회
        current = current.next; // index-1 번째 노드의 next가 얻고자 하는 노드
      }
    } else { // index가 리스트 길이의 반보다 작을 때
      current = this.tail; // tail부터 시작해서 순회
      for(let j = this.length - 1; j > index; j--) { // index와 같아지기 전까지 순회
        current = current.prev; // index+1 번째 노드의 prev가 얻고자 하는 노드
      }
    }
    return current; // 얻고자 하는 노드의 값을 반환
  }
}

const list = new doublyLinkedList();
list.get(2);
```
1. 매개 변수로 index가 들어와야 한다.
1. index가 0보다 작거나 목록의 길이보다 크거나 같으면 null을 반환한다.
1. index에 도달할 때까지 목록을 순회하고 해당 특정 index의 노드를 반환한다.
<ol>
  <li>매개 변수로 index가 들어와야한다.</li>
  <li>index가 0보다 작거나 목록의 길이보다 크거나 같으면 null을 반환한다.</li>
  <li>index가 리스트 길이의 반보다 크거나 같을 때
    <ol>
      <li>head부터 시작하여 next로 순회한다.</li>
      <li>0부터 index-1까지 순회하고 그때 저장된 노드의 next가 얻고자 하는 노드이다.</li>
    </ol>
  </li>
  <li>index가 리스트 길이의 작을 때
    <ol>
      <li>tail부터 시작하여 prev로 순회한다.</li>
      <li>목록의 길이-1 부터 index+1까지 순회하고 그때 저장된 노드의 prev가 얻고자 하는 노드이다.</li>
    </ol>
  </li>
  <li>연결 리스트를 반환한다.</li>
</ol>

### set
* 연결 목록에서 위치에 해당하는 노드 값을 변경해주는 메서드

```javascript
class doublyLinkedList {
  constroctor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
  set(index, val) {
    const foundNode = this.get(index); // 바꾸고자 하는 노드를 찾아온다.
    if(!foundNode) return false;  // 바꾸고자 하는 노드가 없을 때 
    foundNode.val = val; // 찾은 요소를 새로운 값으로 변경
    return true;
  }
}

const list = new doublyLinkedList();
list.set(2, "HELLO");
```
1. 매개 변수로 index와 value가 들어와야 한다.
1. 우선 get 함수를 사용하여 특정 노드를 찾는다.
1. 노드를 찾을 수 없으면 false를 반환한다.
1. 노드를 찾으면 해당 노드의 값을 함수에 전달된 값으로 설정하고 true를 반환한다.

### insert
* 연결리스트의 특정 위치에 노드를 추가해주는 매서드

```javascript
class Node{
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

class doublyLinkedList {
  constroctor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
  insert(index, val) {
    if(index < 0 || index > this.length) return false; // index가 0보다 작거나 목록의 길이보다 클 때
    if(index === this.length) return !!this.push(val); // index가 목록의 길이와 같을 때
    if(index === 0) return !!this.unshift(val); // index가 0일 때
    // !!(이중 부정): !!"Hi" => !!truthy => !false => true
    const newNode = new Node(val); // 새로 추가할 노드
    const beforeNode = this.get(index - 1); // 추가할 위치의 이전 노드
    const afterNode = beforeNode.next; // 추가할 위치의 기존 노드
    beforeNode.next = newNode; // 이전 노드의 next를 추가할 노드로 변경
    newNode.prev = beforeNode; // 추가할 노드의 prev를 이전 노드로 변경
    newNode.next = afterNode; // 추가할 노드의 next를 기존 노드로 변경
    afterNode.prev = newNode; // 기존 노드의 prev를 추가할 노드로 변경
    this.length++; // 추가했으므로 갯수 +1
    return true; // 추가하였으므로 true를 반환
  }
}

const list = new doublyLinkedList();
list.insert(2, "HELLO");
```
1. 매개 변수로 index와 value가 들어와야 한다.
1. index가 0보다 작거나 목록의 길이보다 크면 false를 반환한다.
1. index가 목록의 길이와 같으면 push와 같은 기능
1. index가 0이면 unshift와 같은 기능
1. 위의 경우가 아니면 get 메서드를 사용하여 index - 1 위치의 노드에 접근하여 해당 노드의 다음 포인터를 새 노드로 설정한다.
1. 새 노드의 다음 포인터를 기존에 index 위치에 있던 노드로 설정한다.
1. 새 노드의 다음 포인터를 기존에 index 위치에 있던 노드로 설정한다.
1. 기존 index 위치의 노드 이전 포인터를 새 노드로 설정한다.
1. 목록의 길이를 1만큼 늘린다.
1. true를 반환한다.

### remove
* 연결 리스트이 특정 위치에 노드 제거해주는 매서드

```javascript
class doublyLinkedList {
  constroctor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
  remove(index) {
    if(index < 0 || index >= this.length) return undefined; // index가 0보다 작거나 길이보다 크거나 같을 때
    if(index === 0) return this.shift(); // index가 0일 때
    if(index === this.length - 1) return this.pop(); // index가 length-1 과 같을 때
    const removedNode = this.get(index); // 삭제할 노드
    const beforeNode = removedNode.prev; // 삭제할 위치의 이전 노드
    const afterNode = removedNode.next; // 삭제할 위치의 다음 노드
    beforeNode.next = afterNode; // 삭제할 위치의 이전 노드의 next를 삭제할 위치의 다음 노드로 변경
    afterNode.prev = beforeNode; // 삭제할 위치의 다음 노드의 prev를 삭제할 위치의 이전 노드로 변경
    removedNode.prev = null; // 삭제할 노드의 prev를 비었음으로 설정
    removedNode.next = null; // 삭제할 노드의 next를 비었음으로 설정
    this.length--; // 삭제하였으므로 갯수 -1
    return removedNode; // 삭제한 노드를 반환
  }
}

const list = new doublyLinkedList();
list.remove(2);
```
1. 매개 변수로 index가 들어와야 한다.
1. index가 0보다 작거나 길이보다 크거나 같으면 undefined를 반환한다.
1. index가 length-1 과 같으면 pop과 같은 기능
1. index가 0이면 shift와 같은 기능
1. 위의 경우가 아니면 get 메서드를 사용하여 index 위치의 노드에 접근한다.
1. 삭제할 노드의 이전 노드에 next를 삭제할 노드의 다음 노드로 설정한다.
1. 삭제할 노드의 다음 노드에 prev를 삭제할 노드의 이전 노드로 설정한다.
1. 삭제할 노드의 prev와 next를 null로 설정한다.
1. 목록의 길이를 1만큼 감소한다.
1. 제거된 노드의 값을 반환한다.

## 이중 연결리스트의 Big O
* 접근
  * **O(N)** 
  * 접근하고자하는 위치까지 찾아가야 한다.
* 삽입
  * **O(1)**
  * push, unshift
* 제거
  * **O(1)**
  * pop, shift, remove
* 탐색
  * **O(N)** : get, set  
  * n의 값에 따라 head 또는 tail에서 탐색하기 때문에 정확히는 O(N/2)이지만, 간단히 O(N)이다.
  * 그러나 단일 연결 리스트보다는 확실히 빠르다.