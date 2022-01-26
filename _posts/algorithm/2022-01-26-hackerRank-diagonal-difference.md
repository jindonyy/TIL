---
title: "<span>HackerRank</span> Diagonal Difference"
header:
  teaser: /assets/images/algorithm/hackerRank_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, HackerRank]
date: 2022-01-26
---

## 문제 설명
정사각 행렬이 주어지면 대각선의 합 사이의 절대 차이를 계산합니다.
예를 들어, 정사각형 행렬 배열은 다음과 같습니다.
```
1 2 3
4 5 6
9 8 9  
```
왼쪽에서 오른쪽 대각선 = `1 + 5 + 9 = 15`입니다. 오른쪽에서 왼쪽 대각선 = `3 + 5 + 9 = 17`이다. 이들의 절대차는 `|15 - 17| = 2`다.

### 함수 설명
아래 편집기에서 `diagonalDifference` 함수를 완성하십시오.  
대각선차이는 다음 매개변수를 사용합니다.  
* int arr[n][m]: 정수 배열

### 출력
* int: 절대 대각선 차이

### 입력 형식
첫 번째 줄에는 정방 행렬 `arr`의 행과 열의 개수인 단일 정수 `n`이 포함됩니다.  
다음 `n`줄은 행 `arr[i]`를 나타내며 공백으로 구분된 정수 `arr[i][j]`로 구성되어 있다.

### 제약
-100 <= arr[i][j] <= 100

### 출력 형식
행렬의 두 대각선의 합 사이의 절대 차이를 단일 정수로 반환합니다.

### 입력 예시
```
3
11 2 4
4 5 6
10 8 -12
```

### 출력 예시
```
15
```

### 설명
기본 대각선은 다음과 같다.
```
11
  5
    -12
```
기본 대각선의 합: 11 + 5 - 12 = 4  
보조 대각선은 다음과 같다.
```
4
  5
    10
```
보조 대각선의 합: 4 + 5 + 10 = 19  
차이: |4 - 19| = 15  
참고: |x|는 x의 절대값입니다.

## 답안
#### 나의 풀이
```javascript
function diagonalDifference(arr) {
    const sum = { left: 0, right: 0 };
    const lineLen  = arr.length;

    for(let idx = 0; idx < lineLen; idx++) {
        sum.left += newArr[idx][idx];
        sum.right += newArr[idx][lineLen - 1 - idx];
    }
    
    return Math.abs(sum.left - sum.right);
}
```
이중 배열이지만 이중 반복문을 사용하지 않고,  
index가 왼쪽 줄은 0부터 1씩 증가하고 오른쪽 줄은 끝에서부터 1씩 감소하기 때문에  
반복문의 index를 활용하여 구현