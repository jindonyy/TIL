---
title: "기수 정렬(Radix sort)"
layout: single
classes: wide
categories:
  - data structure
tags:
  - [data structure, radix sort, sort]
date: 2021-12-15
---

## 기수 정렬이란?
* 숫자들간의 직접 비교를 하지 않고 정렬하는 알고리즘이다.  
다른 정렬들과 달리 실제로 이 숫자가 저 숫자보다 작은가? 하는 그런 비교를 하지 않는다.
* 숫자 목록에서 사용할 수 있는 특수 정렬 알고리즘이다.  
모든 숫자는 이진법으로 표기할 수 있고, 이진수를 대상으로 사용하는 정렬이다.  
그리고 문자열이나 이미지 같은 데이터도 원한다면 이진법으로 변환할 수 있다.  
그렇지만 우리가 실제로 사용하는 데이터는 결국 숫자이다.
* 숫자의 크기에 대한 정보가 숫자의 자릿수에 의해 정해진다는 사실을 이용한다.  
(자릿수가 긴 숫자일수록 더 큰 숫자이다.)
* 비교를 하지 않아 정렬 속도가 빠르지만 비교하려는 숫자와 최댓값의 최고 자릿수의 크기만한 메모리가 더 필요하다.
* 자리수가 고정되어 있어서 안정성이 있는 정렬 방식

## 기수 정렬 방법
1. 0~9 까지의 Bucket을 준비한다.
2. 모든 숫자에 대하여 가장 낮은 자릿수부터 해당하는 Bucket에 차례대로 숫자를 넣는다.
3. 0부터 차례대로 들어있는 버킷에서 숫자를 가져와 새로운 배열에 넣어준다.
4. 숫자들 중 가장 높은 자릿수에 도달할 때까지 자릿수를 높여가며 이 과정을 반복한다.

정렬 알고리즘 예시 시각화 사이트: [https://visualgo.net/en/sorting](https://visualgo.net/en/sorting)  

#### < 예시 >
<ol>
  <li>
    1의 자리부터 시작하여 각 숫자의 1의 자리에 맞는 bucket에 숫자들을 넣어준다.
    <img src='{{ "/assets/images/2021-12-15-radix-sort-1_1.png" | relative_url }}' style="width:650px;" title="기수 정렬 설명" alt="기수 정렬 설명"/>
    <img src='{{ "/assets/images/2021-12-15-radix-sort-1_2.png" | relative_url }}' style="width:650px;" title="기수 정렬 설명" alt="기수 정렬 설명"/>
  </li>
  <li>
    그럼 0번의 bucket부터 차례대로 숫자들을 가져와 새로운 배열에 넣어준다.<br>
    그럼 1의 자리에 대한 정렬이 되었다.
    <img src='{{ "/assets/images/2021-12-15-radix-sort-1_3.png" | relative_url }}' style="width:650px;" title="기수 정렬 설명" alt="기수 정렬 설명"/>
  </li>
  <li>
    이제 10의 자리부터 시작하여 각 숫자의 10의 자리에 맞는 bucket에 숫자들을 넣어준다.
    <img src='{{ "/assets/images/2021-12-15-radix-sort-1_4.png" | relative_url }}' style="width:650px;" title="기수 정렬 설명" alt="기수 정렬 설명"/>
  </li>
  <li>
    그럼 0번의 bucket부터 차례대로 숫자들을 가져와 새로운 배열에 넣어준다.<br>
    그럼 10의 자리에 대한 정렬이 되었다.
    <img src='{{ "/assets/images/2021-12-15-radix-sort-1_5.png" | relative_url }}' style="width:650px;" title="기수 정렬 설명" alt="기수 정렬 설명"/>
  </li>
  <li>
  위의 방법을 숫자의 가장 높은 자릿수인 1000의 자리까지 반복해준다.  
  그럼 아래와 같이 정렬된 숫자를 얻을 수 있다.
    <img src='{{ "/assets/images/2021-12-15-radix-sort-1_6.png" | relative_url }}' style="width:650px;" title="기수 정렬 설명" alt="기수 정렬 설명"/>
  </li>
</ol>


## 기수 정렬 헬퍼(pivot helper) 함수
기수 정렬을 구현하기 위해서는 세가지 헬퍼 함수가 필요하다. 

#### 데이터의 자리 수에 해당하는 숫자를 반환해주는 함수
숫자 데이터와 자리수를 넣으면 그에 자리수에 해당하는 숫자를 반환해주는 헬퍼 함수가 필요하다.
```javascript
getDigit(12345, 0); // 5
getDigit(12345, 1); // 4
getDigit(12345, 2); // 3
getDigit(12345, 3); // 2
getDigit(12345, 4); // 1
getDigit(12345, 5); // 0
```
헬퍼 함수는 두가지 방법으로 구현할 수 있다.
* string의 index를 이용  
매개변수로 들어온 숫자를 (십진법의 숫자가 들어온다고 가정) 문자열로 바꿔서 문자열의 인덱스 값으로 원하는 숫자를 찾은 다음
다시 숫자로 바꾸는 것이다.  
그러나 문자열에서 인덱스는 왼쪽에서 오른쪽으로 적용된다.  
데이터의 0번째 자리 값을 물어봤을 때 스트링으로 바꿔서 0번을 찾으면 해당 데이터의 첫번째(젤 높은 자릿수)의 숫자가 반환된다.  
때문에 음수로 인덱스를 설정하는 방식으로 계산하여 로직을 짜야해서 복잡하다.
* 자릿수가 10의 제곱이라는 것을 이용한다.  
10은 10<sup>1</sup>, 100은 10<sup>2</sup>이다.  
이런 식으로 매개변수로 들어오는 n이 10의 n승으로 계산되어 반환하는 것이다.  
수학적 계산은 들어가지만 문자열을 이용한 것보다 로직이 덜 복잡하므로 숫자를 이용하여 구현해보도록 하겠다.

```javascript
function getDigit(num, i) {
  return Math.floor(Math.abs(num) / Math.pow(10, i)) % 10;
}

getDigit(-7325, 2);
// 3
```
1. 음수 값이 들어올 수 있으므로 Math.abs 를 이용해 절대값을 바꾸어 준다.
```javascript
Math.abs(-7325) // 7325
```
2. Math.pow 를 이용해 반환하고 싶은 자릿수를 계산하여 앞에서 구한 절댓값에 나누어 준다.
```javascript
7325 / Math.pow(10, 2) // 7325 / 100 => 73.23
```
3. Math.floor 를 이용해 정수화 시켜준다.
```javascript
Math.floor(73.23) // 73
```
4. 나머지 10을 하여 끝에 1의 자리만 남게 한다.
```javascript
73 % 10 // 3
```

#### 숫자의 최고 자릿수가 얼마인지 알려주는 함수
자릿수에 따라 bucket에 넣었다 뺏다하는 과정을 총 몇 번 반복해야하는 지 알아야 한다.  
이를 구하기 위한 첫 번째 함수이다.
```javascript
digitCount(1); // 1
digitCount(25); // 2
digitCount(314); // 3
```
이런 식으로 매개변수로 들어오는 숫자의 가장 높은 자릿수가 10의 몇제곱인지 계산하여 반환해주어야 한다.  
(숫자의 총 길이라고도 표현할 수 있다.)
```javascript
function digitCount(num) {
  if (num === 0) return 1;
  return Math.floor(Math.log10(Math.abs(num))) + 1;
}

digitCount(-7325); // 4
```
1. 음수 값이 들어올 수 있으므로 Math.abs 를 이용해 절대값을 바꾸어 준다.
```javascript
Math.abs(-7325) // 7325
```
2. Math.log10 을 이용해 해당 숫자가 10의 몇 제곱인지 구한다.  
주의할 점은 log10(0) 은 -Infinity 이므로 이 경우 예외처리를 해주어야 한다.
```javascript
if (num === 0) return 1;
Math.log10(7325) // 3.864807629026147
```
3. Math.floor 를 이용해 정수화 시켜준다.  
그 다음 10의 자리일 경우 10<sup>1</sup>, 100의 자리일 경우 10<sup>2</sup>이므로 +1 을 해주어야 한다.
```javascript
Math.floor(3.864807629026147) + 1 // 3 + 1 => 4
```

#### 데이터들의 최고 자릿수 중 가장 큰 수를 구하는 함수
자릿수에 따라 bucket에 넣었다 뺏다하는 과정을 총 몇 번 반복해야하는 지 알아야 한다.  
이를 구하기 위한 두 번째 함수이다.
```javascript
function mostDigits(nums) {
  let maxDigits = 0;

  for (let i = 0; i < nums.length; i++) {
    maxDigits = Math.max(maxDigits, digitCount(nums[i]));
  }

  return maxDigits;
}
```
1. for문으로 해당 배열의 숫자들을 digitCount 매개변수로 넘겨주어 해당 숫자의 최고 자릿수를 구한다.
2. 구한 자릿수와 현재 maxDigits 중에 더 높은 값을 구해 재할당 해준다.
3. 루프가 끝난 뒤 젤 큰 자릿수가 들어간 maxDigits를 반환해준다.

## 기수 정렬 구현
```javascript
function getDigit(num, i) { // num의 i번째 자릿수에 해당 하는 숫자를 반환 
  return Math.floor(Math.abs(num) / Math.pow(10, i)) % 10;
}

function digitCount(num) { // num의 최고 자릿수를 반환
  if (num === 0) return 1;
  return Math.floor(Math.log10(Math.abs(num))) + 1;
}

function mostDigits(nums) { // nums 중에서 가장 큰 숫자의 최고 자릿수를 반환
  let maxDigits = 0;

  for (let i = 0; i < nums.length; i++) {
    maxDigits = Math.max(maxDigits, digitCount(nums[i]));
  }

  return maxDigits;
}

function radixSort(nums) {
  let maxDigitCount = mostDigits(nums); // 가장 큰 숫자의 최고 자릿수

  for(let d = 0; d < maxDigitCount; d++) { // maxDigitCount 만큼 순회
    // 0~9까지 해당하는 값들이 들어올 이중 배열을 생성
    // [ [], [], [], ... [] ] => length: 10
    let digitBuckets = Array.from({length: 10}, () => []);

    for(let i = 0; i < nums.length; i++) { // nums 배열의 모든 숫자들을 순회
      let digit = getDigit(nums[i], d); // nums[i]의 d번째 자릿수에 숫자를 저장

      digitBuckets[digit].push(nums[i]); // 위에서 만든 bucket에 digit에 해당하는 배열에 nums[i]를 push
    }
    console.log(...digitBuckets);

    nums = [].concat(...digitBuckets); // digitBuckets 안의 모든 배열들을 합쳐준다.
    console.log(nums);
  }

  return nums;
}

radixSort([23, 345, 5467, 12, 2345, 9852]);

// [] [] [12, 9852] [23] [] [345, 2345] [] [5467] [] []
// [12, 9852, 23, 345, 2345, 5467]

// [] [12] [23] [] [345, 2345] [9852] [5467] [] [] []
// [12, 23, 345, 2345, 9852, 5467]

// [12, 23] [] [] [345, 2345] [5467] [] [] [] [9852] []
// [12, 23, 345, 2345, 5467, 9852]

// [12, 23, 345] [] [2345] [] [] [5467] [] [] [] [9852]
// [12, 23, 345, 2345, 5467, 9852]
```
1. 숫자 데이터들을 받아오는 함수를 만든다. `radixSort`
2. 가장 큰 숫자의 최고 자릿수를 구한다. `mostDigits, digitCount`
3. d = 0부터 앞에서 구한 최고 자릿수까지 반복한다.
4. 각 자릿수에 대한 버킷을 만든다. (0 ~ 9) `let digitBuckets`
5. k번째 숫자를 구한 뒤 `getDigit`, 해당 버킷에 각 숫자 배치한다.
6. 버킷에 배치된 숫자를 **새로운** 배열에 버킷에 배치된 순서대로 가져온다.

## 기수 정렬의 시간복잡도
기수정렬은 모든 경우에 똑같이 **O(dn)**의 시간복잡도를 가진다.  
* 최악의 경우: **O(dn)**  
  \- 엄청나게 긴 숫자가 포함된 경우
* 평균: **O(dn)**
* 최고의 경우: **O(dn)**
  \- 모든 숫자들이 1자릿수인 경우 O(n)이 될 수 있다.
* 공간복잡도: **O(d + n)**
여기서 n은 우리가 정렬하려는 숫자의 갯수이고, d는 가장 큰 숫자의 최고 자릿수이다.  
만약 엄청나게 긴 숫자가 포함되어 있다면 기수 정렬에서 고려해야할 큰 변수가 된다!
  
때문에 기수 정렬의 시간복잡도는 아직도 논쟁 중인 부분이다.  
평균 성능이 n log n 값을 가졌던 비교 정렬에 비해서 기수 정렬이 이론상으로는 더 빠를 수 있기 때문이다.  
그러나 컴퓨터가 정보를 실제로 어떻게 저장하는지에 따라서 실제로는 그렇지 않을 수도 있으며, 비교 정렬과 비슷할 수도 있다.

## 이전의 정렬 방식들과 정리
* 합병 정렬과 퀵 정렬은 효율적인 표준 정렬 알고리즘이다.
* 퀵 정렬은 최악의 경우 느릴 수 있지만 평균적으로 합병 정렬과 비슷하다.
* 합병 정렬은 새 배열을 만들기 때문에 더 많은 메모리를 차지하다. (내부 합병 정렬이 존재하지만 매우 복잡하다.)
* 기수 정렬은 숫자에 대한 퀵 정렬 알고리즘이다.
* 기수 정렬은 자리 값을 이용하여 숫자를 정렬한다.