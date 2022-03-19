---
title: "<span>프로그래머스</span><span>Lv2</span> 기능개발"
header:
  teaser: /assets/images/algorithm/programmers_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programmers, stack, queue]
date: 2022-03-20
---

## 문제 설명

[https://programmers.co.kr/learn/courses/30/lessons/42586](https://programmers.co.kr/learn/courses/30/lessons/42586)

프로그래머스 팀에서는 기능 개선 작업을 수행 중입니다. 각 기능은 진도가 100%일 때 서비스에 반영할 수 있습니다.  
또, 각 기능의 개발속도는 모두 다르기 때문에 뒤에 있는 기능이 앞에 있는 기능보다 먼저 개발될 수 있고, 이때 뒤에 있는 기능은 앞에 있는 기능이 배포될 때 함께 배포됩니다.  
먼저 배포되어야 하는 순서대로 작업의 진도가 적힌 정수 배열 progresses와 각 작업의 개발 속도가 적힌 정수 배열 speeds가 주어질 때 각 배포마다 몇 개의 기능이 배포되는지를 return 하도록 solution 함수를 완성하세요.

### 제한 조건

- 작업의 개수(progresses, speeds배열의 길이)는 100개 이하입니다.
- 작업 진도는 100 미만의 자연수입니다.
- 작업 속도는 100 이하의 자연수입니다.
- 배포는 하루에 한 번만 할 수 있으며, 하루의 끝에 이루어진다고 가정합니다. 예를 들어 진도율이 95%인 작업의 개발 속도가 하루에 4%라면 배포는 2일 뒤에 이루어집니다.

### 입출력 예

|progresses|speeds|return|
|[93, 30, 55]|[1, 30, 5]|[2, 1]|
|[95, 90, 99, 99, 80, 99]|[1, 1, 1, 1, 1, 1]|[1, 3, 2]|

### 입출력 예 설명

##### 입출력 예 #1

첫 번째 기능은 93% 완료되어 있고 하루에 1%씩 작업이 가능하므로 7일간 작업 후 배포가 가능합니다.  
두 번째 기능은 30%가 완료되어 있고 하루에 30%씩 작업이 가능하므로 3일간 작업 후 배포가 가능합니다. 하지만 이전 첫 번째 기능이 아직 완성된 상태가 아니기 때문에 첫 번째 기능이 배포되는 7일째 배포됩니다.  
세 번째 기능은 55%가 완료되어 있고 하루에 5%씩 작업이 가능하므로 9일간 작업 후 배포가 가능합니다.  
<br>
따라서 7일째에 2개의 기능, 9일째에 1개의 기능이 배포됩니다.

##### 입출력 예 #2

모든 기능이 하루에 1%씩 작업이 가능하므로, 작업이 끝나기까지 남은 일수는 각각 5일, 10일, 1일, 1일, 20일, 1일입니다. 어떤 기능이 먼저 완성되었더라도 앞에 있는 모든 기능이 완성되지 않으면 배포가 불가능합니다.  
<br>
따라서 5일째에 1개의 기능, 10일째에 3개의 기능, 20일째에 2개의 기능이 배포됩니다.

## 답안

#### 나의 풀이

```javascript
function solution(progresses, speeds) {
  const success = progresses.map((progress, idx) =>
    Math.ceil((100 - progress) / speeds[idx])
  );
  const answer = [];
  for (let i = 0; i < success.length; i++) {
    let count = 0;
    for (let j = i + 1; j < success.length; j++) {
      if (success[i] >= success[j]) {
        count++;
      } else break;
    }
    i += count;
    answer.push(count + 1);
  }
  return answer;
}
```

시간복잡도: O(N<sup>2</sup>)

1. 100%가 몇 일이 지난 후에 완성되는 지 계산하여야 한다.  
   진행률을 담은 배열(processes)의 각 요소에서 100에서 현재 요소의 차를 구한 뒤, 하루에 진행하는 퍼센트인 speeds 배열에 idx번 째를 가져와 나누어 준다.  
   100퍼센트를 넘겨야하므로 나누어준 값을 올림해준다.
   그럼 각 기능별로 100퍼센트가 되기 위해 걸리는 요일이 반환되고, success에 저장한다.
1. success를 돌며 현재 기능의 걸리는 날보다 뒤의 요소가 더 적거나 같게 걸리는 날이 있으면 해당 기능이 오픈할 때 같이 오픈하면 되므로 작거나 같은 요소를 만나면 count를 1씩 더해준다.  
   그러다 더 오래 걸리는 기능을 만나면 그 뒤부터는 함께 오픈할 수 없으므로 break를 한다.
1. 뒤의 요소를 검사하는 for문이 끝났으면 작거나 같은 요소를 찾은 개수인 count에서 자기 자신을 포함해야하므로 + 1 을 한 뒤 answer에 push 한다.
1. 앞에서 찾은 개수만큼 제외하고 뒤의 요소를 다시 비교하여 검사해야하므로 i에 count를 더해준다.

### 다른 사람 풀이

```javascript
function solution(progresses, speeds) {
  let answer = [0];
  let days = progresses.map((progress, index) =>
    Math.ceil((100 - progress) / speeds[index])
  );
  let maxDay = days[0];

  for (let i = 0, j = 0; i < days.length; i++) {
    if (days[i] <= maxDay) {
      answer[j] += 1;
    } else {
      maxDay = days[i];
      answer[++j] = 1;
    }
  }

  return answer;
}
```

1. 배열을 돌면서 maxDay를 초기값을 days[0]로 설정하여 0번째 값보다 큰지 작거나 같은지 비교한다.
1. 최고 값보다 작거나 같은 값을 만났을 때 answer의 j번째에 1씩 더해준다.
1. 큰 값을 만났을 시 더 maxDay를 업데이트 해주고, j를 1더하여 answer의 j번째에 1을 설정해준다.
