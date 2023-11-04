---
title: 코딩의 작업효율을 올려주는 Sublime Text Package
pubDate: 2015-06-29
tags:
  [
    'sublime text',
    '서브라임 텍스트',
    '패키지',
    '확장 기능',
    'package',
    'random text',
    'plugin',
    '플러그인',
    'sapjil',
    'All Autocomplete',
    'AutoFileName',
    'Diffy',
    'Emmet',
    'GitGutter',
    'Goto-CSS-Declaration',
    'SCSS',
    'SublimeLinter',
    'Tag',
    'BracketHighlighter',
    'W3CValidators',
  ]
description: Sublime Text Package중에서 작업효율을 올려주는 것들을 위주로 정리해 보았습니다. 익숙해지면 분명 작업시간이 단축되는 것을 체감하실 수 있을겁니다.
categories:
  - coding
# heroImage: '/blog-placeholder-2.jpg'
---

![sapjil-sublimetext](https://c2.staticflickr.com/4/3956/19236566915_a0e2baa0a3_o.jpg)

최근의 많이 사용되고 있는 에디터중에는 Brackets, Sublime Text가 가장 많이 사용되고 있지 않나 생각됩니다. 이상하게도 한국에서는 Editplus가 많은데 그 이유는 잘 모르겠습니다만.. 저는 Sublime Text를 애용하는 편입니다. 개인적으로 Coda를 주로 사용했었는데 Sublime을 접한 후로는 메인으로 사용하고 있습니다.

초반에는 그저 가볍고 좋아보여서 사용하기 시작했지만 사용하다보니 이것 저것 플러그인을 깔고 몸집이 커지는 느낌도 들고.. 이번기회에 실제로 사용하지 않는 플러그인을 삭제도 할겸, 정리하고 나니 지우지 않게 되는 몇가지가 있어 정리를 해 보았습니다.

**table of contents**

- [Package Control - 사전에 설치해 두어야 함](#Package-Control)
- [All Autocomplete - 자동완성을 지원](#All-Autocomplete)
- [AutoFileName - 자동으로 파일의 위치를 표시](#AutoFileName)
- [Diffy - 파일을 비교해줌](#Diffy)
- [Emmet - 젠코딩](#Emmet)
- [GitGutter - 버전관리상태를 알아 볼수 있게 도와줌](#GitGutter)
- [Goto-CSS-Declaration - html에서 클래스 선택시 css로 이동시켜줌](#Goto-CSS-Declaration)
- [SCSS - SASS에 Syntax적용](#SCSS)
- [SublimeLinter - Lint 설치](#SublimeLinter)
- [Tag - 태그의 열고 닫기를 지원](#Tag)
- [BracketHighlighter - Tag의 온오프 상태 확인](#BracketHighlighter)
- [W3CValidators - w3c문법 체크](#W3CValidators)
- [Random-sublime-text-plugin - 랜덤 텍스트 생성](#Random-sublime-text-plugin)

## Package Control

Sublime Text에서 각종 추가기능을 사용하기 위해서는 Package Control을 사용해야 합니다. 공식사이트에서 제공하는 코드를 복사해서 Package Control를 활성화 해주시면 됩니다.

[package control installation](https://packagecontrol.io/installation)

## All Autocomplete

자동완성을 도와줍니다.

![sublimetext-AllAutocomplete](https://c1.staticflickr.com/1/401/19239180481_30a4bbe8bf_o.png)

## AutoFileName

코딩시에는 CSS를 불러들이거나, 이미지를 불러들이는등 여러가지로 파일을 임포트 시킬 경우가 있습니다. 그럴경우에 자동으로 파일의 위치를 알려주어 작업을 용이하게 해줍니다.

![sublimetext-AutoFileName](https://c1.staticflickr.com/1/475/19209396496_1c486a953f_o.png)

## Diffy

파일을 비교해주는 플러그인입니다. 저같은 경우 Mac용 Kaleidoscope를 사용하고 있어서 실제로는 사용하지 않지만 필요하신 분들이 계실것 같아 목록에 추가시켜 보았습니다.

![sublimetext-Diffy](https://c1.staticflickr.com/1/415/19209333676_0af432f65d_o.png)

비교하고 싶은 파일 2개를 불러들여 'View &gt; Layout &gt; Columns:2'를 선택한후 <kbd>⌘</kbd> + <kbd>K</kbd>, <kbd>⌘</kbd> + <kbd>D</kbd>순으로 누르면 다른 부분을 하이라이트 시켜줍니다. 별도로 파일비교툴을 사용하지 않는다면 이 팩키지만으로도 확인작업이 가능하리라 생각됩니다.

## Emmet

Zen-Coding은 많이 사용되고 있기에 따로 설명이 필요없겠죠? 예를 들어 html에서는 `<ul>li*5>`처럼 작성후 `Ctr+e`로 ul안에 li를 5개만들어주는 작업이 가능하며, CSS에서는 `float:right`를 작성할 경우 `flr`이라고 작성하면 `float: right`처럼 작성됩니다.

![sublimetext-Emmet](https://c1.staticflickr.com/1/425/18614858753_7e48eb20ff_o.png)

## GitGutter

혹시 Git을 사용하고 계신가요? 버전관리를 하고 계신분이라면 꼭! 추가시키시면 후회하지 않으실 플러그인입니다. 코드작업시에 이전 작업에서 수정된 부분과, 현재 작업을 진행하고 있는 부분을 확인시켜 주기 때문에 무척 도움이 됩니다.

![sublimetext-GitGutter](https://c1.staticflickr.com/1/266/19047802790_77c46ddcf5_o.png)

## Goto-CSS-Declaration

html에서 사용되고 있는 클래스를 선택한후 해당 옵션을 선택하면 자동으로 CSS의 해당 클래스로 이동됩니다.

![sublimetext-Goto-CSS-Declaration](https://c2.staticflickr.com/4/3754/18612944764_4b0f08289f_o.png)

## SCSS

SASS를 작업할때 Sublime에서는 Syntax가 적용되어 있지 않기 때문에 구분이 힘듭니다. 이 플러그인을 적용시킴으로 해서 알아보기 쉬어집니다.

![sublimetext-scss](https://c1.staticflickr.com/1/518/19049273119_bb31207637_o.png)

## SublimeLinter

Lint의 경우는 각종 문법오류를 체크해줍니다. 작업하는 순간에 오류를 체크해주기 때문에 실수를 상당수 줄여줍니다.

![sublimetext-lint](https://c1.staticflickr.com/1/378/19229506942_df64fc001a_o.png)

SublimeLinter-jshint, SublimeLinter-csslint, SublimeLinter-contrib-scss-lint, SublimeLinter-phplint등등이 있으니 작업환경에 맞추어서 적용시키면 좋을것 같습니다.

## Tag

Tag를 열고 닫는작업을 수월하게 해줍니다. `<tag>`를 열고, `</>`까지 입력하면 자동으로 닫아주는 플러그인입니다.

![sublimetext-Tag](https://c1.staticflickr.com/1/527/19209332826_7ab3063b63_o.png)

## BracketHighlighter

코딩의 기본은 각종 Tag의 열고 닫기입니다. 이 기본을 지키지 않으면 문제가 많이 있겠죠? 해당 패키지는 Tag의 열고 닫는 부분을 알기 쉽게 표시해 줍니다.

![sublimetext-BracketHighlighter](https://c2.staticflickr.com/4/3674/18614858843_e382c48f7f_o.png)

## W3CValidators

W3C에 접속해서 오류를 확인해 줍니다. 직접 사이트에 접속해서 확인하는 방법도 있지만 개인적으로는 너무 많은 정보를 보여주고 있기 때문에 이 플러그인처럼 오류가 나는 부분만을 뽑아서 보여준다는 점이 마음에 드는 부분입니다.

![sublimetext-W3C Validation](https://c2.staticflickr.com/4/3791/19049273799_2d6eba12f9_o.png)

'Tools &gt; W3C Validators'에서 체크하고자 하는 문서형식을 고르면 됩니다.
위 예제는 HTML의 마크업작업은 HTML5형식으로 작업한 후에 HTML4를 기준으로 체크를 진행한 예입니다.

## Random-sublime-text-plugin

다양한 형태의 랜덤 텍스트를 생성시켜줍니다.

![random-sublime-text-plugin](https://media.giphy.com/media/3oz8xKvVpylFjnSLK0/giphy.gif)

샘플로 이메일을 랜덤으로 생성시켜봤습니다. 보시면 아시겠지만 텍스트, 컬러, 성, 이름, 이메일등등 다양한 옵션이 있습니다. 은근 사용하기 편합니다.
