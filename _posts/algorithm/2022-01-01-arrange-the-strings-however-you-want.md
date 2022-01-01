---
title: "<span>프로그래머스</span><span>Lv1</span> 문자열 내 마음대로 정렬하기"
header:
  teaser: /assets/images/algorithm/programmers_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2022-01-01
---
💚 2022년 새해 첫문제 ^O^)/ 💙

## 문제 설명
문자열로 구성된 리스트 strings와, 정수 n이 주어졌을 때, 각 문자열의 인덱스 n번째 글자를 기준으로 오름차순 정렬하려 합니다. 예를 들어 strings가 ["sun", "bed", "car"]이고 n이 1이면 각 단어의 인덱스 1의 문자 "u", "e", "a"로 strings를 정렬합니다.

### 제한 조건
* strings는 길이 1 이상, 50이하인 배열입니다.
* strings의 원소는 소문자 알파벳으로 이루어져 있습니다.
* strings의 원소는 길이 1 이상, 100이하인 문자열입니다.
* 모든 strings의 원소의 길이는 n보다 큽니다.
* 인덱스 1의 문자가 같은 문자열이 여럿 일 경우, 사전순으로 앞선 문자열이 앞쪽에 위치합니다.

### 입출력 예

|strings|n|return|
|-|-|-|
|["sun", "bed", "car"]|1|["car", "bed", "sun"]|
|["abce", "abcd", "cdx"]|2|["abcd", "abce", "cdx"]|

### 입출력 예제
##### 입출력 예 1
"sun", "bed", "car"의 1번째 인덱스 값은 각각 "u", "e", "a" 입니다. 이를 기준으로 strings를 정렬하면 ["car", "bed", "sun"] 입니다.

##### 입출력 예 2
"abce"와 "abcd", "cdx"의 2번째 인덱스 값은 "c", "c", "x"입니다. 따라서 정렬 후에는 "cdx"가 가장 뒤에 위치합니다. "abce"와 "abcd"는 사전순으로 정렬하면 "abcd"가 우선하므로, 답은 ["abcd", "abce", "cdx"] 입니다.

## 답안
#### 나의 풀이
```javascript
function solution(strings, n) {
  return strings.sort((a, b) => {
    if(a[n] === b[n]) return a > b ? 1 : -1;
    return a[n] > b[n] ? 1 : -1;
  });
}
```

#### 다른 사람 풀이
```javascript
function solution(strings, n) {
  return strings.sort((s1, s2) => s1[n] === s2[n] ? s1.localeCompare(s2) : s1[n].localeCompare(s2[n]));
}
```
* <a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare">localeCompare</a> 사용

```javascript
function solution(strings, n) {
  return strings.sort((a, b) => {
    const chr1 = a.charAt(n);
    const chr2 = b.charAt(n);

    if (chr1 == chr2) {
      return (a > b) - (a < b);
    } else {
      return (chr1 > chr2) - (chr1 < chr2);
    }
  })
}
```
* `(a > b) - (a < b)` boolean 값이 truty와 falsy값으로 변경되어 계산됨.. ^^;