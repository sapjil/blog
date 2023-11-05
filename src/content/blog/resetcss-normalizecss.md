---
title: reset.css 와 Normalize.css
pubDate: 2017-01-06
tags: normalize, reset, css, css3, coding, markup, 초기화, 마크업
description: 사이트 구축시 사용되는 CSS중에서 가장 많이 알려져 있고, 알려져 있는 만큼 많이 사용되고 있는 것 중에서 비슷하면서도 다른 성격을 가지고 있는 reset.css와 normalize.css에 대해서 살짝 알아보았습니다.
categories:
  - coding
# heroImage: '/blog-placeholder-2.jpg'
---

가끔 Reset CSS와 Normalize를 동일시하시는 분들이 있는것 같습니다만, 확실한 차이가 있는 만큼 모르시던 분들은 이번 기회에 차이점을 이해하시면 어떨까 합니다. Normalize.css는 Reset CSS와 비슷한 기능을 하지만 조금 다른 부분이 있습니다.<mark> Reset CSS가 말 그대로 무조건 초기화를 시켜버리는것에 집중하고 있는것에 반해 Normalize의 경우는 초기화는 시키지만 어느정도 스타일이 가미되어 있다</mark>고 이해하시면 좋을듯 합니다.

![sapjil-resetcss-normalizecss](https://farm1.staticflickr.com/592/31726689720_9303aef7ca_c.jpg)

## 사이트제작시 기본적으로 알아두면 좋을 CSS

어느사이엔가 웹에서 **CSS(cascadind style sheet)**는 기술의 발전에 따라 여러 유파가 생기고 없어지고 살아남기를 반복하는 생태계가 형성되어, 초기에는 없던 것들이 기술의 발달과 함께 여러 방향으로 발전을 하였습니다. 어느 분야나 마찬가지 겠지만, 깊이있게 들어가고 시간이 경과 할수록 나름대로의 생태계가 형성되는건 어쩔 수 없는 자연현상인것 같습니다. 이제는 거의 모든 마크업 엔지니어들이 작업에 도입하고 있다고 보여지는 reset.css와 normalize.css도 이런 흐름속에서 나온 산물이라고 생각되며, 초기 작업시간을 단축시켜준다는 효율성이 입증 되면서 공유되어 알려지기 시작했다고 기억하고 있습니다...

### Reset.css

**Reset CSS**란 설명하자면 <mark>브라우저간의 차이를 최대한 없에서, 스타일이 0인 상태에서 디자인을 만들어 나가기</mark> 위해 생겨난것입니다.

```css
* {
  marin: 0;
  padding: 0;
  border: none;
}
```

웹 초기(?)에 reset이라는 개념이 잡히기 전에는 전역셀렉트인 `*`로 초기화시키는 방법을 많이 사용하곤 했었습니다만, 전역으로 사용되는 만큼 불필요한 렌더링으로 인해 0.몇초 단위까지 신경써야 하는 거대 기업들에서 근무하던 머리좋은 변태분들(?)께서 신경써주신 덕분에 요새는 거의 사용되고 있진 않는 방식입니다.

Eric Mayer씨가 고안한 [Reset CSS](http://meyerweb.com/eric/tools/css/reset/)가 가장 유명하고 yahoo에서 발표한 [YUI](http://yuilibrary.com/yui/docs/cssreset/)도 많이 사용되곤 했습니다. 찾아보니 Reset CSS는 v2.0으로 2011년도가 최신상태이고, YUI는 2014년에 v3.18.1이 나온뒤 업데이트가 없는것 같습니다.

이 외에도 디자이너, 마크업엔지니어가 자기 취향에 맞게끔 만들어낸 여러 Reset CSS가 존재하고 있으니 찾아보시고 소스를 보면서 공부해 보시길 추천합니다.

아래 CDN을 통해서 지난 버전까지도 확인이 가능합니다.
[https://cdnjs.com/libraries/meyer-reset](https://cdnjs.com/libraries/meyer-reset)

### Normalize.css

가끔 Reset CSS와 Normalize를 동일시하시는 분들이 있는것 같습니다만.. [Normalize.css](http://necolas.github.io/normalize.css/)는 <mark>Reset CSS와 비슷한 기능을 하지만 속을 들여다 보면, 조금 다르다</mark>는것을 확인할 수 있습니다.

간단한 예제로 최신 버전인 v5.0.0에서 h1은 다음과 같은 속성을 이미 가지고 있습니다. reset에서 속성을 `font-size: 100%`등으로 전체 사이트의 폰트를 통일 시켜두는 것과 다르다는 것을 확인 할 수 있는 부분입니다.

```css
h1 {
  font-size: 2em;
  margin: 0.67em 0;
}
```

<mark>Normalize의 사용상 주의점</mark>이 있습니다. 앞서 언급했듯이 reset보다 디자인적인 요소가 가미되어 있기때문에, 진행하는 프로젝트에 미치는 범위를 미리 파악하시는게 좋습니다. Normalize중에서 아무거나 한가지를 선택해서 사용하면 좋을 것 같습니다만, 요새는 Reset CSS보다 Normalize가 많이 사용되고 있는 것으로 알고 있습니다.

아래 CDN을 통해서 지난 버전까지도 확인이 가능합니다.
[https://cdnjs.com/libraries/normalize](https://cdnjs.com/libraries/normalize)

> 한동안 프로젝트나 여러 개인사정 때문에 포스팅을 원활하게 하지 못했습니다만.. 새해를 맞이하야 도메인과 호스팅 비용도 계산을 했으니 다시 Re-Start 해보겠습니다.
