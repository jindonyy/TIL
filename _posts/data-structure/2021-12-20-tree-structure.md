---
title: "트리 구조(tree structure)"
layout: single
classes: wide
categories:
  - data structure
tags:
  - [data structure, tree structure]
date: 2021-12-20
---

## 트리 구조란?
* 나무에서 가지가 뻗는 모양이라 하여 트리 구조라 한다.
* 부모와 자식 관계의 노드로 구성된 데이터 구조이다.
<img src='{{ "/TIL/assets/images/2021-12-20-tree_1.png" | relativec_url }}' style="width:500px;" title="트리구조 설명" alt="트리구조 설명"/>
<img src='{{ "/TIL/assets/images/2021-12-20-tree_2.png" | relativec_url }}' style="width:500px;" title="트리구조 설명" alt="트리구조 설명"/>

### 트리 구조 용어
<img src='{{ "/TIL/assets/images/2021-12-20-tree_3.png" | relativec_url }}' style="width:650px;" title="트리구조 설명" alt="트리구조 설명"/>

* **Node(노드)**
  * 트리를 구성하고 있는 기본 요소  
  * 노드에는 키 또는 값과 하위 노드에 대한 포인터를 가지고 있음.
  * A, B, C, D, E, F, G, H, I, J
* **Root(뿌리)**
  * 트리의 최상위 노드
  * A
* **Parent(부모)**
  * 자식 노드를 가진 노드
  * H, I에 부모 노드는 D
* **Child(자식)**
  * 부모 노드의 하위 노드
  * 노드 D의 자식 노드는 H, I
* **Siblings(형제)**
  * 부모가 같은 노드 그룹
  * H, I는 같은 부모를 가지는 형제 노드
* **Leaf(나뭇잎)**
  * 자식이 없는 노드
  * H, I, J, F, G
* **Edge(간선)**
  * 노드와 노드 간의 연결선
  * A, B, D, H들은 edge되어 있다.  
* **Depth(깊이)**
  * 루트에서 어떤 노드까지의 간선(Edge) 수
  * 루트 노드의 깊이 : 0
  * D의 깊이 : 2
* **height(높이)**
  * 어떤 노드에서 리프 노드까지 가장 긴 경로의 간선(Edge) 수
  * 리프 노드의 높이 : 0
  * A 노드의 높이 : 3

### 트리 구조의 주의 점
* 트리 구조는 **자식 관계의 다른 노드만을** 가리켜야 한다.  
동급의 노드나 부모의 노드를 가리키면 안된다.
<img src='{{ "/TIL/assets/images/2021-12-20-tree_4.png" | relativec_url }}' style="width:500px;" title="트리구조 설명" alt="트리구조 설명"/>
위의 구조는 9와 8이 동급의 노드를 가리키므로 트리 구조가 아니다.

* **출발점(root)이 하나**여야 한다.
<img src='{{ "/TIL/assets/images/2021-12-20-tree_5.png" | relativec_url }}' style="width:500px;" title="트리구조 설명" alt="트리구조 설명"/>

### 연결 리스트와 트리 구조
* 연결 리스트는 일자로 쭉 뻗은 단방향이기 때문에 뒤 또는 앞뒤로 작업이 가능했다.  
* 그러나 트리는 갈수 있는 경로가 여러 가지이다.
* 사실 연결 리스트도 넓게 보면 가지가 하나인 트리라고도 할 수 있다.

## 트리 구조의 실제 예시
* HTML DOM  
ex) html -> head, body -> main, nav, ...
<img src='{{ "/TIL/assets/images/2021-12-20-tree_6.png" | relativec_url }}' style="width:650px;" title="트리구조 설명" alt="트리구조 설명"/>

* 네트워크 라우팅
* 추상 구문 트리  
ex) while
<img src='{{ "/TIL/assets/images/2021-12-20-tree_7.png" | relativec_url }}' style="width:600px;" title="트리구조 설명" alt="트리구조 설명"/>
ex) JSON
<img src='{{ "/TIL/assets/images/2021-12-20-tree_8.png" | relativec_url }}' style="width:400px;" title="트리구조 설명" alt="트리구조 설명"/>

* 인공 지능
* Heap(힙)  
  \- 힙도 트리로 된 자료 구조이다.
* 운영 체제의 폴더
ex) 폴더 구조 및 경로
<img src='{{ "/TIL/assets/images/2021-12-20-tree_9.png" | relativec_url }}' style="width:350px;" title="트리구조 설명" alt="트리구조 설명"/>
* 컴퓨터 파일 시스템

## 트리 구조의 종류
* 트리(Trees)
* 이진 트리(Binary Trees)
* 이진 탐색 트리(Binary Search Trees
* 등등 아주 많지만 위의 3가지가 대표적