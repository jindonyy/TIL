---
title: "<span>Leetcode</span> first bad version"
header:
  teaser: /assets/images/algorithm/leetcode_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, Leetcode, Birnary search]
date: 2022-02-12
---

## 문제 설명
[https://leetcode.com/problems/first-bad-version/](https://leetcode.com/problems/first-bad-version/)  
<br>
당신은 제품 매니저이며 현재 새로운 제품을 개발하기 위해 팀을 이끌고 있습니다.  
유감스럽게도 귀사의 최신 버전의 제품이 품질 검사를 통과하지 못했습니다.  
각 버전은 이전 버전을 기반으로 개발되기 때문에 불량 버전 이후의 버전도 모두 불량입니다.  
[1, 2, ..., n] 버전이 n개이고 다음 버전이 모두 불량인 첫 번째 버전을 찾으려고 합니다.  
버전이 불량인지 여부를 반환하는 API bool isBadVersion(버전)이 제공됩니다.  
첫 번째 불량 버전을 찾는 함수를 구현합니다. API 호출 수를 최소화해야 합니다.

### Example 1:
Input: n = 5, bad = 4  
Output: 4  
Explanation:  
call isBadVersion(3) -> false  
call isBadVersion(5) -> true  
call isBadVersion(4) -> true  
그러면 4가 첫 번째 나쁜 버전입니다.

### Example 2:
Input: n = 1, bad = 1  
Output: 1
 
### Constraints:
- 1 <= bad <= n <= 2<sup>31<sup> - 1

## 답안
```javascript
/**
 * Definition for isBadVersion()
 * 
 * @param {integer} version number
 * @return {boolean} whether the version is bad
 * isBadVersion = function(version) {
 *     ...
 * };
 */

/**
 * @param {function} isBadVersion()
 * @return {function}
 */

const solution = function(isBadVersion) {
    /**
     * @param {integer} n Total versions
     * @return {integer} The first bad version
     */
    return function(n) {
        let start = 1;
        let end = n;
        let middle = Math.floor((start + end) / 2);

        while(start < end) {
            if(isBadVersion(middle)) end = middle;
            else start = middle + 1;
            middle = Math.floor((start + end) / 2);
        }

        return middle;
    };
};
```
1. isBadVersion 함수로 middle 값이 bad인지 체크한다.
2. bad인 경우 - 더 앞의 bad를 찾기 위해 end를 middle로 할당한다.  
bad가 아닐 경우 - 뒤에 bad를 찾기 위해 start를 middle 다음 인덱스로 할당한다.
3. start와 end가 같아지면 반복문을 종료하고 middle을 반환한다.

## 다른 사람 풀이
```javascript
var solution = function(isBadVersion) {
    /**
     * @param {integer} n Total versions
     * @return {integer} The first bad version
     */
    
    return function(n) {
        const binarySearch = (low, high) => {
            
            if (high - low <= 1) {
                return isBadVersion(low) ? low : high
            }
			
            const mid = low + Math.floor((high-low) / 2)
            
            return isBadVersion(mid) ? binarySearch(low,mid) : binarySearch(mid,high)
        }
        
        return binarySearch(1,n) 
    };
};
```
반복문이 아닌 재귀함수를 사용한 이진 탐색 !