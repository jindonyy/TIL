---
title: "<span>HackerRank</span> Time Conversion"
header:
  teaser: /assets/images/algorithm/hackerRank_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, HackerRank]
date: 2022-01-28
---

## 문제 설명
[https://www.hackerrank.com/challenges/time-conversion/problem](https://www.hackerrank.com/challenges/time-conversion/problem)

## 답안
```javascript
function timeConversion(s) {
    let hour = s.slice(0, 2);

    if(s[s.length - 2] === 'A' && hour === '12') hour = '00';
    else if(s[s.length - 2] === 'P' && hour !== '12') hour = Number(hour) + 12;

    return hour + s.slice(2, s.length -2);
}
```
- `let hour = s.slice(0, 2);`  
앞에 두글자만 바꾸어주면 되기 때문에 slice로 잘라주었다.
- `s[s.length - 2]`  
AM과 PM을 구분하기 위해 끝에서 두번 째 글자만 비교하면 되므로 문자열의 index로 활용하였다.
- `hour + s.slice(2, s.length -2);`  
앞의 두글자를 구한뒤 맨 뒤의 글자 두글자를 뺴고 복사하여 반환하였다.