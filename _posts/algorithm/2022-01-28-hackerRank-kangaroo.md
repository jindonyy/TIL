---
title: "<span>HackerRank</span> Number Line Jumps (kangaroo)"
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
[https://www.hackerrank.com/challenges/kangaroo/problem?isFullScreen=true](https://www.hackerrank.com/challenges/kangaroo/problem?isFullScreen=true)

## 답안
```javascript
function kangaroo(x1, v1, x2, v2) {
    if(v1 <= v2) return 'NO';

    let idx = 1;
    while(true) {
        if(x1 + v1 * idx > x2 + v2 * idx) return 'NO';
        if(x1 + v1 * idx === x2 + v2 * idx) return 'YES';
        idx++;
    }
}

// 재풀이
function kangaroo(x1, v1, x2, v2) {
    if(v1 <= v2) return 'NO';
    if(Number.isInteger((x2 - x1) / (v1 - v2))) return 'YES';
    return 'NO';
}
```
#### < 1차 풀이 >
- x2가 x1보다 크다는 조건이 있으므로 v2가 v1보다 크면 절대 만날 수가 없으므로 바로 'NO'를 반환
- 무한 루프를 돌면서 x1이 x2와 같아 지는 시점이 있으면 'YES'를 반환
- 그러나 x1의 누적합이 x2의 누적합을 넘어서면 만날 일이 없으므로 'NO'를 반환

#### < 2차 풀이 >
반복문을 사용하지 않고, 두 캥거루가 만나게 되는 지점을 idx라고 한다면  
idx가 정수여야지만 두 캥거루가 만날 수 있게 된다.
```javascript
x1 + v1 * idx = x2 + v2 * idx
x2 - x1 = v1 * idx - v2 * idx = (v1 - v2) * idx
idx = (x2 - x1) / (v1 - v2)
```
위의 공식으로 idx를 구한 뒤 정수인지 판별해주어 'YES'를 반환해준다.