---
title: "<span>Leetcode</span> search insert position"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode, Birnary search]
date: 2022-02-12
---

## 문제 설명
[https://leetcode.com/problems/search-insert-position/](https://leetcode.com/problems/search-insert-position/)  
<br>
정렬된 배열의 고유 정수와 대상 값이 지정되면 대상이 있는 경우 인덱스를 반환합니다. 그렇지 않다면 인덱스를 순서대로 삽입했을 때의 위치에 다시 넣습니다.  
O(log n) 런타임 복잡성을 가진 알고리즘을 작성해야 합니다.

### Example 1:
Input: nums = [1,3,5,6], target = 5  
Output: 2

### Example 2:
Input: nums = [1,3,5,6], target = 2  
Output: 1

### Example 3:
Input: nums = [1,3,5,6], target = 7  
Output: 4
 
### Constraints:
- 1 <= nums.length <= 104
- -104 <= nums[i] <= 104
- nums contains distinct values sorted in ascending order.
- -104 <= target <= 104

## 답안
```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
*/
const searchInsert = function(nums, target) {
    let start = 0;
    let end = nums.length -1;
    let middle = Math.floor((start + end) / 2);
    
    while(target !== nums[middle] && start < end) {
        if(target < nums[middle]) end = middle;
        else start = middle + 1;
        middle = Math.floor((start + end) / 2);
    }
    
    return target <= nums[middle] ? middle : middle + 1;
};
```
1. 이진 탐색을 위해 시작, 끝, 중간 지점을 지정한다.
1. target이 middle과 같아지면 middle을 반환해야 하므로 while문 종료한다.  
start가 end보다 커지면 안되므로 이 경우에도 while문 종료한다.
1. while문이 종료된 뒤, 값 반환
    - `target < nums[middle]` => middle 인덱스에 target이 삽입해야 하므로 middle 반환
    - `target === nums[middle]` => middle 인덱스에 target이 들어있으므로 middle 반환
    - `target > nums[middle]` => middle 다음 인덱스에 target이 추가되야 하므로 middle 반환