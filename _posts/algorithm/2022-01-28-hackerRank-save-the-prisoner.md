---
title: "<span>HackerRank</span> Save the Prisoner!"
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
[https://www.hackerrank.com/challenges/save-the-prisoner/problem](https://www.hackerrank.com/challenges/save-the-prisoner/problem)

## 답안
```javascript
function saveThePrisoner(n, m, s) {
    const result = (m % n - 1 + s) % n;
    return result === 0 ? n : result;
}
```
- m개가 n개를 넘어서게 되면 다시 1번부터 시작해야하므로 나머지를 이용하였다.
- 그러나 자기 자신도 사탕을 받고 넘어가므로 -1을 해주어야 한다.
- 그 다음, 시작점이 s를 더해주면 n을 넘어가는 경우가 생기므로 다시 n의 나머지를 구한다.