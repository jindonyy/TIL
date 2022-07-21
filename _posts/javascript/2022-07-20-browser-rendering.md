---
title: "브라우저 렌더링 과정"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [browser rendering]
date: 2022-7-20
---

> ⚠️ '모던 자바스크립트 딥다이브'와 추가 학습을 토대로, 정리한 내용입니다.

우리가 작성한 HTML, CSS, JavaScript를 브라우저가 어떻게 파싱하여 렌더링 하는지 알아보도록 하자.

## 브라우저 렌더링 과정

1. 브라우저는 HTML, CSS, JavaScript 등 렌더링에 필요한 **리소스를 서버에 요청**하고 **서버로부터 응답**을 받는다.
2. 서버로부터 응답된 HTML과 CSS를 브라우저의 렌더링 엔진이 파싱하여 DOM과 CSSOM을 생성하고, 이들을 결합하여 **렌더 트리**를 생성한다.
3. 브라우저의 자바스크립트 엔진은 서버로부터 응답된 자바스크립트를 파싱하여 AST를 생성하고, 바이트 코드로 변환하여 실행한다. 이 때 **자바스크립트는 DOM API를 통해 DOM이나 CSSOM을 변경**할 수 있다. 변경된 DOM과 CSSOM은 다시 렌더 트리로 결합된다.
4. 렌더 트리를 기반으로 HTML 요소의 레이아웃(위치와 크기)을 계산하고, 브라우저 화면에 **HTML 요소를 페인팅**한다.
   <img src='https://cypress-pink-680.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F4e519839-309c-4f27-bd1c-86329cc1abfe%2Fclient-server.png?table=block&id=179760f8-8bd9-43cc-9ad0-cc6e4719174a&spaceId=de050283-0f2d-4547-b1c0-171096436e1e&width=2000&userId=&cache=v2' style="margin-bottom: 0;" title="브라우저 렌더링 과정" alt="브라우저 렌더링 과정"/>
   <small>출처 | https://poiemaweb.com/js-browser</small>

## 1. 브라우저의 요청과 서버의 응답

렌더링에 필요한 리소스는 모두 서버에 존재한다. 때문에 필요한 리소스를 먼저 서버에 요청해야 한다.  
서버에 요청하기 위해서 브라우저는 주소창을 제공한다. 브라우저의 주소창에 URL을 입력하고 엔터를 누르면 호스트 이름이 DNS를 통해 IP 주소로 변환된다. 그럼 이 IP 주소를 가진 서버에게 요청을 전송하게 되는 것이다.
<img src='{{ "/assets/images/2022-07-20-URL.png" | relative_url }}' style="width: 520px;" title="URL 설명" alt="URL 설명"/>  
주소창에 www.google.com을 입력한 후 엔터를 치면, google.com으로 루트 요청(protocol과 host만 있는 요청)이 가게 된다. 루트 요청은 암묵적으로 index.html을 응답하도록 기본 설정이 되어 있어 index.html이 응답으로 오게 된다.  
만약, 정적 파일을 서버에 요청하려면 www.google.com/data/data.json 과 같이 정적 파일의 경로(path)를 URI의 호스트 뒤에 입력해주면 된다.  
<br>
index.html을 요청하면 응답으로는 HTML만 올까?  
Network 탭을 확인해보면 HTML 외에도 CSS, JavaScript, 이미지, 폰트 등의 정적 파일이 온 것을 확인할 수 있다. 최초 응답으로는 HTML만 오지만, 브라우저의 렌더링 엔진이 HTML을 파싱하는 중에 외부 리소스를 로드하는 태그(link - CSS, img - 이미지, script - JavaScript 등)를 만나면 <u>HTML 파싱을 중단하고 태그들에 적힌 리소스들을 서버에 요청</u>한다.

## 2-1. HTML 파싱과 DOM 생성

URL을 통해 서버의 응답으로 온 HTML 문서는 문자열로만 이루어진 텍스트 파일이다.  
때문에 이 문자들을 파싱하여 브라우저가 렌더링할 수 있는 자료구조로 변환하여 메모리에 저장해야 한다.

> 💡 파싱(parsing) 이란?  
> 프로그래밍 언어의 문법에 맞게 작성된 텍스트 문서의 문자열을 토큰으로 분해하고, 토큰에 문법적 의미와 구조를 반영하여 **파스 트리를 생성**하는 일련의 과정이

아래의 그림은 브라우저가 HTML을 파싱하여 브라우저가 이해할 수 있는 자료구조인 DOM을 생성하는 과정이다.
<img src='https://velog.velcdn.com/images%2Fdev_jazziron%2Fpost%2Fdceb8a33-ee17-456b-b5fb-738e51c4ece6%2Fimage.png' title="HTML 파싱과 DOM 생성" alt="HTML 파싱과 DOM 생성"/>
<small>출처 | https://poiemaweb.com/js-dom</small>

1. 브라우저는 서버가 응답한 HTML 문서를 바이트(2진수) 형태로 응답받는다. 그리고 이 바이트 형태의 HTML 문서는 meta 태그의 charset 속성에 지정된 인코딩 방식(ex: UTF-8)을 기준으로 문자열로 변환된다.  
   meta 태그에 지정된 인코딩 방식은 content-type: text/html; charset=utf-8과 같이 응답 헤더에 담겨온다. 브라우저는 이를 확인하고 문자열로 변환한다.
   <img src='https://cypress-pink-680.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F692b9c53-4ab6-4c49-92f1-9efab48d9999%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-03-31_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_6.22.22.png?table=block&id=e835c921-ff63-4472-9982-97d13ee969b3&spaceId=de050283-0f2d-4547-b1c0-171096436e1e&width=2000&userId=&cache=v2' style="width: 521px;margin-bottom: 0.4em;" title="서버의 응답에 header" alt="서버의 응답에 header"/>
   <small style="display: block;margin-bottom: 2em;">출처 | https://cypress-pink-680.notion.site/c858833d3f6d4a5e8bad4a0a85abec2d</small>
2. 문자열로 변환된 HTML 문서를 읽어 최소 단위인 토큰들로 분해한다.
   > 💡 [토큰(token)](https://kin.naver.com/qna/detail.nhn?d1id=1&dirId=1040101&docId=61973019&qb=7YyM7IScIO2GoO2BsCDrnLs=&enc=utf8&section=kin&rank=3&search_sort=0&spq=0) 이란?  
   > 문법적 의미를 가지며, 문법적으로 더 나눌 수 없는 코드의 기본 요소를 의미
3. 각 토큰들은 객체로 변환하여 [노드(Node)](https://velog.io/@keinn51/HTML%EC%97%90%EC%84%9C-%EB%85%B8%EB%93%9C%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)들을 생성한다. 토큰의 내용에 따라 문서 노드, 요소 노드, 어트리뷰트 노드, 텍스트 노드가 생성된다. (이 노드들은 DOM을 구성하는 기본 요소이다.)
4. HTML 문서는 HTML 요소들로 이루어지며, 이 요소들은 중첩 관계를 갖는다. 즉, HTML 요소의 콘텐츠 영역(시작 태그에서 종료 태그 사이)에는 텍스트 뿐만 아니라 다른 HTML 요소도 포함될 수 있다. 이 중첩 관계에 의해 HTML 요소의 부자 관계가 형성되고, 이를 반영하여 모든 노드들을 트리 자료 구조로 구성된다. 이 트리 자료 구조를 DOM(Document Object Model)이라 부른다.

## 2-2. CSS 파싱과 CSSOM 생성

렌더링 엔진은 한줄 씩 파싱하여 DOM 트리를 만들어 나간다. 그러다 CSS를 로드하는 link 태그나 style 태그를 만나게 되면 DOM 생성을 잠시 멈춘다.  
그리고 link 태그의 href에 지정된 CSS 파일을 서버에 요청하거나, style 태그 내의 CSS를 HTML과 동일한 파싱 과정을(바이트 -> 문자 -> 토큰 -> 노드 -> CSSOM) 거쳐 CSSOM을 생성한다.  
CSS 파싱이 완성되면 HTML 파싱을 중단되었던 지점부터 다시 시작한다.
CSSOM은 CSS의 상속을 반영하여 생성된다.
<img src='https://cypress-pink-680.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F8f3c37cd-ea32-4b99-8b25-fb6608e4029a%2Fcssom-tree.png?table=block&id=684dba78-f904-4dbe-86cb-6975614848f3&spaceId=de050283-0f2d-4547-b1c0-171096436e1e&width=1160&userId=&cache=v2' style="margin-bottom: 0.4em;" title="서버의 응답에 header" alt="서버의 응답에 header"/>
<small style="display: block;margin-bottom: 2em;">출처 | https://cypress-pink-680.notion.site/c858833d3f6d4a5e8bad4a0a85abec2d</small>

## 2-3. 렌더 트리 생성

생성된 DOM과 CSSOM은 렌더링을 위해 **렌더 트리**로 결합된다.  
렌더 트리는 렌더링을 위한 트리 구조의 자료 구조이다. 따라서, 화면에 렌더링 되지 않는 노드들(html, head, link, script 태그 등)과 CSS에 의해 비표시(`display: none`)된 노드들은 렌더 트리에 포함되지 않는다. (`opacity:0;` `visibility: hidden;` 사용자 눈에는 보이지 않지만 레이아웃에서 공간을 차지하기 때문에 Render Tree에 포함된다.) 즉, 렌더 트리는 화면에 렌더링 되는 노드들만으로 구성된다. 렌더링 되는 태그들은 CSSOM의 속성들과 연결되어 렌더링된다.  
이러한 렌더 트리 생성 과정은 이후에도 반복될 수 있다. (아래의 reflow와 repainting에서 설명)

## 3-1. 자바스크립트 파싱에 의한 HTML 파싱 중단

CSS와 마찬가지로 HTML을 파싱하던 중 script 태그를 만나면 DOM 생성을 중단한다. 그리고 script 태그의 src에 지정된 파일을 서버에 요청하여 로드한 js 파일이나 script 내의 JavaScript 파일을 파싱하기 위해 자바스크립트 엔진에게 제어권을 넘긴다. 이후 자바스크립트 파싱이 끝난 후 렌더링 엔진으로 다시 제어권을 넘겨 중단된 시점부터 다시 HTML 파싱을 시작한다.  
이처럼 렌더링 엔진과 자바스크립트 엔진은 병렬이 아니라 직렬적으로 즉, **동기적으로** 파싱을 한다. 위에서 아래로 순차적으로 HTML, CSS, JavaScript를 파싱하고 실행한다.  
이것은 script 태그의 위치에 따라 HTML 파싱이 블로킹 되어 DOM 생성이 지연될 수 있다는 것을 의미한다. 따라서 script 태그의 위치는 중요한 의미를 가진다.

```html
...
<head>
  <meta charset="UTF-8" />
  <link rel="stylesheet" href="style.css" />
  <script>
    const $app = document.querySelector("#app");
    $app.style.color = "red"; // TypeError: Cannot read property 'style' of null
  </script>
</head>
<body>
  <div id="app"></div>
</body>
...
```

위의 코드를 보면 DOM API인 querySelector를 이용하여 id가 app인 HTML 요소를 가져오려 한다. 그러나 해당 스크립트가 실행되는 시점에는 아직 id가 app인 요소가 파싱되지 않아 DOM에 존재하지 않는다. 따라서, 위 예제는 error가 발생하여 정상 작동되지 않는다.  
이런 문제를 방지하기 위해 script 태그를 body의 제일 하단에 위치 시키는 것이 안전한 방법이다. 이렇게 하면 자바스크립트가 실행되는 시점에는 이미 DOM 생성이 완료된 후이다. 따라서, 로딩/파싱/실행으로 인해 렌더링에 지장받는 일이 발생하지 않아 페이지 로딩 시간이 단축된다.

## 3-2. script 태그의 async/defer 속성

위의 문제를 근본적으로 해결하기 위해 HTML5부터 script 태그에 async와 defer 속성이 추가되었다.  
이 속성은 외부 js 파일을 로드할 때 사용할 수 있는 속성이기 때문에 인라인으로 작성한 script 태그에는 사용할 수 없다.  
async와 defer 속성을 이용하면 HTML 파싱과 js 파일의 로드가 비동기적으로 동시에 진행된다. 하지만 JavaScript의 실행 시점에 차이가 있다.  
(해당 속성들은 IE10 이상에서 정상적으로 지원된다.)

#### async

비동기적으로 js 파일을 로드한 후, 완료되면 바로 자바스크립트의 파싱을 시작한 후 실행하게 된다. 때문에 이때, HTML 파싱은 중단된다.  
또한, 여러 개의 script에 async 속성을 지정하면 비동기적으로 순서에 상관없이 로드가 완료된 js 파일부터 파싱과 실행을 시작한다. 따라서, 순서가 보장되지 않으므로 순서에 상관이 없는 파일에만 지정해서 사용해야 한다.

#### defer

async와 마찬가지로 비동기로 로드하지만, defer 속성의 script는 파싱과 실행을 HTML 파싱이 끝난 후, 즉 DOM 생성이 끝난 이후에 시작한다.  
따라서, DOM 조작을 해야하는 script 파일은 defer 속성을 사용해야 한다.

## 3-3. 자바스크립트 파싱과 실행

자바스크립트 파싱과 실행은 브라우저의 렌더링이 아닌 자바스크립트 엔진(크롬의 V8, 파이어폭스의 SpiderMonkey 등)이 처리한다. 자바스크립트 엔진은 자바스크립트 코드를 파싱하여 CPU가 이해할 수 있는 저수준 언어로 변환하고 실행하는 역할을 한다.  
아래의 그림은 자바스크립트 엔진이 자바스크립트를 파싱하는 과정이다.
<img src="https://velog.velcdn.com/images%2Fkhg04170%2Fpost%2Fe1cb1494-89d1-4529-af48-db6926155f26%2FIMG_C64FD440D0A4-1.jpeg">
<small>출처 | https://velog.io/@chappi/</small>

#### 1. 토크나이징

HTML 파싱과 같이 단순한 문자열인 자바스크립트 코드를 어휘 분석하여 토큰들로 분해한다.

#### 2. 파싱

토큰들의 집합을 구문 분석하여 AST(추상적 구문 트리)를 생성한다. AST는 토큰에 문법적 의미와 구조를 반영한 트리 구조의 자료 구조이다.  
 AST를 사용하면 인터프리터나 컴파일러 외에도 TypeScript, Babel, Prettier 같은 트랜스파일러를 구현할 수도 있다.

#### 3. 바이트 코드 생성과 실행

생성된 AST는 인터프리터가 실행할 수 있는 중간 코드인 바이트 코드로 변환되고, 인터프리터에 의해 실행된다.

## 4. painting과 reflow, repainting

완성된 렌더 트리는 각 HTML 요소의 레이아웃(위치와 크기)을 계산하는데 사용되며, 브라우저 화면에 픽셀을 렌더링하는 페인팅 처리에 입력된다.

### layout

레이아웃에서는 브라우저의 뷰포트(브라우저 화면 상에서 실제로 표시되는 영역) 내에 표시될 노드의 정확한 위치와 크기를 계산한다.

- 페이지 초기 렌더링 시 최초 layout 과정이 일어난다.
- %, vh, vw와 같이 상대적인 위치 및 크기가 pixel 단위로 변환된다.
  <img src="https://cypress-pink-680.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F8607db79-1701-450e-b029-268bbaead2aa%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-03-31_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_8.51.19.png?table=block&id=6cfdbf96-8cbf-4544-b03c-3f2e46e3ec15&spaceId=de050283-0f2d-4547-b1c0-171096436e1e&width=2000&userId=&cache=v2">
  <small>출처 | https://cypress-pink-680.notion.site/c858833d3f6d4a5e8bad4a0a85abec2d</small>

### painting

레이아웃에서 위치, 크기 계산이 완료된 각 노드들 픽셀로 채우는 단계이다.

- 글자색, 배경색, 이미지, 그림자 등 요소의 모든 시각적 부분을 그린다.
- 처리하는 스타일이 복잡할수록 소요시간이 늘어난다. (그라데이션, 그림자 효과 등)

### reflow와 repainting

DOM이나 CSSOM을 변경하는 DOM API가 사용된 경우, 변경된 DOM과 CSSOM은 다시 렌더 트리에 결합된다.  
이렇게 변경된 렌더 트리를 기반으로 레이아웃 계산과 페인팅 과정이 거쳐 브라우저의 화면에 리렌더링한다. 이를 리플로우, 리페인팅이라 한다.
<img src="https://velog.velcdn.com/images%2Fchappi%2Fpost%2Fc5c76a16-584b-4ae5-b9c1-f19d9636c772%2F13.png">
<small>출처 | https://velog.io/@chappi/</small>

#### reflow

리플로우는 레이아웃을 다시 계산하는 것으로, 아래의 경우처럼 레이아웃에 영향을 주는 변경이 일어날 경우에 한하여 실행된다.

- 자바스크립트에 의한 노드 추가 또는 삭제
- 브라우저 창의 리사이징에 의한 뷰포트 크기 변경
- HTML 요소의 레이아웃(위치, 크기)등을 변경시키는 스타일(width, height, margin, padding, border, display, position 등)의 변경

#### repaint

재결합된 렌더 트리를 기반으로 다시 페인트하는 것을 말한다.  
reflow가 일어나면 repaint도 다시 일어나게 되지만, 꼭 reflow가 일어나지 않아도 레이아웃에 영향이 없는 css 속성(`opacity`, `background-color` , `visibility` , `outline` 등)이 변화되면 paint 과정을 다시 수행하게 된다.  
<br>
<br>
레이아웃 계산과 다시 실행되는 리렌더링은 비용이 많이 드는 작업이므로, 가급적 리렌더링이 빈번하게 발생하지 않도록 주의하는 것이 좋다.
