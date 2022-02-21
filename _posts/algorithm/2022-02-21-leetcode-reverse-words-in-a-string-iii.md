---
title: "<span>Leetcode</span> Reverse Words in a String III"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode]
date: 2022-02-21
---

## 문제 설명
[https://leetcode.com/problems/reverse-words-in-a-string-iii/submissions/](https://leetcode.com/problems/reverse-words-in-a-string-iii/submissions/)  
<br>
문자열 `s`가 주어지면 공백과 초기 단어 순서를 유지하면서 문장 내 각 단어의 문자 순서를 반대로 합니다.

### Example 1:
Input: s = "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"

### Example 2:
Input: s = "God Ding"
Output: "doG gniD"
 
### Constraints:
- 1 <= s.length <= 5 * 10<sup>4</sup>
- s contains printable ASCII characters.
- s does not contain any leading or trailing spaces.
- There is at least one word in s.
- All the words in s are separated by a single space.

## 답안
```javascript
/**
 * @param {string} s
 * @return {string}
 */
var reverseWords = function(s) {
    return s.split(' ').map(word => word.split('').reverse().join('')).join(' ');
};
```
시간복잡도: O(N<sup>2</sup>)
1. 공백을 기준으로 split 해준다.
1. 공백으로 나눠진 단어를 또 split해주어 reverse로 뒤집어준다.
1. 뒤집어진 배열을 join하여 단어로 만든 뒤 map으로 바꿔준다.
1. 다시 공백으로 join해준다.

```javascript
/**
 * @param {string} s
 * @return {string}
 */
var reverseWords = function(s) {
    let answer = '';
    let word = '';
    for(one of s) {
        if(one === ' ') {
            word += ' ';
            answer += word;
            word = '';
        } else {
            word = one + word;
        }
    }
    return answer += word;
};
```
시간복잡도: O(N)
1. 뒤집어진 단어를 담을 word와 전체 문자열을 담을 answer를 만들어 준다.
1. 문자열 길이만큼 반복문을 돈다.
1. 글자가 공백이 아닐 경우 word 앞에 글자를 더해준다.
1. 공백을 만났을 때, 공백을 word 뒤에 더해 다시 answer에 더해준다. word를 빈문자열로 초기화해준다.
1. 마지막에 word는 공백이 없으므로 answer에 더해준 후 반환한다.