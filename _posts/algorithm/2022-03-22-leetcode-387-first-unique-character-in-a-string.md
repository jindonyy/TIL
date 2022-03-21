---
title: "<span>Leetcode</span> 387. First Unique Character in a String"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode]
date: 2022-03-22
---

## 문제 설명

[https://leetcode.com/problems/first-unique-character-in-a-string/](https://leetcode.com/problems/first-unique-character-in-a-string/)

문자열이 지정되면 문자열에서 첫 번째 반복되지 않는 문자를 찾아 인덱스를 반환합니다. 존재하지 않으면 -1을 반환합니다.

### Example 1:

Input: s = "leetcode"  
Output: 0

### Example 2:

Input: s = "loveleetcode"  
Output: 2

### Example 3:

Input: s = "aabb"  
Output: -1

### Constraints:

- 1 <= s.length <= 10<sup>5</sup>
- s consists of only lowercase English letters.

## 답안

```javascript
/**
 * @param {string} s
 * @return {number}
 */
const firstUniqChar = function (s) {
  const charactersLength = {};
  for (const one of s) {
    charactersLength[one] = charactersLength[one]
      ? charactersLength[one] + 1
      : 1;
  }

  let nonRepeatingCharacter;
  for (const one of s) {
    if (charactersLength[one] === 1) {
      nonRepeatingCharacter = one;
      break;
    }
  }

  return s.indexOf(nonRepeatingCharacter);
};
```

시간복잡도: O(N)

1. for..of로 문자열의 각 알파벳을 key로 갯수를 value로 저장한다.
2. for..of를 다시 돌며 가장 먼저 발견한 1글자를 찾는다.
3. 찾은 문자의 인덱스를 반환한다.
