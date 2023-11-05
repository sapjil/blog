---
title: 어쩌면 !important가 필요없을지도? CSS의 우선순위
pubDate: 2015-04-07
tags: priorities, calculation, css, 우선순위, 가상클래스, 클래스, 태그, 선택자, 점수, 계산법,!important, important
description: 무의미하게 사용하는 것 보다는 한번쯤 CSS 각각의 요소가 기본적으로 가지고 있는 우선순위를 고려하고, 높은 순서대로 적용된다는 점에 주의하면서 코딩을 한다면 !important를 사용하지 않고도 양질의 코딩이 가능하지 않을까 생각됩니다.
categories:
  - coding
# heroImage: '/blog-placeholder-2.jpg'
---

![css](https://farm8.staticflickr.com/7621/16446129813_4d36bcbd37_o.jpg)

얼마전 스터디에서 처음배우는 HTML, CSS라는 주제로 강의를 할일이 있었는데 듣던 분중에서 포인트에 대해서도 언급을 하면 좋을것 같다는 의견을 주신 분이 계셨었습니다. 당시에는 기억나는것도 없고해서 모른다고 했었는데 어디서 주워 들었던 것 같기도 한 가물가물한 기억이 있어 찾아보게 되었고 다행하게도 지금까지 가지고 있던 CSS의 룰과 다른점은 없었으나 '점수'로 구분을 주는 방식은 생각지 않았었기에 새롭게 알 수 있는 부분이 있었습니다.

개념상으로 우선순위를 점수로 계산하는 방법을 실제로 도입하기에는 애매한 부분이 없지 않지만 하나의 기준은 될 것 같습니다. <mark>CSS의 셀렉터가 기본적으로 가지고 있는 우선순위를 점수로 계산하여 높은 순서대로 적용</mark>된다는 점은 주의가 필요하겠습니다.

[table caption: CSS 우선순위에 따른 점수표]

| 지정방법       | 예제              |   점수 |
| :------------- | :---------------- | -----: |
| !important     | !important        |    ??? |
| 직접기입       | style=""          | 1000점 |
| ID             | #sample           |  100점 |
| Class          | .sample           |   10점 |
| 속성선택자     | a[href*="sample"] |   10점 |
| 가상클래스속성 | :first-child      |   10점 |
| 태그선택자     | ul                |    1점 |
| 전체선택       | \*                |    0점 |

상기의 점수표를 기준으로 몇가지 예제를 확인해 보겠습니다. 실제로 점수는 아래와 같은 방식으로 채점 되어집니다.

[table caption: CSS 우선순위에 따른 계산예제]

| 지정방법             | 예제                                   |   점수 |
| :------------------- | :------------------------------------- | -----: |
| !important           | color: #C00 !important;                | 최우선 |
| style=""             | 1000(style="")                         | 1000점 |
| #sample              | 100(#sample)                           |  100점 |
| li.color.label       | 1(li) + 10(.color) + 10(.label)        |   21점 |
| table tr td.color    | 1(table) + 1(tr) +  1(td) + 10(.color) |   13점 |
| li:last-child        | 1(li) + 10(:last-child)                |   11점 |
| div + \*[href="com"] | 1(div) + 0(\*) + 10([href="com"])      |   11점 |
| h1 div + span        | 1(h1) + 1(div) + 1(span)               |    3점 |
| li                   | 1(li)                                  |    1점 |

간단하게 샘플로 확인을 해 보았습니다. ID가 100점이고 Class의 합이 100점을 넘을 경우 어떻게 되는가를 시험해 본 경우입니다.

<p class="codepen" data-height="300" data-theme-id="13579" data-default-tab="result" data-user="minamiland" data-slug-hash="OPYOBZ" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="css 우선순위">
  <span>See the Pen <a href="https://codepen.io/minamiland/pen/OPYOBZ/">
  css 우선순위</a> by minamiland (<a href="https://codepen.io/minamiland">@minamiland</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

결과를 보시면 아시겠지만, Class가 총 12개로 120점이며 폰트색상을 `#C00`로 지정했지만, ID에서 지정된 폰트색상 `#333`에 영향을 미치질 못합니다. `.a.b`와 `.a .b`처럼 Class사이를 붙여서 사용할 경우나 Class사이를 띄워서 사용하는 경우에도 ID에 영향을 미치지는 못하는것 같습니다. 결국 ID와 Class사이에는 점수가 영향을 미치지 못한다는 결론이 나오는거겠죠?! 그럼 `!important`의 경우는 어떨까요?

<p class="codepen" data-height="300" data-theme-id="13579" data-default-tab="result" data-user="minamiland" data-slug-hash="wBbPVQ" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="css 우선순위">
  <span>See the Pen <a href="https://codepen.io/minamiland/pen/wBbPVQ/">
  css 우선순위</a> by minamiland (<a href="https://codepen.io/minamiland">@minamiland</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

`!important`를 사용하면 위의 예제처럼 이러한 기존의 룰이 깨져 버립니다. 이정도로 `!important`는 강력한 녀석이니 사용에 주의를 하는것이 좋겠습니다.

**참고:**

- <a href="http://www.nextree.co.kr/p8468/" target="_blank" rel="noopener noreferrer">http://www.nextree.co.kr/p8468/</a>
- <a href="http://www.clearboth.org/css3_1_by_isdn386/" target="_blank" rel="noopener noreferrer">http://www.clearboth.org/css3_1_by_isdn386/</a>
- <a href="http://qiita.com/oh_rusty_nail/items/e896825cd54e5c0a3666" target="_blank" rel="noopener noreferrer">http://qiita.com/oh_rusty_nail/items/e896825cd54e5c0a3666</a>
- <a href="http://creator.aainc.co.jp/archives/4947" target="_blank" rel="noopener noreferrer">http://creator.aainc.co.jp/archives/4947</a>

<!--update : 2016-07-26 table summary 부분 수정-->
