---
title: "<span>Leetcode</span> 104. Maximum Depth of Binary Tree"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode]
date: 2022-03-09
---

## 문제 설명

[https://leetcode.com/problems/maximum-depth-of-binary-tree/](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

이진 트리의 루트가 지정되면 최대 깊이를 반환합니다.  
이진 트리의 최대 깊이는 루트 노드에서 가장 먼 리프 노드까지 가장 긴 경로를 따라 있는 노드의 수입니다.

### Example 1:

Input: root = [3,9,20,null,null,15,7]  
Output: 3

### Example 2:

Input: root = [1,null,2]  
Output: 2

### Constraints:

- The number of nodes in the tree is in the range [0, 10<sup>4</sup>].
- -100 <= Node.val <= 100

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
 * @return {number}
 */
const maxDepth = function (root) {
  if (!root) return 0;

  const leftDepth = maxDepth(root.left) + 1;
  const rightDepth = maxDepth(root.right) + 1;
  return leftDepth > rightDepth ? leftDepth : rightDepth;
};
```

시간복잡도: O(N)

1. root.left와 root.right를 매개변수로 maxDepth 함수를 재귀로 들어간다.
1. root가 더 이상 없어질 때 제일 자식 노드 밑이므로 0을 반환한다.
1. 재귀가 탈출할 때마다 1씩 더해준다.
1. 최종으로 나온 leftDepth, rightDepth 중에 큰 값을 반환한다.
