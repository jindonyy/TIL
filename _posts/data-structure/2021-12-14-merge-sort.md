---
title: "합병 정렬(Merge sort)"
layout: single
classes: wide
categories:
  - data structure
tags:
  - [data structure, merge sort, sort]
date: 2021-12-14
---

## 합병 정렬이란?
* 합병과 정렬이라는 두 가지의 기능을 하는 알고리즘이다.
* 0개 또는 1개 요소의 배열은 항상 정렬된다는 사실을 활용환 방식이다.
* 배열을 0개 또는 1개 요소의 더 작은 배열로 분해한 다음 새로 정렬된 배열을 구성하는 방식으로 작동한다.

## 합병 정렬 방법
<img src='{{ "/assets/images/2021-12-14-post-img2.png" | relative_url }}' style="width:600px;margin-top: 1.8em;" title="합병 정렬 설명" alt="합병 정렬 설명"/>

1. 배열을 1/2 단위로 계속 나누어 각각 0개 또는 1개 요소의 배열이 되도록 한다.
2. 나눈 2개의 배열을 각각 다시 합치는데 이때, 합친 뒤 정렬을 해준다.
3. 정렬을 한 뒤 다시 합치고, 다시 정렬, 다시 합치기를 반복해준다.

정렬 알고리즘 예시 시각화 사이트: [https://visualgo.net/en/sorting](https://visualgo.net/en/sorting)  
  
구현하기 전에 합병 정렬에서 중요한 합병의 방법을 좀 더 자세히 알아보자.  

## 합병 방법
앞서 보았듯이 합병 정렬을 구현하려면 먼저 두 정렬된 배열 합병을 담당하는 함수를 구현하는 것이 유용하다.  
### 구현 방식
* 정렬된 두 배열이 지정되면 helper 함수는 두 입력 배열의 모든 요소로 구성된 새 배열을 만들어야 힌다.  
* 이 함수는 O(n + m) 시간과 O(n + m) 공간에서 실행되어야 하며 전달된 파라미터를 수정해서는 안 된다.

### 구현 순서
1. 빈 배열을 만들고 각 입력 배열에서 가장 작은 값을 살펴본다.
2. 첫 번째 배열의 값이 두 번째 배열의 값보다 작으면 첫 번째 배열의 값을 새 배열에 밀어넣고, 첫 번째 배열의 다음 값으로 이동한다.  
  첫 번째 배열의 값이 두 번째 배열의 값보다 크면 두 번째 배열의 값을 새 배열에 밀어넣고, 두 번째 배열의 다음 값으로 이동한다.
3. 한 배열이 소진되면 다른 배열의 나머지 값을 모두 밀어 넣는다.

### 구현 예시
```javascript
function merge(arr1, arr2) {
  let results = [];
  let i = 0;
  let j = 0;

  while(i < arr1.length && j < arr2.length) { // 두 배열 중 길이가 더 짧은 배열의 길이까지만 순회하도록
    if(arr1[i] < arr2[j]) { // 더 작은 값을 푸쉬
      results.push(arr1[i]);
      i++;
    } else {
      results.push(arr2[j]);
      j++;
    }
  }

  while(i < arr1.length) { // 위의 while문에서 arr1의 요소가 남았을 경우
    results.push(arr1[i]);
    i++;
  }

  while(j < arr2.length) { // 위의 while문에서 arr2의 요소가 남았을 경우
    results.push(arr2[j]);
    j++;
  }

  return results;
}

merge([1, 10, 50], [2, 14, 99, 100]);

// [1, 2, 10, 14, 50, 99, 100]
```
위의 방법처럼 두 배열을 합병할 수 있다.  
그럼 이제 merge 함수에 정렬된 두 배열을 매개변수로 넘겨주는 정렬함수까지 구현해보자.

## 합병 정렬 구현
```javascript
function merge(arr1, arr2) {
  let results = [];
  let i = 0;
  let j = 0;

  while(i < arr1.length && j < arr2.length) { // 두 배열 중 길이가 더 짧은 배열의 길이까지만 순회하도록
    if(arr1[i] < arr2[j]) { // 더 작은 값을 푸쉬
      results.push(arr1[i]);
      i++;
    } else {
      results.push(arr2[j]);
      j++;
    }
  }

  while(i < arr1.length) { // 위의 while문에서 arr1의 요소가 남았을 경우
    results.push(arr1[i]);
    i++;
  }

  while(j < arr2.length) { // 위의 while문에서 arr2의 요소가 남았을 경우
    results.push(arr2[j]);
    j++;
  }

  return results;
}

function mergeSort() {
  if(arr.length <= 1) return arr;
  // 제일 안쪽의 재귀로 들어왔을 때(배열의 길이가 1개 이하일 때) arr을 return 해주어 재귀를 빠져나온다.

  let mid = Math.floor(arr.length/2); // 매개 변수로 들어오는 배열의 길이가 홀수일 수도 있으므로 
  let left = mergeSort(arr.slice(0, mid)); // 0부터 중간 지점 전까지 복사
  let right = mergeSort(arr.slice(mid)); // 중간 지점부터 끝까지 복사

  return merge(left, right);
  // 나누어준 배열들을 정렬과 합병을 해주는 merge 함수로 넘겨주고 그 결과 값을 마지막에 return 해준다.
}

mergeSort([1, 10, 50, 2, 14, 99, 100]]);
// [1, 2, 10, 14, 50, 99, 100]
```
<img src='{{ "/assets/images/2021-12-14-post-img3.png" | relative_url }}' style="width:650px;" title="합병 정렬 설명" alt="합병 정렬 설명"/>

## 합병 정렬의 시간복잡도
* 합병 정렬은 항상 시간 복잡도가 같다.  
앞서 포스팅했던 버블 정렬은 2차 함수 관계인 n제곱의 시간이 걸렸다.  
데이터가 어느 정도 정렬되어 있는 최상의 경우에도 1차 함수 관계인 n의 시간 값을 가진다.  
합병 정렬은 그런 식의 경계 조건이 없다. 들어오는 데이터가 어떻게 생겼는지는 신경을 쓰지 않아도 된다.  
그냥 배열을 다 나눈 다음에 다시 하나 하나 합병하기 때문에 입력값이 무엇인지와 관련없다.  
이미 정렬이 되어있든, 반대로 정렬이 되어있든, 완전히 무작위이든!
* 합병 정렬의 시간 복잡도는 **O(n log n)** 이다.
<img src='{{ "/assets/images/2021-12-14-post-img4.png" | relative_url }}' style="width:650px;" title="합병 정렬 설명" alt="합병 정렬 설명"/>
전체 배열의 길이가 32인 배열을 합병 정렬한다고 생각해보자.  
그럼 그 배열을 길이가 1 이하인 배열로 나누는데 걸리는 횟수는 4번이다. 즉 log 2인 것이다.  
여기서 나누어준 배열을 merge 함수를 통해 n번씩 비교해주었다.  
때문에 합병 정렬을 O(n log n)이 되는 것이다.
<br>
<br>
<img src='{{ "/assets/images/2021-12-14-post-img5.png" | relative_url }}' style="width:700px;" title="시간 복잡도 그래프" alt="시간 복잡도 그래프"/>
위의 표를 보면 n log n은 n<sup>2</sup> 보다 훨씬 낫다.  
데이터가 무엇인지 가리지 않는 정렬 알고리즘을 사용하는 경우라면 n log n이 최상이다.
<br>
<br>
* 최악의 경우: **O(n log n)**  
* 평균: **O(n log n)**
* 최고의 경우: **O(n log n)**  

## 합병 정렬의 공간복잡도
* 공간복잡도: **O(n)**

<p style="margin-top: -1em;">상수값의 공간 복잡도를 가지는 버블 정렬과 비교하면 약간 다르다.<br>
합병 정렬을 다룰 때는 배열이 커질 수록 메모리에 저장해야 하는 배열의 개수가 많아진다.<br>
그래서 더 많은 공간이 필요합니다.<br>
보통은 시간 복잡도에 더 집중하지만 공간도 고려를 해야 한다.<br>
특히 합병 정렬 같은 것은 버블 정렬이나 다른 앞에서 배운 정렬에 비하면 더 많은 공간을 점유</p>