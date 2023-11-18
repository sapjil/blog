---
title: Wordpress 테마, 기본요소만 다운받자 - Underscores
pubDate: 2015-01-21
tags:
  [
    'build',
    'design',
    'generator',
    'theme',
    'underscores',
    'wordpress',
    '_s',
    '워드프레스',
    '테마',
    '생성',
    '제네레이터',
    '빌더',
    '디자인',
  ]
description: 이웃나라 일본에서 フリー素材アイドル MIKA☆RIKA라는 재미난 기획의, 무료제공 이미지 사이트가 있어 소개해봅니다. 아이돌이 자신들을 홍보하는 차원에서 시작한 서비스이며, 단순 사진뿐만 아니라 몇가지 사운드파일도 제공하고 있습니다. 2017년12월31일까지 기간제한을 두고 있습니다만, 자신들의 로고를 표시할경우에는 기간제한이 없다고 합니다.
categories: wordpress
# heroImage: '/blog-placeholder-2.jpg'
---

![Underscores | A Starter Theme for WordPress](https://farm8.staticflickr.com/7492/15708158004_75a6120942_o.png)

혹시, wordpress의 테마작업에 관심이 있으신가요? 그런 분들에게 Underscores라는 사이트를 소개합니다만, <mark>뭔가 화려하면서도 원하는 기능이 충실한 테마를 만들수 있을거라 기대하시면 곤란합니다. Underscores는 디자인적인 요소가 일체 배제된 녀석이기 때문입니다.</mark><sup>1</sup>

일단 Theme Name이라는 입력란에 만들고자 하는 테마명을 입력후 생성시키면 해당 테마를 zip파일로 받아볼 수 있습니다. Underscores에서 제공하는 서비스는 딱 여기까지입니다.

![Underscores | A Starter Theme for WordPress](https://farm9.staticflickr.com/8661/16144704177_597d8b3937_o.png)

추가로 입력폼 하단에 있는 Advanced Options을 선택하시면 테마이름, 테마슬러그, 제작자, 제작자의 페이지, 테마설명등을 추가로 기입할 수 있는 옵션이 있기는 합니다만 이 이상의 어떠한 옵션도 없습니다. 뭐랄까, 근본적인 기능에 충실한 사이트라고 생각됩니다.

![Underscores | A Starter Theme for WordPress](https://farm9.staticflickr.com/8566/16328811401_d4a5325ee6_o.png)

다운받은 파일의 압축을 풀어보시면 다음과 같이 테마제작에 필요한 기본적인, 필요한 파일들을 확인하실 수 있습니다.

![aligncenter](https://farm8.staticflickr.com/7464/16328696782_bb822a8e12_o.png)

다운받은 파일중에서 style.css를 열어보시면 테마명이 등록되어 있는걸 확인하실 수 있을겁니다. 저같은 경우 옵션설정을 하지 않아서 테마URI나 제작자 정보가 기본정보로 등록되어 있습니다. 관련정보들은 작업자 본인의 환경에 적합하게 수정시키시면 됩니다.

```
Theme Name: sapjil
Theme URI: http://underscores.me/
Author: Underscores.me
Author URI: http://underscores.me/
Description: Description
Version: 1.0.0
License: GNU General Public License v2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html
Text Domain: sapjil
Tags:
```

테마를 다운받아 테마폴더(<code>wordpress &gt; wp-content &gt; theme</code>)에 넣어두고 활성화를 시키시면 다음과 같은 아무런 장식적 요소가 없는 페이지가 보입니다.

![underscores-sample](https://farm8.staticflickr.com/7496/16329626675_b539630def_o.png)

딱하나, 굳이 아쉬운 점을 들라고 한다면 온라인으로 생성시켜주는 Generator 들이 가지고 있는 공통요소지만.. Underscores에서 사용되고 있는 기본 Id나 Class를 사용해야 한다는 점입니다. 여기서, '굳이'라고 하는 이유는 이런 Id, Class도 자기 방식대로 수정하려 하면 가능은 하기 때문입니다. 그렇게 신경쓰이는 부분도 아니니 익숙해지면 더 편할것 같기도... <mark>아무런 장식이 없지만 wordpress에서 사용되는 기본적인 파일들이 충실하게 들어가 있다고 생각합니다.</mark> CSS와 HTML에 대한 지식이 있다면 이제 흰색 종이에 선을 그리고, 색을 입히는 작업을 시작해 보시는건 어떨까요. <mark>wordpress의 구조를 이해하거나 CSS/HTML을 공부하는데 있어서도 도움</mark>이 될 것 같아 추천해 봅니다.

[underscores.me](http://underscores.me/)

1. 엄밀히 따지면 Underscores에서 사용되고 있는 리셋개념의 CSS가 적용되어 있긴 합니다.
