---
title: "<span>Leetcode</span> 217. Contains Duplicate"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode]
date: 2022-03-14
---

## 문제 설명

[https://leetcode.com/problems/contains-duplicate/](https://leetcode.com/problems/contains-duplicate/)

정수 배열 num이 지정되면 배열에 값이 두 번 이상 나타나면 true를 반환하고 모든 요소가 고유한 경우 false를 반환합니다.

### Example 1:

Input: nums = [1,2,3,1]  
Output: true

### Example 2:

Input: nums = [1,2,3,4]  
Output: false

### Example 3:

Input: nums = [1,1,1,3,3,4,3,2,4,2]  
Output: true

### Constraints:

- 1 <= nums.length <= 10<sup>5</sup>
- -10<sup>9</sup> <= nums[i] <= 10<sup>9</sup>

## 답안

```javascript
/**
 * @param {number[]} nums
 * @return {boolean}
 */
const containsDuplicate = function (nums) {
  return new Set([...nums]).size < nums.length ? true : false;
};
```

중복이 있는지 없는지에 따라 반환값이 결정되므로 Set을 이용하여 중복을 제거하고 원본 배열과 개수를 비교한다.
