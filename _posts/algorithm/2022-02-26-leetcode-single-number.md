---
title: "<span>Leetcode</span> Single Number"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode]
date: 2022-02-26
---

## 문제 설명
[https://leetcode.com/problems/single-number/](https://leetcode.com/problems/single-number/)  
<br>
문자열 `s`가 주어지면 공백과 초기 단어 순서를 유지하면서 문장 내 각 단어의 문자 순서를 반대로 합니다.

### Example 1:
Input: nums = [2,2,1]  
Output: 1

### Example 2:
Input: nums = [4,1,2,1,2]  
Output: 4

### Example 3:
Input: nums = [1]  
Output: 1
 
### Constraints:
- 1 <= nums.length <= 3 * 10<sup>4</sup>
- -3 * 10<sup>4</sup> <= nums[i] <= 3 * 10<sup>4</sup>
- Each element in the array appears twice except for one element which appears only once.

## 답안
```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function(nums) {
    if(nums.length === 1) return nums[0];

    const sortArr = nums.sort((a, b) => a - b);
    for(let idx = 0; idx < sortArr.length - 1; idx += 2) {
        if(sortArr[idx] !== sortArr[idx + 1]) return sortArr[idx];
    }

    return sortArr[sortArr.length - 1];
};
```
시간복잡도: O(N)
1. nums의 숫자가 한개일 경우 항상 첫번째 인덱스의 값이 single number이다.
1. sort를 이용해 오름차순으로 정렬한다.
1. for문을 돌려 현재 인덱스의 값과 다음 인덱스의 값을 비교하여 다를 경우 해당 인덱스의 값을 반환한다.
1. 2개의 같은 수를 가진 경우는 비교할 필요가 없으므로 for문의 idx는 2씩 증가하고,  
마지막 인덱스의 다음 값은 없으므로 sortArr.length - 1 까지 루프한다.
1. for문이 끝나도 반환되는 값이 없으면 마지막 인덱스의 값이 single number이므로  
마지막 인덱스의 값을 반환한다.