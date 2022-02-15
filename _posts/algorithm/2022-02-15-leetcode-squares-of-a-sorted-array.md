---
title: "<span>Leetcode</span> Squares of a Sorted Array"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode, Birnary search]
date: 2022-02-15
---

## 문제 설명
[https://leetcode.com/problems/squares-of-a-sorted-array/](https://leetcode.com/problems/squares-of-a-sorted-array/)  
<br>
내림차순으로 정렬된 정수 배열 `nums`가 주어지면 내림차순 으로 정렬된 각 숫자의 제곱 배열을 반환합니다 .

### Example 1:
Input: nums = [-4,-1,0,3,10]  
Output: [0,1,9,16,100]  
Explanation: After squaring, the array becomes [16,1,0,9,100].  
After sorting, it becomes [0,1,9,16,100].

### Example 2:
Input: nums = [-7,-3,2,3,11]  
Output: [4,9,9,49,121]
 
### Constraints:
- 1 <= nums.length <= 10<sup>4</sup>
- -104 <= nums[i] <= 10<sup>4</sup>
- nums is sorted in non-decreasing order.

## 답안
```javascript
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var sortedSquares = function(nums) {
    return nums.map(num => num**2).sort((a, b) => a - b);
};
```
너무 쉽게 통과되서 퀵정렬 사용하여 다시 풀어볼 예정