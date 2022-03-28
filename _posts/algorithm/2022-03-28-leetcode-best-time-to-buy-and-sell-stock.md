---
title: "<span>Leetcode</span> 121. Best Time to Buy and Sell Stock"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode]
date: 2022-03-28
---

## 문제 설명

[https://leetcode.com/problems/best-time-to-buy-and-sell-stock/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

배열로 가격이 주어집니다. 여기서 price[i]는 i번째 날의 특정 주식 가격입니다.  
주식 한 개를 살 날을 선택하고 다른 날을 선택하여 수익을 극대화하려고 합니다.

### Example 1:

Input: prices = [7,1,5,3,6,4]  
Output: 5  
Explanation: 2일차(가격 = 1)에 구입하고 5일차(가격 = 6), 이익 = 6-1 = 5에 판매합니다.
판매 전에 구입해야 하므로 2일차에 구입하고 1일차에 판매하는 것은 허용되지 않습니다.

### Example 2:

Input: prices = [7,6,4,3,1]  
Output: 0  
Explanation: 이 경우 거래가 이루어지지 않으며 최대 이익 = 0입니다.

### Constraints:

- 1 <= prices.length <= 10<sup>5</sup>
- 0 <= prices[i] <= 10<sup>4</sup>

## 답안

```javascript
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function (prices) {
  const priceInfos = prices.map((price, idx) => [price, idx]);
  const ascending = priceInfos.sort((a, b) => a[0] - b[0]);
  const descending = priceInfos.sort((a, b) => b[0] - a[0]);
  const results = ascending.map(([min, buy]) => {
    for (let j = 0; j < descending.length; j++) {
      const [max, sell] = descending[j];
      if (buy > sell) continue;
      return max - min;
    }
  });
  return Math.max(...results);
};
```

시간복잡도: O(log N)

1. prices를 가격과 index를 담은 이중 배열로 map 한다.
1. 맵한 배열을 오름차순과 내림차순으로 정렬한다.
1. 오름차순 정렬 배열로 map을 돌면서 사려는 날이 파려는 날보다 크면 안되므로 continue해주고 그렇지 않은 경우 내림차순으로 정렬한 배열은 가장 큰 값이 앞에 와있으므로 사려는 날보다 index가 큰 수 중에 가장 첫번째 수가 이율이 가장 큰 날이므로 두 차이를 반환한다.
1. 각 날 별로 최대이익이 적힌 results 배열에서 가장 큰 값을 반환한다.

O(N)으로 풀어야 하는 문제인건지 Time Limit Exceeded 가 뜬다..ㅠ\_ㅠ
