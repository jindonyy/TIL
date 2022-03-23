---
title: "<span>Leetcode</span> 326. Power of Three"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode]
date: 2022-03-24
---

## 문제 설명

[https://leetcode.com/problems/power-of-three/](https://leetcode.com/problems/power-of-three/)

정수 n을 지정하면 3의 거듭제곱이면 true를 반환합니다. 그렇지 않으면 false를 반환합니다.  
정수 n은 n == 3<sup>x</sup>인 정수 x가 존재하는 경우 3의 거듭제곱입니다.

### Example 1:

Input: n = 27  
Output: true

### Example 2:

Input: n = 0  
Output: false

### Example 3:

Input: n = 9  
Output: true

### Constraints:

- -2<sup>31</sup> <= n <= 2<sup>31</sup> - 1

## 답안

```javascript
/**
 * @param {number} n
 * @return {boolean}
 */
var isPowerOfThree = function (n) {
  if (n === 0) return false;
  if (n === 1) return true;

  while (true) {
    if (n === 3) return true;
    const first = Math.sqrt(n);
    if (Number.isInteger(first)) {
      // 81, 36
      if (Number.isInteger(first / 3)) n = first;
      else return false;
    } else {
      // 27, 8
      const second = Math.sqrt(n / 3);
      if (Number.isInteger(second / 3)) n = second;
      else return false;
    }
  }
};
```

시간복잡도: O(log N)

3<sup>21</sup>이 n으로 왔을 떄 3으로 계속 나누어 확인한다면 21번을 전부 돌아야 한다.  
따라서, 제곱수가 짝수냐 홀수냐를 기준으로 짝수일 경우 반으로 나누어 확인해주고, 홀수인 경우 3으로 나누어 제곱수를 짝수로 만들어준다. (3<sup>20</sup> -> 3<sup>10</sup> -> 3<sup>5</sup> -> 3<sup>4</sup> -> 3<sup>2</sup> -> 3<sup>1</sup>)
