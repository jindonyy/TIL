---
title: "<span>Leetcode</span> 268. Missing Number"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode]
date: 2022-03-26
---

## 문제 설명

[https://leetcode.com/problems/missing-number/](https://leetcode.com/problems/missing-number/)

[0, n] 범위의 n개의 고유 번호가 포함된 배열 번호를 지정하면 배열에서 누락된 유일한 번호를 반환합니다.

### Example 1:

Input: nums = [3,0,1]  
Output: 2  
Explanation: 3개의 숫자가 있기 때문에 n = 3이므로, 모든 숫자는 [0,3] 범위에 있습니다. 2는 수치로 표시되지 않기 때문에 범위 내에서 누락된 번호입니다.

### Example 2:

Input: nums = [0,1]  
Output: 2  
Explanation: 2개의 숫자가 있기 때문에 n = 2이므로 모든 숫자는 [0,2] 범위에 있습니다. 2는 수치로 표시되지 않기 때문에 범위 내에서 누락된 번호입니다.

### Example 3:

Input: nums = [9,6,4,2,3,5,7,0,1]  
Output: 8  
Explanation: 9개의 숫자가 있기 때문에 n = 9이므로, 모든 숫자는 [0,9] 범위에 있습니다. 8은 수치로 표시되지 않기 때문에 범위 내에서 누락된 숫자입니다.

### Constraints:

- n == nums.length
- 1 <= n <= 104
- 0 <= nums[i] <= n
- 모든 숫자는 한결같습니다.

## 답안

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
const missingNumber = function (nums) {
  let total = nums.length;
  const sum = nums.reduce((acc, cur, idx) => {
    total += idx;
    return (acc += cur);
  });
  return total - sum;
};
```

시간복잡도: O(N)

1. 0 ~ n까지 전부 더한 숫자에서 nums의 전부 더한 값을 뺴주면 없는 요소를 찾을 수 있다.
