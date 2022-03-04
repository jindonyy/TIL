---
title: "<span>Leetcode</span> Linked List Cycle"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode]
date: 2022-03-05
---

## 문제 설명
[https://leetcode.com/problems/linked-list-cycle/](https://leetcode.com/problems/linked-list-cycle/)  

연결 리스트의 헤드인 헤드가 주어지면 연결 리스트에 주기가 있는지 확인합니다.  
목록에 다음 포인터를 계속 따라가며 다시 도달할 수 있는 노드가 있는 경우 연결 리스트에 주기가 있습니다.  내부적으로 pos는 tail 포인터가 연결된 노드의 인덱스를 나타내는 데 사용됩니다. pos는 매개 변수로 전달되지 않습니다.  
연결 리스트에 주기가 있는 경우 true를 반환합니다. 그렇지 않으면 거짓을 반환하십시오.

### Example 1:
Input: head = [3,2,0,-4], pos = 1  
Output: true  
Explanation: 이 연결 리스트에는 주기가 있으며, 여기서 테일은 첫 번째 노드(0-indexed)에 연결됩니다.

### Example 2:
Input: head = [1,2], pos = 0  
Output: true  
Explanation: 이 연결 리스트에는 꼬리가 0번째 노드로 연결되는 주기가 있습니다.

### Example 3:
Input: head = [1], pos = -1  
Output: false  
Explanation: 이 연결 리스트에 주기가 없습니다.
 
### Constraints:
- 목록에 있는 노드의 수는 [0, 10<sup>4</sup>] 범위에 있습니다.
- -10<sup>5</sup> <= Node.val <= 10<sup>5</sup>
- pos는 -1이거나 연결 리스트에서 유효한 인덱스입니다.

## 답안
```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */

/**
 * @param {ListNode} head
 * @return {boolean}
 */
var hasCycle = function(head) {
    if(!head) return false;

    let turtle = head, rabbit = head;
    while(rabbit && rabbit.next) {
        turtle = turtle.next;
        rabbit = rabbit.next.next;
        if(turtle === rabbit) return true;
    }

    return false;
};
```
시간복잡도: O(N)
1. 토끼와 거북이 알고리즘을 이용하여 구현  
[https://velog.io/@lacomaco/%ED%86%A0%EB%81%BC%EC%99%80-%EA%B1%B0%EB%B6%81%EC%9D%B4-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-LeetCode-142](https://velog.io/@lacomaco/%ED%86%A0%EB%81%BC%EC%99%80-%EA%B1%B0%EB%B6%81%EC%9D%B4-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-LeetCode-142)
1. turtle과 rabbit은 head부터 시작한다.
1. rabbit이 두칸씩 뛰어 더 null에 더 빨리 도착하므로 rabbit이 null이 되거나, 두 칸씩 뛰므로 null의 next는 에러가 나므로 rabbit의 next도 체크하여 while문을 순회한다.
1. turtle은 한칸씩 next, rabbit은 두칸씩 next해준다.
1. turtle과 rabbit이 만나게 되면 순환 루프이기 때문에 false를 반환해준다.
1. while문이 종료될 경우 null을 만난 경우이므로 true를 반환한다.