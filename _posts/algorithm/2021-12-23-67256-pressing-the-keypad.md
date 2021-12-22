---
title: "<span>프로그래머스</span><span>Lv1</span> [카카오 인턴] 키패드 누르기"
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2021-12-23
---

### 문제 설명
스마트폰 전화 키패드의 각 칸에 다음과 같이 숫자들이 적혀 있습니다.  
<img src='{{ "/assets/images/2021-12-23-67256.png" | relative_url }}' style="width: 400px;" />  
이 전화 키패드에서 왼손과 오른손의 엄지손가락만을 이용해서 숫자만을 입력하려고 합니다.  
맨 처음 왼손 엄지손가락은 `*` 키패드에 오른손 엄지손가락은 `#` 키패드 위치에서 시작하며, 엄지손가락을 사용하는 규칙은 다음과 같습니다.

1. 엄지손가락은 상하좌우 4가지 방향으로만 이동할 수 있으며 키패드 이동 한 칸은 거리로 1에 해당합니다.
1. 왼쪽 열의 3개의 숫자 `1`, `4`, `7`을 입력할 때는 왼손 엄지손가락을 사용합니다.
1. 오른쪽 열의 3개의 숫자 `3`, `6`, `9`를 입력할 때는 오른손 엄지손가락을 사용합니다.
1. 가운데 열의 4개의 숫자 `2`, `5`, `8`, `0`을 입력할 때는 두 엄지손가락의 현재 키패드의 위치에서 더 가까운 엄지손가락을 사용합니다.  
만약 두 엄지손가락의 거리가 같다면, 오른손잡이는 오른손 엄지손가락, 왼손잡이는 왼손 엄지손가락을 사용합니다.

순서대로 누를 번호가 담긴 배열 numbers, 왼손잡이인지 오른손잡이인 지를 나타내는 문자열 hand가 매개변수로 주어질 때, 각 번호를 누른 엄지손가락이 왼손인 지 오른손인 지를 나타내는 연속된 문자열 형태로 return 하도록 solution 함수를 완성해주세요.

### 제한 조건
* numbers 배열의 크기는 1 이상 1,000 이하입니다.
* numbers 배열 원소의 값은 0 이상 9 이하인 정수입니다.
* hand는 `"left"` 또는 `"right"` 입니다.
  * `"left"`는 왼손잡이, `"right"`는 오른손잡이를 의미합니다.
* 왼손 엄지손가락을 사용한 경우는 `L`, 오른손 엄지손가락을 사용한 경우는 `R`을 순서대로 이어붙여 문자열 형태로 return 해주세요.

### 입출력 예
|numbers|hand|result|
|-|-|-|
|[1, 3, 4, 5, 8, 2, 1, 4, 5, 9, 5]|"right"|"LRLLLRLLRRL"|
|[7, 0, 8, 2, 8, 3, 1, 5, 7, 6, 2]|"left"|"LRLLRRLLLRR"|
|[1, 2, 3, 4, 5, 6, 7, 8, 9, 0]|"right"|"LLRLLRLLRL"|

### 입출력 예에 대한 설명
#### 입출력 예 #1
순서대로 눌러야 할 번호가 [1, 3, 4, 5, 8, 2, 1, 4, 5, 9, 5]이고, 오른손잡이입니다.

|왼손 위치|오른손 위치|눌러야 할 숫자|사용한 손|설명|
|-|-|-|-|-|
|*|#|1|L|1은 왼손으로 누릅니다.|
|1|#|3|R|3은 오른손으로 누릅니다.|
|1|3|4|L|4는 왼손으로 누릅니다.|
|4|3|5|L|왼손 거리는 1, 오른손 거리는 2이므로 왼손으로 5를 누릅니다.|
|5|3|8|L|왼손 거리는 1, 오른손 거리는 3이므로 왼손으로 8을 누릅니다.|
|8|3|2|R|왼손 거리는 2, 오른손 거리는 1이므로 오른손으로 2를 누릅니다.|
|8|2|1|L|1은 왼손으로 누릅니다.|
|1|2|4|L|4는 왼손으로 누릅니다.|
|4|2|5|R|왼손 거리와 오른손 거리가 1로 같으므로, 오른손으로 5를 누릅니다.|
|4|5|9|R|9는 오른손으로 누릅니다.|
|4|9|5|L|왼손 거리는 1, 오른손 거리는 2이므로 왼손으로 5를 누릅니다.|
|5|9|-|-|-|

따라서 `"LRLLLRLLRRL"`를 return 합니다.

#### 입출력 예 #2
왼손잡이가 [7, 0, 8, 2, 8, 3, 1, 5, 7, 6, 2]를 순서대로 누르면 사용한 손은 `"LRLLRRLLLRR"`이 됩니다.

#### 입출력 예 #3
오른손잡이가 [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]를 순서대로 누르면 사용한 손은 `"LLRLLRLLRL"`이 됩니다.

## 답안
#### 나의 풀이
```javascript
function solution(numbers, hand) {
  let answer = '';
  const position = {
    L: 10,
    R: 12
  };
  const fingerInfo = {
    1: 'L',
    4: 'L',
    7: 'L',
    3: 'R',
    6: 'R',
    9: 'R',
    left: 'L',
    right: 'R'
  };

  numbers.forEach(num => {
    if(num === 0) num = 11;

    const finger = fingerInfo[num];
    if(finger) {
      answer += fingerInfo[num];
      position[fingerInfo[num]] = num;
    } else {
      const abs = {
        left: Math.abs(num - position.L),
        right: Math.abs(num - position.R)
      };
      const gap = {
        left: parseInt(abs.left / 3) + abs.left % 3,
        right: parseInt(abs.right / 3) + abs.right % 3
      };

      if(gap.left > gap.right) {
        answer += 'R';
        position.R = num;
        return;
      } else if(gap.left < gap.right) {
        answer += 'L';
        position.L = num;
        return;
      } else {
        answer += fingerInfo[hand];
        position[fingerInfo[hand]] = num;
      }
    }
  });

  return answer;
}
```

#### 다른 사람 풀이
```javascript
function solution(numbers, hand) {
  const hands = new Map();
  let answer = "";
  hands.set("left", "*");
  hands.set("right", "#");

  numbers.forEach((number) => {
    if([1, 4, 7].includes(number)) {
      answer += "L";
      hands.set("left", number);
    } else if([3, 6, 9].includes(number)) {
      answer += "R";
      hands.set("right", number);
    } else {
      answer += findNearest(hands, number, hand);
    }
  });

  return answer;
}

function findNearest(hands, number, hand) {
  const keypad = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9],
    ["*", 0, "#"],
  ];

  const left = hands.get("left");
  const right = hands.get("right");
  let numIndex;
  let leftIndex;
  let rightIndex;

  keypad.forEach((arr, index) => {
    if(arr.includes(number)) numIndex = [index, arr.indexOf(number)];
    if(arr.includes(left)) leftIndex = [index, arr.indexOf(left)];
    if(arr.includes(right)) rightIndex = [index, arr.indexOf(right)];
  });

  const leftDistance = checkDistance(numIndex, leftIndex);
  const rightDistance = checkDistance(numIndex, rightIndex);

  if(leftDistance === rightDistance) {
    if(hand === "left") {
      hands.set("left", number);
      return "L";
    } else {
      hands.set("right", number);
      return "R";
    }
  } else {
    if(leftDistance < rightDistance) {
      hands.set("left", number);
      return "L";
    } else {
      hands.set("right", number);
      return "R";
    }
  }
}

function checkDistance(numIndex, hand) {
  if(numIndex[0] === hand[0]) {
    return Math.abs(numIndex[1] - hand[1]);
  }

  return(
    Math.abs(numIndex[0] - hand[0]) + Math.abs(numIndex[1] - hand[1])
  );
}
```
Map 사용