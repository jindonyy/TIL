---
title: "compiler와 interpreter의 차이점"
header:
  teaser: /assets/images/cs/2021-12-30-compiler-interpreter_teaser.webp
layout: single
classes: wide
categories:
  - CS
tags:
  - [javascript, CS, compiler, interpreter]
date: 2021-12-30
---

컴파일러와 인터프리터는 고급언어로 작성된 원시 프로그램(Source Program)을 목적 프로그램(Object Program)으로 번역하는 번역 프로그램이며, 프로그램 번역 방식에 따라 구분된다.

## 컴파일러(compiler)
- 소스 코드 전체를 한 번 훑고 고레벨 언어를 바로 기계어로 변환하여 **실행 파일을 생성(저장)한 후에 실행한다.**
- 번역기 같은 역할
- 저장해 놓기 때문에 상대적으로 빠르다. 👍👍
- 그러나 코드를 일부만 수정해도 다시 컴파일 해야한다. 👎
- 기계어로 변환하기 때문에 플랫폼(운영체제 OS)에 종속적이다. 👎  
만약, 윈도우에서 컴파일을 했다면 이 프로그램을 리눅스에서 쓸 수 없다.  
프로그램이 리눅스에서 필요하다면 리눅스에서, 윈도에서 필요하다면 윈도우에서 컴파일을 해야한다. (대부분의 경우 시스템 콜이 다르기 때문에 코드를 다시짜야한다.)
- 실행 전에 컴파일을 수행한다.
- 저장으로 인해 메모리 사용이 상대적으로 높다. 👎
- 전체를 읽고난 후, 전체 오류를 동시에 표시한다.
- 때문에 오류를 감지하기 어렵고, 보안적인 관점에서 좋지 않다. 👎
- 사용되는 언어: Java(둘 다 사용), C, C ++, C #, Scala, typescript (비교적 저수준 언어들)

<img src='{{ "/assets/images/cs/2021-12-30-compiler-interpreter_1.png" | relative_url }}' style="margin-top: 2rem;"/>

## 인터프리터(interpreter)
- 저장하지 않고 실행할 때 한 번에 한 줄의 코드를 번역하고 실행한다.
- 실행기 같은 역할  
정확히 말하자면, 고레벨 언어를 중간 코드(intermediate code)로 변환하고 이를 각 행마다 실행한다.  
이 중간 코드는 다른 프로그램에 의해 실행된다.
- 그때 그때 실행 하므로 상대적으로 느리다. 👎👎
- 코드를 수정해도 실행에 영향받지 않는다. 👍
- 실행할 때 해당 플랫폼(운영체제OS)에 맞게 변환하므로 종속적이지 않다. 👍
- 컴파일과 실행을 동시에 수행한다.
- 메모리 사용이 낮다. 👍
- 각 행을 실행할 때마다 하나씩 오류를 표시한다.
- 때문에 오류 감지가 상대적으로 쉽고, 오류가 뜨면 뒤에 코드를 실행하지 않으므로 보안적인 관점에서 좋다. 👍
- 사용되는 언어: Java(둘 다 사용), PHP, Perl, Python, Ruby (비교적 고수준 언어들)

## 차이점

|비교 근거|컴파일러|통역사|
|-|-|-|
|입력|한 번에 전체 프로그램을 사용합니다.|한 번에 한 줄의 코드 나 명령을 사용합니다.|
|저장|실행 파일 생성 ⭕️|실행 파일 생성 ❌|
|작동 순서|compile 뒤에 실행|interpret과 실행을 동시에|
|속도|빠르다|느리다|
|메모리|실행 파일 생성으로 인해 메모리 사용이 많다.|생성하지 않고 실행되기 때문에 메모리 사용이 적다.|
|오류|컴파일 후 모든 오류를 동시에 표시|각 행의 오류를 하나씩 표시|
|오류 감지|어렵다.|상대적으로 쉽다.|
|관련 프로그래밍 언어|C, C ++, C #, Scala, typescript|PHP, Perl, Python, Ruby|

## Reference
[https://cbw1030.tistory.com/276](https://cbw1030.tistory.com/276)  
[https://ko.gadget-info.com/difference-between-compiler](https://ko.gadget-info.com/difference-between-compiler)