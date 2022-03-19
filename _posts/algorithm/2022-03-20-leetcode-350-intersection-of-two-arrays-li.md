---
title: "<span>Leetcode</span> 350. Intersection of Two Arrays II"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode]
date: 2022-03-20
---

## 문제 설명

[https://leetcode.com/problems/intersection-of-two-arrays-ii/](https://leetcode.com/problems/intersection-of-two-arrays-ii/)

2개의 정수 배열 num1과 num2를 지정하면 각각의 교차 배열을 반환합니다. 결과의 각 요소는 양쪽 어레이에 표시된 횟수만큼 표시되어야 하며 결과를 임의의 순서로 반환할 수 있습니다.

### Example 1:

Input: nums1 = [1,2,2,1], nums2 = [2,2]  
Output: [2,2]

### Example 2:

Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]  
Output: [4,9]  
Explanation: [9,4] is also accepted.

### Constraints:

- 1 <= nums1.length, nums2.length <= 1000
- 0 <= nums1[i], nums2[i] <= 1000

### Follow up:

- 지정된 배열이 이미 정렬되어 있으면 어떻게 됩니까? 알고리즘을 어떻게 최적화하시겠습니까?
- num1의 사이즈가 num2의 사이즈에 비해 작으면 어떻게 됩니까? 어떤 알고리즘이 더 나을까요?
- num2의 요소가 디스크에 저장되어 있고 메모리가 제한되어 있어 한 번에 모든 요소를 메모리에 로드할 수 없는 경우에는 어떻게 해야 합니까?

## 답안

```javascript
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
const intersect = function (nums1, nums2) {
  const sortNums1 = nums1.sort((a, b) => a - b);
  const sortNums2 = nums2.sort((a, b) => a - b);
  let pointer = 0;
  return sortNums1.filter((num1) => {
    for (let idx = pointer; idx < sortNums2.length; idx++) {
      const num2 = sortNums2[idx];
      if (num1 == num2) {
        pointer = idx + 1;
        return true;
      }
    }
  });
};
```

시간복잡도: O(n log n)

1. 같은 수끼리 모여있도록 정렬하기 위해 sort를 써서 nums1과 nums2를 정렬한다.
1. pointer를 이용하여 sortNums1의 num1이 sortNums2의 num2와 같은 인덱스를 찾는다.
1. 같은 숫자를 찾았으면 그 숫자를 담아야하므로 true를 반환해주고, 그 다음 num1은 이 앞의 숫자들을 다시 보면 안되므로(sortNums1에 같은 숫자가 2개고 해당 숫자를 sortNums2가 1개만 가진 경우 sortNums1에서 같은 숫자인지 한번만 체크해야하므로, 뒤의 같은 숫자가 또 체크하지 못하게 시작점(pointer)를 옮겨준다.

```
// 에시
sortNums1 = [1, 1, 1, 2, 2, 3, 4];
sortNums2 = [1, 1, 2, 4, 5];
```

- num1 = 1 => pointer = 0, nums2 = 1(0번 쨰)부터 시작하여 idx가 0일 때, pointer를 1로 변경, true 반환
- num1 = 1 => pointer = 1, nums2 = 1(1번 째)부터 시작하여 idx가 1일 때, pointer를 2로 변경, true 반환
- num1 = 1 => pointer = 2, nums2 = 2부터 시작하여 idx가 끝날 때까지 같은 숫자를 찾지 못하여 pointer는 그대로, undefined(falsy)를 반환
- num1 = 2 => pointer = 2, nums2 = 2부터 시작하여 idx가 2일 때, pointer를 3로 변경, true 반환
- num1 = 2 => pointer = 3, nums2 = 4부터 시작하여 idx가 끝날 때까지 같은 숫자를 찾지 못하여 pointer는 그대로, undefined(falsy)를 반환
- num1 = 3 => pointer = 3, nums2 = 4부터 시작하여 idx가 끝날 때까지 같은 숫자를 찾지 못하여 pointer는 그대로, undefined(falsy)를 반환
- num1 = 4 => pointer = 3, nums2 = 4부터 시작하여 idx가 3일 때, pointer를 4로 변경, true 반환
- filter문 종료, true를 반환했던 [1, 1, 2, 4]를 반환

이중배열을 two pointer처럼 사용하여 filter문은 O(N)이다.
