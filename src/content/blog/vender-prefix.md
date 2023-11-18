---
title: 벤더 프리픽스(vendor prefix) 정도는 알고 가셔야죠?
pubDate: 2017-02-08
tags:
  [
    '벤더 프리픽스',
    '프리프로세서',
    '전처리',
    '컴파일',
    'vendor prefix',
    'prefixfree',
    'Preprocessor',
    '-moz-',
    '-webkit-',
    '-o-',
    '-ms-',
    'compile',
    'compiler',
    'sapjil',
    'css',
  ]
description: CSS3가 완전히 정착되면 없어질 것으로 예상되고 있는  벤더 프리픽스 (vendor prefix)는 각각의 브라우저에서 판독이 가능한 접두어를 붙여서 해당 브라우저에서 인식할 수 있게 하는 것을 지칭하고 있습니다. 개념과 사용법에 대하여 알아 보았습니다.
categories: css
# heroImage: '/blog-placeholder-2.jpg'
---

이제는 마크업엔지니어라면 다들(?) 알고 있겠지만 그래도 그냥 코딩만 하기보다는 누가 물어봤을 때 대답해주면 전문가다워 보일 수 있을 것 같아 알아봤습니다.

![sapjil-vendor-prefix](https://live.staticflickr.com/65535/32873585537_16ee51cf60_c.jpg)

## 벤더 프리픽스 (vendor prefix) 개념

> vendor - 자동판매
> prefix - 접두사

브라우저별로 따로 놀던 CSS3의 속성을 잡아주기 위해서 사용되기 시작된 프리픽스는 마크업시 Css의 Class앞에 `-moz-`, `-webkit-`, `-o-`, `-ms-`라는 <mark>각 브라우저에서 판독이 가능한 접두어를 붙여서 해당 브라우저에서 인식할 수 있게 하는 것</mark>을 지칭하고 있습니다. 요새는 하나하나 직접작성 하는것 보다 Codekit, Compass, grunt, gulp등과 같은 전처리(Preprocessing)를 도와주는 툴을 사용하고 있는게 추세라고 할 수 있을 것 같습니다.

사전 준비를 잘할 경우 Sass의 mixin을 사용하여 비슷한 효과를 볼 수도 있습니다. 익스플로러에 대응하기 위하여 `filter`를 적용시키는 작업을 한적도 있습니다.

```css
[SAMPLE]
background: -ms-linear-gradient(top, #e7a66d 0%, #fcb16d 1%, #ff8d05 42%, #ffc450 100%);
background: linear-gradient(to bottom, #e7a66d 0%, #fcb16d 1%, #ff8d05 42%, #ffc450 100%);
filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#e7a66d', endColorstr='#ffc450', GradientType=0);
```

브라우저가 버전업을 할 수록 이러한 프리픽스의 사용은 점점 없어질 것으로 기대를 했었는데 벌써 3, 4년전 이야기로 기억되고.. 아직도 남아 있는걸 보면 어디까지나 추론에 지나지 않지만 앞으로도 3, 4년은 거뜬할 것 같네요. 사용하는데 있어서도 딱히 어려울것은 없지만 브라우저가 버전업이 되면서 불필요하게 생기는 요소들에 대해서는 멘테넌스가 필요하다는 점은 주의가 필요할 것 같습니다.

## 사용법

너무 쉬워서(?) 특별히 사용법을 언급 하는건 좀 그렇습니다.
CSS가 읽히는 순서나 특성을 생각하면 따로 설명이 필요 없는 부분이지만..
적혀있는 순서대로 읽고, 자기한테 적합한 부분과 만나면 판단을 내리고 다음 속성으로 넘어갑니다.
예. 그렇습니다. <mark>CSS의 문법 특성만 이해하고 있다면 사용에 아무런 문제가 없습니다.</mark>
아, 큰 의미는 없지만 아무런 접두어가 붙지 않는 CSS3속성을 가장 마지막에 둔다는 것 정도는 주의하셔도 좋을 것 같습니다.

> 아래는 기본적인 사용 예제입니다. 브라우저가 계속 버전업되고 있는 상황인만큼 사용전에 꼭 확인해보시기 바랍니다. 오페라의 경우 -o-를 사용하다가 -webkit-으로 변동되기도 한 걸로 나타나고 있네요.. **[caniuse](http://caniuse.com/#feat=matchesselector)**

| CSS Sample                       | Browser           |
| -------------------------------- | ----------------- |
| **-webkit-**border-radius: 10px; | 사파리, 크롬      |
| **-moz-**​border-radius: 10px;   | 파이어폭스        |
| **-o-**​border-radius: 10px;     | 오페라            |
| **-ms-**border-radius: 10px;     | 인터넷 익스프롤러 |
| border-radius: 10px;             | 표준 속성         |

이런 입력을 하지 않아도 해결해 주는 JS라이브러리도 있습니다만.. 어디까지나 개인적인 취향이지만 [prefixfree](http://leaverou.github.io/prefixfree/)와 같은 스크립트를 추가 시키는 것 보다 CSS에서 대처하는 쪽을 선호하는 편입니다. SASS와 같은 컴파일러를 사용하는 방법이 보편화되기 전에는 일일이 수작업이 동반되어야 했던 관계로 확인 차원에서 문제가 있었습니다. 때문에 JS를 사용하여 일괄 적용하고, 불필요해질 경우엔 그 스크립트만 제거시키는 방향으로 작업이 진행되곤 하였습니다. 화면에서 이루어지는 디자인적인 문제를 가능하면 스크립트가 아닌 CSS에서 제어시키는 게 좋다고 생각하는 이유는.. 단순히 스크립트로 도배가 되는걸 별로 좋아하지 않아서 입니다.

만약 프리프로세서를 사용하지 않고 있는 상황에서 벤더 프리픽스를 사용하여야 한다면 [caniuse](http://caniuse.com/)를 통해 브라우저별 적용 범위에 대해 한번쯤 확인해 보시길 추천합니다.

새롭게 마크업 엔지니어를 시작하시는 분에게 조금이라도 도움이 되는 정보가 되었으면 좋겠습니다.
