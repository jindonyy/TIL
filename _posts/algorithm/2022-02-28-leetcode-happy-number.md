---
title: "<span>Leetcode</span> Happy Number"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode]
date: 2022-02-28
---

## 문제 설명
[https://leetcode.com/problems/happy-number/](https://leetcode.com/problems/happy-number/)  

숫자 n이 행복한지 결정하는 알고리즘을 쓰세요.  
행복수는 다음 프로세스에 의해 정의된 숫자입니다.  
임의의 양의 정수로 시작하여 숫자를 자릿수의 제곱합으로 바꿉니다.  
숫자가 1이 될 때까지 이 과정을 반복하거나 1을 포함하지 않는 사이클에서 끝없이 반복한다.  
이 과정이 1로 끝나는 숫자는 행복합니다.  
n이 행복한 숫자이면 true를 반환하고, 그렇지 않으면 false를 반환합니다.

### Example 1:
Input: n = 19  
Output: true  
Explanation:  
12 + 92 = 82  
82 + 22 = 68  
62 + 82 = 100  
12 + 02 + 02 = 1

### Example 2:
Input: n = 2  
Output: false
 
### Constraints:
- 1 <= n <= 2<sup>31</sup> - 1

## 답안
```javascript
/**
 * @param {number} n
 * @return {boolean}
 */
const isHappy = function (n) {
  let sum = n;
  let sumList = {};
  while (sum !== 1) {
    const nArr = String(sum).split("");
    sum = nArr.reduce((acc, cur) => (acc += cur ** 2), 0);
    if (sumList[sum]) return false;
    sumList[sum] = true;
  }
  return true;
};
```
시간복잡도: O(N<sup>2</sup>)
1. happy number가 아닐 경우 제곱의 합들이 계속 반복되는 순간이 생긴다.
1. 각 자릿수를 제곱하기 위해 문자열로 바꾼 뒤 split 해준다.
1. split한 배열의 제곱들을 reduce하여 sum에 저장한다.
1. while문으로 제곱들의 합이 1이 아닐 때까지 반복한다.
1. sumList 라는 객체를 만들고 sum을 키로 사용하여 객체에 추가해준다.
1. 추가해줄 때 만약 해당 키가 이미 있다면 기존에 반복했던 제곱들의 합이므로 happy number가 아니다.  
때문에 false를 반환하여 종료한다.
1. 반복문이 종료될 때는 sum이 1인 것이므로 true를 반환한다.

## 다른 사람 풀이
```javascript
function isHappy(n) {
  let slow = fast = n;
  while (true) {
    slow = sq(slow);
    fast = sq(sq(fast));
    if (slow === fast) break;
  }
  
  return slow === 1;
}

function sq(num) {
  let sum = 0;
  while (num > 0) {
    let d = num % 10;
    sum += d * d;
    num = Math.floor(num/10);
  }
  return sum;
}
```
시간복잡도: O(N<sup>2</sup>)  
문자열로 바꾸지 않고 숫자로 계산  
사실 숫자로 계산하고 숫자로 비교하는 것이 더 빠르다!