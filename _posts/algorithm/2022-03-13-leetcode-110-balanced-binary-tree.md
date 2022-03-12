---
title: "<span>Leetcode</span> 110. Balanced Binary Tree"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode]
date: 2022-03-13
---

## 문제 설명

[https://leetcode.com/problems/balanced-binary-tree/](https://leetcode.com/problems/balanced-binary-tree/)

이진 트리가 주어지면 높이 균형이 맞는지 확인합니다.  
이 문제의 경우 높이 균형 이진 트리는 다음과 같이 정의됩니다.  
각 노드의 왼쪽 및 오른쪽 하위 트리가 높이가 1 이하인 이진 트리.

### Example 1:

![example 1](https://assets.leetcode.com/uploads/2020/10/06/balance_1.jpg)
Input: root = [3,9,20,null,null,15,7]  
Output: true

### Example 2:

![example 2](https://assets.leetcode.com/uploads/2020/10/06/balance_2.jpg)
Input: root = [1,2,2,3,3,null,null,4,4]  
Output: false

### Example 3:

Input: root = []  
Output: true

### Constraints:

- The number of nodes in the tree is in the range [0, 5000].
- -10<sup>4</sup> <= Node.val <= 10<sup>4</sup>

## 답안

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {boolean}
 */
const getSideDepth = function (root) {
  if (!root) return 0;

  const leftDepth = getSideDepth(root.left);
  const rightDepth = getSideDepth(root.right);
  if (leftDepth === false || rightDepth === false) return false;
  return Math.abs(leftDepth - rightDepth) <= 1
    ? Math.max(leftDepth, rightDepth) + 1
    : false;
};

const isBalanced = function (root) {
  if (!root) return true;

  return getSideDepth(root) ? true : false;
};
```

시간복잡도: O(N)

1. root.left와 root.right로 재귀를 타고 들어간다.
1. root가 비었을 시 0을 반환하게 하여 젤 안쪽 재귀를 종료 시킨다.
1. 제일 안쪽의 node에 들어갔을 시, leftDepth와 rightDepth는 각각 0으로 반환된다. 그럼 두 depth를 비교하여 반환값을 정한다.

- 두개의 depth의 차가 1이하 일때는 두 dpeth 중 큰 숫자를 비교하여 1증가하여 반환한다.
- 두개의 depth의 차가 1초과 일때는 false를 반환한다.

1. 하나가 false일 경우 최종 반환값은 false여야 하므로, leftDepth와 rightDepth 둘 중 하나 이상이 false일 경우 계속 false를 반환한다.
1. getSideDepth 함수에서 반환된 값이 false냐 숫자(truethy)에 따라 true 또는 false를 반환한다.
