---
title: "<span>Leetcode</span> Move Zeroes"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode]
date: 2022-02-19
---

## 문제 설명
[https://leetcode.com/problems/move-zeroes/](https://leetcode.com/problems/move-zeroes/)  
<br>
정수 배열이 주어지면 0이 아닌 요소의 상대적 순서를 유지하면서 모든 0을 nums의 끝으로 이동합니다.  
배열의 복사본을 만들지 않고 제자리에서 이 작업을 수행해야 합니다.

### Example 1:
Input: nums = [0,1,0,3,12]  
Output: [1,3,12,0,0]

### Example 2:
Input: nums = [0]  
Output: [0]
 
### Constraints:
- 1 <= nums.length <= 10<sup>4</sup>
- -23<sup>1</sup> <= nums[i] <= 23<sup>1</sup> - 1

## 답안
```javascript
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
const moveZeroes = function(nums) {
    let swapIdx = 0;
    for(let i = 0; i < nums.length; i++) {
        if(nums[i] === 0) continue;
        [nums[swapIdx], nums[i]] = [nums[i], nums[swapIdx]];
        swapIdx++;
    }
    return nums;
};
```
시간복잡도: O(N)
1. 0이 아닌 요소가 젤 처음 0번째 인덱스에 가야하므로 swapIdx을 0으로 초기화
1. nums[i]가 0이 아닐 때, nums[swapIdx]와 nums[i]를 교체
1. 앞으로 땡겨줄 때마다 0이 아닌 요소가 배열의 앞쪽에 쌓이므로 그 다음에 0이 아닌 요소가 들어가기 위해서 swapIdx++을 해준다.