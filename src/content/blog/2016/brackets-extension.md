---
title: 코딩의 작업효율을 올려주는 Brackets 확장기능
pubDate: 2016-07-08
tags: outline, document, merge, guide, todo, emmet, zencoding, linter, w3c, sass, hint, git, sinppets, lorem, comb, ipsum, autoprefixer, adobe, brackets, coding, extension, plugin, 코딩, 플러그인, 확장기능, 효율성, sapjil, 삽질
description: 이제는 많이 안정화 되었다고 생각되는 Adobe 'Brackets'로 코딩작업시에 작업시간을 단축시켜주어 업무효율을 올려줄것이라 기대되는 플러그인들을 위주로 정리해 보았습니다.
categories:
  - coding
# heroImage: '/blog-placeholder-3.jpg'
---

![sapjil-Brackets](https://c3.staticflickr.com/8/7098/27885232610_e6d8fa513b_b.jpg)

계속해서 Sublime Text 3로 즐거운(?) 코딩 생활을 지속하는데 있어 불편함은 전혀 없지만, 새로운 에디터를 활용해보고자 Adobe Brackets를 사용해보았습니다.

작년까지 잠깐 사용해 볼때는 Sublime에 너무 익숙해서인지 편리성 같은 건 잘 느끼지 못한채 살짝 위화감까지 있었는데 이번에 잠시 사용해 보면서 정말 필요했던 기능을 발견했던터라 몇일간 데모 사이트를 구축해보면서 이것저것 필요해보이는 플러그인들을 깔아보고 쓸만 하다고 생각되는것 몇가지를 어디까지나 개인적인 관점에서 소개하고자 합니다.

<i class="fa fa-list-alt"></i> **table of contents**

- 확장기능 인스톨

- 추천 확장기능 1

  - [Color Merge](#Color Merge) - CSS에 적용된 컬러를 뽑아서 팔레트로 표시
  - [Document Outline](#Document-Outline) - HTML5문서의 아웃라인을 표시
  - [Tabs - Custom working](#Tabs-Custom-working) - 열려있는 각 파일간을 Tab으로 이동
  - [Indent Guides](#Indent-Guides) - 문서에 인덴트 적용
  - [Todo](#Todo) - 문서상의 todo를 확인
  - [Emmet](#Emmet) - 젠코딩

- 추천 확장기능 2

  - [Interactive Linter](#Interactive-Linter) - 각종 오류체크 확인
  - [SASSHint](#SASSHint) - SASS에서 사용된 변수값을 쉽게 불러올수 있게 해줌
  - [W3CValidation](#W3CValidation) - w3c의 문법을 체크

- 기타 확장기능
  - [Brackets Outline List](#Brackets-Outline-List)
  - [Brackets Git](#Brackets-Git)
  - [Brackets Snippets (by edc)](#Brackets-Snippets-by-edc)
  - [QuickForm Tool](#QuickForm-Tool)
  - [Lorem Pixel](#Lorem-Pixel)
  - [Lorem Ipsum](#Lorem-Ipsum)
  - [Markdown Preview](#Markdown-Preview)
  - [CSS Comb](#CSS-Comb)
  - [Beauty](#Beauty)
  - [Autoprefixer](#Autoprefixer)

[TOP – 100 extensions](#TOP-100-extensions)

## 확장기능 인스톨

![Brackets](https://c4.staticflickr.com/8/7713/28086454611_c2f7f2ccac_z.jpg)

따로 설명이 필요 없겠지만, 플러그인을 설치 할때는 검색해서 찾아서 설치버튼을 누르면 됩니다. 쉽죠?

## 추천 확장기능1

### Color Merge

![Brackets](https://c3.staticflickr.com/8/7334/27880636290_d787bd8749_z.jpg)

확인하고자 하는 <mark>CSS파일을 열고 플러그인을 활성화 시키면 페이지에서 사용되고 있는 컬러들을 쭈~욱 뽑아서 컬러팔레트로 보여 줍니다.</mark> 작업을 하다보면 사이트나 이미지에서 컬러픽커로 색을 가져다 사용하기도 하는데 값이 조금씩 달라지는 경우가 있습니다. 결국 색상이 늘어나는 이유중에 하나이기도 하죠.

해당플러그인을 사용할경우 CSS에서 사용되고 있는 색상들을 시각적으로 확인할 수 있어서 그동안 무의미하게 들어가 있던 색상을 정리 할 수 있었습니다. 또한 작업자 마다 다르기도 하지만 같은 컬러값을 대문자, 소문자(#FFF, #fff)로 사용하기도 하는데 이런 경우도 개별로 카운트하고 있어서 한쪽으로 통일 시킬 수 있습니다. <mark>아쉽게도 RGB값으로 사용된 컬러는 리스트에서 확인할 수 없습니다.</mark>

욕심이지만 RGB, RGBA에서 그라데이션까지 파악할 수 있다면 감히 신의 플러그인이라고 할 수 있지 않을까 생각해 봅니다.

### Document Outline

![Brackets](https://c2.staticflickr.com/8/7492/28083604881_91466ed12d_z.jpg)

문서의 아웃라인을 확인할 수 있게 해줍니다. Chrome등의 브라우저에서 플러그인으로 Heading을 기준으로 하는 아웃라인을 확인하던 기능인데 에디터상에서 확인할 수 있어서 나름 편리한 기능입니다.

### Tabs - Custom working

![Brackets](https://c4.staticflickr.com/8/7650/27547759403_1bd5982642_z.jpg)

ctr + pgUp, pgDown으로 Tab간을 이동할 수 있게끔 도와주며 각 파일 속성별로 아이콘을 생성시켜줍니다.

### Indent G

![Brackets](https://c1.staticflickr.com/8/7485/28057938192_0f60502f16_z.jpg)

기본으로는 지원되지 않는 기능으로 알고 있는데, 문서구조를 파악하기 쉽게끔 시각적으로 인덴트 구조를 표시해줍니다.

### Todo

![Brackets](https://c5.staticflickr.com/8/7523/28057938412_8d5204d2f8_z.jpg)

코딩작업시 필요한 Todo를 보여줍니다. 기본셋팅으로 todo, note, fixme, feture가 적용되어 있는데 설정에서 새로 추가시킬 수 도 있습니다.

### Emmet

![Brackets](https://c5.staticflickr.com/8/7352/28129207916_daa5c9d48c_z.jpg)

젠코딩으로 유명한 emmet. 편하긴 하지만 많이 사용하지는 않아서 기능상 몰랐던 부분도 있는데 Brackets에 사용된 emmet에는 나름 편리한 기능이 탑재되어 있습니다. 숫자를 정수단위, 소수점 단위로 올리거나 내릴 수 있다니... 많이 사용되진 않지만 가려운곳을 긁어주는 기능등이 있습니다.

Sublime에서는 짧은소스를 적은 후에 단축키로 랜더링(?)을 시켜주는 방식인데 해당 플러그인은 입력창에 입력시 실시간으로 보여주는점이 다른것 같습니다.

## 추천 확장기능2

### Interactive Linter

<mark>각종오류를 체크해줌으로 생각지 말고 필수 설치 항목이라 생각됩니다!!</mark>

coffeescript, csslint, htmlhint, eslint, jscs, jshint, jslint, jsx, jsonlint를 포함하고 있기 때문에 작업시 오류가 나거나 확인이 필요한 부분을 확인이 가능합니다.

### SASSHint

미리 지정해 둔 값들을 불러들이기에 편합니다.
SASS 파일 작성시 '$'를 붙이면 지정되어 있는 값들을 보여주기 때문에 작업이 수월합니다.

### W3CValidation

w3c의 문법을 체크하여 에러창 에서 확인이 필요한 부분을 지적 해줍니다.

## 기타 확장기능

사용자에 따라서 필요하기도 하고 필요 없을 것 같은 기능들입니다. 그래도 설치 해두면 가끔씩 사용할 만한 것들을 정리하였습니다.

### Brackets Outline List

![Brackets](https://c4.staticflickr.com/8/7352/28162153955_2974f1478d_z.jpg)

Document Outline과 마찬가지로 문서의 아웃라인을 확인할 수 있게 해줍니다만 다른점은 HTML, CSS문서를 해석해서 쭈~욱 보여준다는 점입니다. Class나 Id를 사용할 경우 태그 옆에 보여줌으로 파악하기가 편할 수도(?) 있을 것 같습니다.

### Brackets Git

![Brackets](https://c5.staticflickr.com/8/7577/28058617652_12f4a12860_z.jpg)

에디터내에서 Git을 사용할 수 있게 도와줍니다.

### Brackets Snippets (by edc)

![Brackets](https://c1.staticflickr.com/8/7543/27546820504_39395d6585_z.jpg)

이미 저장되어 있는 스니펫만으로도 편리하다고 생각되지만, 설정도 변경가능한 만큼 개인취향에 맞게 수정해가는것도 나쁘진 않을 것 같습니다.

### QuickForm Tool

![Brackets](https://c3.staticflickr.com/8/7624/28128947266_cd341d6a7a_z.jpg)

form과 관련된 요소들을 타이핑없이 원클릭으로 요소 추가를 할 수 있게끔 도와줍니다.

### Lorem Pixel

![Brackets](https://c4.staticflickr.com/8/7518/28085151771_66cce7c78d_z.jpg)

Placeholder Image를 첨부시켜줍니다. 데모페이지를 작성하거나 샘플용 이미지를 작성할때 사용하기 편할 것 같습니다. 이미지를 웹상에서 불러오는 만큼 랜더링에는 시간이 걸리는 담점이 있다고 생각됩니다.

### Lorem Ipsum

![Brackets](https://c3.staticflickr.com/8/7433/28059430322_d4efb4b5dd_z.jpg)

영문이지만… 무의미한 데모텍스트를 작성하기 쉽게 도와줍니다.
lorem_p3, lorem_html_p3, lorem_s, lorem_link 등을 타이핑후 tab을 클릭하면 랜덤텍스트가 생성됩니다.
한글용은 발견하지 못했네요...

### Markdown Preview

![Brackets](https://c6.staticflickr.com/8/7568/28086320301_7beecbaa2b_z.jpg)

Markdown형식으로 문서작성을 한다면, 설치해두면 편할듯한 플러그인. 당연한 이야기지만, 파일의 확장자는 md여야 합니다.

### CSS Comb

Sublime Text에서도 도움을 받고 있는 CSS를 깔끔하게 빚질해주는 플러그인으로 소스를 정렬에 민감한 분들에게 추천합니다.

### Beauty

아름답게(?) 문서를 정렬해줍니다. ','와 '{}'를 기준으로 정렬, 줄바꿈 및 자동 인덴트를 적용해주는것 같습니다. 당연한거지만 Sass등으로 컴파일된 CSS에 사용하는건 적합하지 않으며 개인적으로는 HTML에서 사용빈도가 높을것 같습니다.

### Autoprefixer

Css에서 -moz-, -webkit-, -o-등의 폴리필을 첨부해주는데 codekit, glup, grunt등 컴파일을 도와주는 툴을 사용하지 않고 순수하게 하드코딩을 할 경우 도움이 될것 같습니다. 전 codekit을 사용중인 관계로 패스.

## TOP - 100 extensions

Brackets의 TOP 100인 확장기능을 모아둔 곳입니다.
자신에게 필요한 기능은 없는지 확인해보세요~

[http://brackets.dnbard.com/extensions](http://brackets.dnbard.com/extensions)
