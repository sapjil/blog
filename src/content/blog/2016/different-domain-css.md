---
title: 도메인별 스타일(CSS) 지정하기
pubDate: 2016-07-19
tags: tip, css, html, 팁, 스타일시트, 도메인, iframe, href, style sheet
description: 스타일(CSS)을 도메인별로 지정하는 방법에 대하여 알아보겠습니다.
categories:
  - coding
# heroImage: '/blog-placeholder-2.jpg'
---

![different-domain-css](https://c2.staticflickr.com/9/8620/28343814425_0e8390eb14_b.jpg)

마크업을 하다보면 iframe을 사용하게 될 경우가 있습니다.
이 경우, iframe으로 불러들이는 것 까지는 좋은데 그 안에서 스타일을 조정해야 할 경우가 생기면 살짝 곤란해집니다.
버튼색상이나 여백등의 값을 불러오는 쪽에서 제어가 좀 힘들다는 점입니다.

여러 방법이 있을 것 같습니다만 CSS의 속성을 사용하여 제어 할 수 있는 방법이 있습니다.
의외로 사용할 경우가 생길 수 있으니 알아둬서 손해 볼 일은 없을것 같아 소개해 봅니다.

iframe에 관한 제어가 가능합니다.

```html
iframe[src*="sapjil.net"]{ width: 320px; height: auto; }
```

a tag에 대한 제어가 가능합니다.

```html
a[href*="sapjil.net"]{ color: blue; }
```

지정한 URL이외에 적용시키기 위해선 `^`을 사용합니다.

```html
a[href^="sapjil.net"]{ color: blue; }
```

물론 위와 같은 방법이외에도 개별 클래스를 적용해서 조정할 수도 있겠습니다만,
이렇게 <mark>도메인 별로 나누는 것이 좀더 운영에 적합</mark>한것 같다는 생각이 듭니다.
