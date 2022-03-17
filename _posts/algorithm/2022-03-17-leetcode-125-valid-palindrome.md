---
title: "<span>Leetcode</span> 125. Valid Palindrome"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode]
date: 2022-03-17
---

## 문제 설명

[https://leetcode.com/problems/valid-palindrome/](https://leetcode.com/problems/valid-palindrome/)

문구는 모든 대문자를 소문자로 변환하고 영숫자가 아닌 문자를 모두 삭제한 후 앞뒤로 동일하게 읽으면 회문입니다. 영숫자에는 문자와 숫자가 포함됩니다.  
문자열이 지정되면 palindrome이면 true를 반환하고 그렇지 않으면 false를 반환합니다.

### Example 1:

Input: s = "A man, a plan, a canal: Panama"  
Output: true  
Explanation: "amanaplanacanalpanama" is a palindrome.

### Example 2:

Input: s = "race a car"  
Output: false  
Explanation: "raceacar" is not a palindrome.

### Example 3:

Input: s = " "  
Output: true  
Explanation: s는 문자 이외의 문자를 삭제한 후의 빈 문자열입니다.  
빈 문자열은 앞뒤가 같기 때문에 palindrome입니다.

### Constraints:

- 1 <= s.length <= 2 \* 10<sup>5</sup>
- s는 인쇄 가능한 ASCII 문자로만 구성됩니다.

## 답안

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
const isPalindrome = function (s) {
  const newS = s.replace(/[^a-zA-Z0-9]/gi, "").toLowerCase();
  let reverseS = "";
  for (const one of newS) reverseS = one + reverseS;
  return newS === reverseS;
};
```

시간복잡도: O(N)

1. 대소문자, 숫자가 아닌 경우 공백으로 replace 해준 뒤, 전부 소문자로 바꾸어 newS에 저장한다.
1. newS를 앞에 하나씩 추가해주어 뒤집어 준다.
1. newS와 뒤집어진 문자가 같은 지 비교하여 boolean 값을 반환한다.
