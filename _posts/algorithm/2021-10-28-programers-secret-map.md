---
title: "<span>프로그래머스</span><span>Lv1</span> 비밀지도"
header:
  teaser: /assets/images/algorithm/programmers_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2021-10-28
---

2022.03.10 재풀이

## 문제 설명

네오는 평소 프로도가 비상금을 숨겨놓는 장소를 알려줄 비밀지도를 손에 넣었다. 그런데 이 비밀지도는 숫자로 암호화되어 있어 위치를 확인하기 위해서는 암호를 해독해야 한다. 다행히 지도 암호를 해독할 방법을 적어놓은 메모도 함께 발견했다.

1. 지도는 한 변의 길이가 n인 정사각형 배열 형태로, 각 칸은 "공백"(" ") 또는 "벽"("#") 두 종류로 이루어져 있다.
2. 전체 지도는 두 장의 지도를 겹쳐서 얻을 수 있다. 각각 "지도 1"과 "지도 2"라고 하자. 지도 1 또는 지도 2 중 어느 하나라도 벽인 부분은 전체 지도에서도 벽이다. 지도 1과 지도 2에서 모두 공백인 부분은 전체 지도에서도 공백이다.
3. "지도 1"과 "지도 2"는 각각 정수 배열로 암호화되어 있다.
4. 암호화된 배열은 지도의 각 가로줄에서 벽 부분을 1, 공백 부분을 0으로 부호화했을 때 얻어지는 이진수에 해당하는 값의 배열이다.

<img src='{{ "/assets/images/2021-10-28-post-img1.png" | relative_url }}' title="비밀지도 문제 설명" alt="비밀지도 문제 설명"/>
네오가 프로도의 비상금을 손에 넣을 수 있도록, 비밀지도의 암호를 해독하는 작업을 도와줄 프로그램을 작성하라.

### 입력 형식

입력으로 지도의 한 변 크기 n 과 2개의 정수 배열 arr1, arr2가 들어온다.

- 1 ≦ n ≦ 16
- arr1, arr2는 길이 n인 정수 배열로 주어진다.
- 정수 배열의 각 원소 x를 이진수로 변환했을 때의 길이는 n 이하이다. 즉, 0 ≦ x ≦ 2n - 1을 만족한다.

### 출력 형식

원래의 비밀지도를 해독하여 '#', 공백으로 구성된 문자열 배열로 출력하라.

### 입출력 예제

| 매개변수 | 값                                          |
| -------- | ------------------------------------------- |
| n        | 5                                           |
| arr1     | [9, 20, 28, 18, 11]                         |
| arr2     | [30, 1, 21, 17, 28]                         |
| 출력     | ["#####","# # #", "### #", "# ##", "#####"] |

| 매개변수 | 값                                                         |
| -------- | ---------------------------------------------------------- |
| n        | 6                                                          |
| n        | 6                                                          |
| arr1     | [46, 33, 33 ,22, 31, 50]                                   |
| arr2     | [27 ,56, 19, 14, 14, 10]                                   |
| 출력     | ["######", "### #", "## ##", " #### ", " #####", "### # "] |

## 답안

#### 나의 풀이

```javascript
function solution(n, arr1, arr2) {
  const binaryArr1 = arr1.map((x) => x.toString(2).padStart(n, 0));
  const binaryArr2 = arr2.map((x) => x.toString(2).padStart(n, 0));

  return binaryArr1.map((el, i) => {
    let pw = "";
    for (let j = 0; j < n; j++) {
      pw += el[j] == 1 || binaryArr2[i][j] == 1 ? "#" : " ";
    }
    return pw;
  });
}
```

#### 옛날 풀이

```javascript
function solution(n, arr1, arr2) {
  let answer = new Array(n).fill("");

  function strLength(x) {
    return x.length < n ? "0".repeat(n - x.length) + x : x;
  }

  arr1 = arr1.map((x) => strLength(x.toString(2)));
  arr2 = arr2.map((x) => strLength(x.toString(2)));

  for (let i = 0; i < arr1.length; i++) {
    for (let j = 0; j < n; j++) {
      if (arr1[i][j] == 1 || arr2[i][j] == 1) {
        answer[i] += "#";
      } else {
        answer[i] += " ";
      }
    }
  }

  return answer;
}
```

fill IE X

#### 다른 사람 풀이

```javascript
var solution = (n, a, b) =>
  a.map((a, i) =>
    (a | b[i]).toString(2).padStart(n, 0).replace(/0/g, " ").replace(/1/g, "#")
  );
```

padStart 사용
