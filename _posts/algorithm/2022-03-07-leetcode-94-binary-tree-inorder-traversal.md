---
title: "<span>Leetcode</span> 94. Binary Tree Inorder Traversal"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode]
date: 2022-03-07
---

## 문제 설명
[https://leetcode.com/problems/binary-tree-inorder-traversal/](https://leetcode.com/problems/binary-tree-inorder-traversal/)  

이진 트리의 루트가 지정되면 노드 값의 중위 순서를 반환합니다.  
[중위 순회 참고](https://yenny-zzang.tistory.com/76)

### Example 1:
Input: root = [1,null,2,3]  
Output: [1,3,2]  

### Example 2:
Input: root = []  
Output: []

### Example 3:
Input: root = [1]  
Output: [1]
 
### Constraints:
- The number of nodes in the tree is in the range [0, 100].
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
 * @return {number[]}
 */
var inorderTraversal = function(root) {
  if(!root) return [];
  
  const leftArr = inorderTraversal(root.left);
  leftArr.push(root.val);
  const rightArr = inorderTraversal(root.right);
  return [...leftArr, ...rightArr];
};
```
시간복잡도: O(N)
1. 중위 순회를 하기 위해 root.left로 재귀를 돌려 left의 left로 타고 들어간다.
1. 그러다 젤 left 자식을 만나면 return 해야하므로 루트 값이 없을 때(!root) 빈 배열을 반환해주는 조건문을 건다.
1. 반환된 빈 배열에는 left 자식들의 값을 저장할 배열로 사용하기 위해 저장하고, left.left..left의 root를 leftArr에 담아준다.
1. 그 다음 left.left..right의 자식을 또 재귀 돌려 빈 노드를 만나면 빈 배열이 반환되면서 right 자식들의 값이 배열에 담긴다.
1. 해당 루트가 반복되면서 젤 상위 root로 왔다가 right.left..left로 파고 들어간다.
1. 최종적으로 상위 root와 상위 root의 left 자식들을 담은 leftArr과 상위 root의 right 자식들을 담은 rigthArr이 하나로 합쳐져 반환된다.