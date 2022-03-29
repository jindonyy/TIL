---
title: "<span>Leetcode</span> 20. Valid Parentheses"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode]
date: 2022-03-30
---

## 문제 설명

[https://leetcode.com/problems/valid-parentheses/](https://leetcode.com/problems/valid-parentheses/)

문자 '(', ')', '{', '}, '[' 및 ']'만 포함된 문자열이 있으면 입력 문자열이 유효한지 여부를 확인합니다.  
입력 문자열은 다음 경우에 유효합니다.

1. 열린 브래킷은 동일한 유형의 브래킷으로 닫아야 합니다.
2. 열린 브래킷은 올바른 순서로 닫아야 합니다.

### Example 1:

Input: s = "()"  
Output: true

### Example 2:

Input: s = "()[]{}"  
Output: true

### Example 3:

Input: s = "(]"  
Output: false

### Constraints:

- 1 <= s.length <= 10<sup>4</sup>
- s는 괄호 '()[]{}'로만 구성됩니다.

## 답안

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function (s) {
  const brackets = {
    "(": ")",
    "{": "}",
    "[": "]",
  };
  const opens = [];
  for (let i = 0; i < s.length; i++) {
    if (brackets[s[i]]) opens.push(s[i]);
    else {
      if (opens.length === 0) return false;
      if (s[i] === brackets[opens[opens.length - 1]]) opens.pop();
      else return false;
    }
  }
  return opens.length ? false : true;
};
```

시간복잡도: O(N)

1. 열린 괄호를 key로 닫힌 괄호를 value로 하는 객체를 만들어 열린 괄호와 닫힌 괄호 짝을 만들어 준다.
1. s를 반복문을 돌면서 brackets[s[i]]를 넣었을 때 value가 있는 경우 열린 괄호이고, 없는 경우 닫힌 괄호이다.
1. s[i]가 열린 괄호인 경우, opens 배열에 push를 한다.
1. s[i]가 닫힌 괄호인 경우,

- 열린 괄호가 이미 다 사라진 뒤에 닫힌 괄호만 남아있을 수 있으므로 opens의 length가 0일때는 false를 반환한다.
- 열린 괄호 중에 가장 마지막 배열의 닫힌 괄호부터 만나야 하므로 `opens[opens.length - 1]`로 체크한다.
- `brackets[opens[opens.length - 1]]` 를 통해 마지막 열린 괄호의 짝인 닫힌 괄호가 s[i]와 동일한 닫힌 괄호인지 확인한다.
- 맞을 경우 마지막 열린 괄호는 짝을 찾았으므로 pop해주고, 아닐 경우 짝이 잘못 연결된 s이므로 false를 반환한다.
