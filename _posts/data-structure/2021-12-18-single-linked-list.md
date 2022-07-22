---
title: "단일 연결 리스트(single linked list)"
header:
  teaser: /assets/images/data-structure/2021-12-18-linked-list_teaser.png
layout: single
classes: wide
categories:
  - data structure
tags:
  - [data structure, single linked list, linked list]
date: 2021-12-18
---

## 단일 연결 리스트란?

- 데이터 요소를 선형적으로 연걸한 것이다.
- 머리(head)와 꼬리(tail), 길이 특성을 포함하는 데이터 구조이다.
- node로 구성되며, 각 node에는 value가 있고 다음 node 또는 null에 대한 포인터가 있다.
  <img src='{{ "/assets/images/data-structure/2021-12-18-single-linked-list_1.png" | relative_url }}' style="width:500px;" title="기수 정렬 설명" alt="기수 정렬 설명"/>

## 배열과의 차이점

### 연결 리스트

- index가 없다.
- 노드들이 다음 노드를 가리키는 포인터를 통해 연결된다.
- 특정 위치의 노드에 접근할 수 없다.  
  리스트 안의 항목을 순차적으로 접근해야하기 때문에 특정 위치의 리스트에 접근하거나 이전 리스트로 돌아가려면 전체 목록을 처음부터 다시 순서대로 읽어야 한다.
- 배열과 달리 요소를 추가할 때 재 할당하거나 재구성하지 않아도 된다.  
  때문에 목록의 특정 지점에 **요소를 추가하거나 요소를 제거할 때 유리하다.**
- 다만 포인터로 다음 연결 리스트를 지정해야하기 때문에 배열보다 더 많은 메모리를 사용하는 단점이 있다.

### 배열

- 삽입한 순서대로 나열된다.
- 삽입 및 삭제의 위치에 따라 시간이 많이 소요될 수 있다.
- 특정 index에 빠르게 전급할 수 있다.

## 단일 연결 리스트를 구현하기 위해 필요한 메서드

### push

- 연결 목록 끝에 새로운 노드 추가해주는 메서드

```javascript
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

class SingleLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  push(val) {
    const newNode = new Node(val); // 새로 추가할 노드
    if (this.head) {
      // 기존에 노드가 있으면
      this.tail.next = newNode; // 기존의 tail의 next를 추가할 노드로
      this.tail = newNode; // 추가한 노드가 새로운 tail이 된다.
    } else {
      // 기존에 노드가 없으면
      this.head = newNode; // 추가한 노드가 head이자
      this.tail = this.head; // tail이다.
    }
    this.length++; // 추가했으므로 갯수 +1
    return this; // 연결 리스트를 반환
  }
}

const list = new SinglyLinkedList();
list.push("HELLO");
```

1. 매개 변수로 value가 들어와야한다.
1. 함수에 전달된 값을 사용하여 새 노드를 만든다.
1. 목록에 head 속성이 있으면 tail의 다음 포인터를 새 노드로 설정하한다.
1. 목록의 tail 속성을 새로 생성된 노드로 설정한다.
1. 목록에 head 속성이 없으면 head와 tail을 새로 생성된 노드로 설정한다.
1. 목록의 길이를 1만큼 늘린다.
1. 연결 리스트를 반환한다.

### pop

- 연결 목록의 끝에서 노드 제거해주는 메서드

```javascript
class SingleLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
  pop() {
    if (!this.head) return undefined; // 리스트가 비었을 시
    let current = this.head; // head부터 시작해서 순회하기 위해 초기 설정
    let newTail = current; // 새로운 tail로 등록될 노드
    // 연결 리스트의 맨 끝요소는 next가 null이므로
    while (current.next) {
      newTail = current; // tail에 도착했을 때는 재할당 되지 않으므로 tail의 앞 노드가 저장
      current = current.next; // 그 다음 노드로 순회하기 위해
    }
    this.tail = newTail; // tail의 앞 노드가 새로운 tail
    this.tail.next = null; // 맨 끝의 노드를 삭제
    this.length--; // 삭제했으므로 갯수 -1
    if (this.length === 0) {
      // 노드가 하나인데 삭제했을 경우
      this.head = null; // head가 비었다 표시
      this.tail = null; // tail이 비었다 표시
    }
    return current; // 삭제한 노드를 반환
  }
}

const list = new SinglyLinkedList();
list.pop();
```

1. 목록에 노드가 없으면 undefined를 반환한다.
1. 꼬리에 도달할 때까지 목록을 순회한다.
1. 마지막 노드(tail)의 이전 노드(뒤에서 두 번째)의 다음 포인터를 null로 설정한다.
1. 꼬리를 마지막 노드의 이전 노드로 설정한다.
1. 목록의 길이를 1만큼 감소한다.
1. 제거된 노드의 값을 반환한다.

### shift

- 연결 목록의 시작 부분(head) 노드를 제거해주는 메서드

```javascript
class SingleLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  shift() {
    if (!this.head) return undefined; // 리스트가 비었을 시
    const oldHead = this.head; // 현재 head를 저장
    this.head = oldHead.next; // 현재 head의 다음 노드를 head로 변경
    this.length--; // 삭제했으므로 갯수 -1
    if (this.length === 0) {
      // 노드가 하나인데 삭제했을 경우
      this.tail = null; // tail이 비었다 표시
    }
    return oldHead; // 삭제한 노드를 반환
  }
}

const list = new SinglyLinkedList();
list.shift();
```

1. 목록에 노드가 없으면 undefined를 반환한다.
1. 현재 head 속성에 값을 변수에 저장
1. head 속성을 현재 head의 다음 노드로 설정
1. 목록의 길이를 1만큼 감소한다.
1. 제거된 노드의 값을 반환한다.

### unshift

- 연결 목록의 시작 부분에 새로운 노드 추가해주는 메서드

```javascript
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

class SingleLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
  unshift(val) {
    const newNode = new Node(val); // 새로 추가할 노드
    if (!this.head) {
      // 기존에 노드가 있으면
      newNode.next = this.head; // 추가할 노드의 next를 현재 head로 지정
      this.head = newNode; // 추가된 노드가 새로운 head가 된다.
    } else {
      // 기존에 노드가 없으면
      this.head = newNode; // 추가할 노드를 head와
      this.tail = this.head; // tail로 지정
    }
    this.length++; // 추가했으므로 갯수 +1
    return this; // 연결 리스트를 반환
  }
}

const list = new SinglyLinkedList();
list.unshift("HELLO");
```

1. 매개 변수로 value가 들어와야한다.
1. 함수에 전달된 값을 사용하여 새 노드를 만든다.
1. 목록에 head 속성이 있으면 새 노드의 다음 포인터를 현재 head였던 노드로 설정한다.
1. 목록의 head 속성을 새로 추가한 노드로 설정한다.
1. 목록에 head 속성이 없으면 head와 tail을 새로 생성된 노드로 설정한다.
1. 목록의 길이를 1만큼 늘린다.
1. 연결 리스트를 반환한다.

### get

- 연결 목록에서 찾고자 하는 위치의 노드를 검색해주는 메서드

```javascript
class SingleLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
  get(index) {
    if (index < 0 || index >= this.length) return null; // index가 0보다 작거나 목록의 길이보다 크거나 같으면
    let current = this.head; // 순회할 때 현재 노드
    for (let j = 0; j < index; j++) {
      // for문의 j와 index가 같아질 때까지
      current = current.next; // 현재 노드를 다음 노드로 업데이트
    }
    return current; // 얻고자 하는 노드의 값을 반환
  }
}

const list = new SinglyLinkedList();
list.get(2);
```

1. 매개 변수로 index가 들어와야 한다.
1. index가 0보다 작거나 목록의 길이보다 크거나 같으면 null을 반환한다.
1. index에 도달할 때까지 목록을 순회하고 해당 특정 index의 노드를 반환한다.

### set

- 연결 목록에서 위치에 해당하는 노드 값을 변경해주는 메서드

```javascript
class SingleLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
  set(index, val) {
    const foundNode = this.get(index, val); // 바꾸고자 하는 노드를 찾아온다.
    if (!foundNode) return false; // 바꾸고자 하는 노드가 없을 때
    foundNode.val = val; // 찾은 요소를 새로운 값으로 변경
    return true;
  }
}

const list = new SinglyLinkedList();
list.set(2, "HELLO");
```

1. 매개 변수로 index와 value가 들어와야 한다.
1. 우선 get 함수를 사용하여 특정 노드를 찾는다.
1. 노드를 찾을 수 없으면 false를 반환한다.
1. 노드를 찾으면 해당 노드의 값을 함수에 전달된 값으로 설정하고 true를 반환한다.

### insert

- 연결리스트의 특정 위치에 노드를 추가해주는 매서드

```javascript
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

class SingleLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
  insert(index, val) {
    if (index < 0 || index > this.length) return false; // index가 0보다 작거나 목록의 길이보다 클 때
    if (index === this.length) return !!this.push(val); // index가 목록의 길이와 같을 때
    if (index === 0) return !!this.unshift(val); // index가 0일 때
    // !!(이중 부정): !!"Hi" => !!truthy => !false => true
    const newNode = new Node(val); // 새로 추가할 노드
    const beforeNode = this.get(index - 1); // 추가할 위치의 이전 노드
    const afterNode = beforeNode.next; // 추가할 위치의 기존 노드
    beforeNode.next = newNode; // 이전 노드의 next를 추가할 노드로 변경
    newNode.next = afterNode; // 추가할 노드의 next를 기존 노드로 변경
    this.length++; // 추가했으므로 갯수 +1
    return true; // 추가하였으므로 true를 반환
  }
}

const list = new SinglyLinkedList();
list.insert(2, "HELLO");
```

1. 매개 변수로 index와 value가 들어와야 한다.
1. index가 0보다 작거나 목록의 길이보다 크면 false를 반환한다.
1. index가 목록의 길이와 같으면 push와 같은 기능
1. index가 0이면 unshift와 같은 기능
1. 위의 경우가 아니면 get 메서드를 사용하여 index - 1 위치의 노드에 접근하여 해당 노드의 다음 포인터를 새 노드로 설정한다.
1. 새 노드의 다음 포인터를 기존에 index 위치에 있던 노드로 설정한다.
1. 목록의 길이를 1만큼 늘린다.
1. true를 반환한다.

### remove

- 연결 리스트이 특정 위치에 노드 제거해주는 매서드

```javascript
class SingleLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
  remove(index) {
    if (index < 0 || index >= this.length) return undefined; // index가 0보다 작거나 길이보다 크거나 같을 때
    if (index === 0) return this.shift(); // index가 0일 때
    if (index === this.length - 1) return this.pop(); // index가 length-1 과 같을 때
    const beforeNode = this.get(index - 1); // 삭제할 위치의 이전 노드
    const removedNode = beforeNode.next; // 삭제할 노드
    beforeNode.next = removedNode.next; // 이전 노드의 next를 삭제할 노드의 다음 노드로 변경
    this.length--; // 삭제하였으므로 갯수 -1
    return removedNode; // 삭제한 노드를 반환
  }
}

const list = new SinglyLinkedList();
list.remove(2);
```

1. 매개 변수로 index가 들어와야 한다.
1. index가 0보다 작거나 길이보다 크거나 같으면 undefined를 반환한다.
1. index가 length-1 과 같으면 pop과 같은 기능
1. index가 0이면 shift와 같은 기능
1. 위의 경우가 아니면 get 메서드를 사용하여 index - 1 위치의 노드에 접근하여 해당 노드의 다음 포인터를 삭제하려는 노드의 다음 포인터로 설정한다.
1. 목록의 길이를 1만큼 감소한다.
1. 제거된 노드의 값을 반환한다.

### reverse

- 연결 리스트의 순서를 반전시켜주는 메서드

```javascript
class SingleLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
  reverse() {
    let current = this.head; // 순회하면서 바꿔줄 노드, head부터 시작해야하므로 초기값 head로 저장
    let next; // 현재 노드의 다음 노드
    let prev = null; // 현재 노드의 이전 노드
    this.head = this.tail; // head를 tail로 변경
    this.tail = current; // tail을 head로 변경
    for (let i = 0; i < this.length; i++) {
      next = current.next; // 현재 노드의 next를 저장
      current.next = prev; // 현재 노드의 next를 이전 요소로 변경
      prev = current; // 다음 순회를 위해 이전 노드를 현재 노드로 변경
      current = next; // 다음 순회를 위해 현재 노드를 다음 노드로 변경
    }
    return this; // 연결 리스트를 반환
  }
}

const list = new SinglyLinkedList();
list.reverse();
```

<ol>
  <li>current라는 변수를 생성하고 head 속성으로 초기화한다.</li>
  <li>next와 prev라는 변수를 생성한다.</li>
  <li>머리와 꼬리를 바꾼다.</li>
  <li>목록을 순회하며 반복한다.
    <ol>
      <li>next에 현재 노드의 다음은 노드를 저장한다.</li>
      <li>현재 노드의 다음 포인터를 이전 노드로 설정한다.</li>
      <li>prev에 현재 노드를 저장한다.</li>
      <li>current에 이전에 저장해둔 next를 저장한다.<br>
      (2번에서 다음 포인터를 이전 노드로 바꿔줬으므로 바꿔주기 전에 저장해놓은 next를 사용)</li>
    </ol>
  </li>
  <li>연결 리스트를 반환한다.</li>
</ol>

## 단일 연결 리스트의 Big O

- 접근
  - **O(N)** : get, set  
    \- 접근하고자 하는 위치까지 찾아가야 한다.
- 삽입
  - **O(1)** : push, unshift
- 제거
  - **O(1)** : shift
  - **O(N)** : pop, remove  
    \- 삭제하려는 위치까지 접근해서 삭제해야한다.
- 탐색
  - **O(N)**
    \- 탐색하고자 하는 위치까지 찾아가야 한다.

## 결론

단일 연결 리스트는 삽입과 삭제하는 부분에서는 배열보다 앞선다!
