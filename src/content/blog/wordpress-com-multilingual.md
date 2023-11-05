---
title: Wordpress.com에서 다국어 설정하기
pubDate: 2015-04-21
tags: multilingual, language, multi, wordpress, wp, 다국어, 언어, 워드프레스, com, org
description: wordpress를 사용해서 블로그나 웹서비스를  하고 있는 사용자층이 국내에서도 많아지고 있는 요즘, 기본으로 제공되는 위젯이 아니면 무조건 유료를 사용해야 하는 wordpress.com에서 별도 플러그인을 사용하지 않고 카테고리와 메뉴를 활용하여 다국어 서비스를 위한 설정방법을 알아봤습니다.
categories:
  - www
# heroImage: '/blog-placeholder-2.jpg'
---

![wordpress-title-format](https://farm9.staticflickr.com/8694/17086506702_ff1794cc84_o.jpg)

## Wordpress, 플러그인 없이 다국어 블로그 작성하기

몇년전부터인가, 한국시장에서도 wordpress(WP)가 인기를 몰기 시작하면서 여러 방면에서 WP와 관련된 비즈니스가 활발히 움직이고 있는걸 확인 할 수 있습니다. 근무중인 회사에서도 오픈 준비중인 사이트의 관련정보와 해당업계동향등을 다루는 블로그를 WP로 운영중입니다.

보통은 .org의 인스톨형을 많이 사용하지만 저희는 .com을 사용하고 있습니다. 파일관리나 버전관리등, 관리측면에서 불필요한 리소스가 발생하기에 .com을 사용하고 있습니다만, 설치형WP처럼 다양한 Plugin을 사용하여 손쉽게 원하는 기능을 추가 시킬수가 없습니다. .com의 경우, 유무료에 상관없이 테마도 플러그인도 WP가 제공하는것만 사용가능하기 때문입니다.

.com에서 다국어 지원을 하기 위해서 이런저런 머리도 굴려봤지만, 검색에 걸리는건 10중 8,9가 인스톨형 WP에서 플러그인을 활용하는 방법이었는데 결국 .com에서 제시하는 [원문](https://en.support.wordpress.com/set-up-a-multilingual-blog/)을 발견할 수 있었습니다. 역시 本家만한게 없는것 같습니다. 따로 검색을 해보기 전에 제작사의 가이드를 우선적으로 확인하는 버릇을 들여야 할듯합니다..

## wordpress.com

![WordPress.com: Create a free website or blog](https://farm8.staticflickr.com/7702/17062406666_6bc09bcc1c_o.png)

공식사이트에서 알려준 다국어지원을 위한 가이드에는 아래와 같은 3가지 방식이 있으니 하나씩 짚어 볼까 합니다.

- [Option 1: One Blog, One Post](#Option-1-One-Blog-One-Post)
- [Option 2: One Blog, Two Posts](#Option-2-One-Blog-Two-Posts)
- [Option 3: Two Blogs](#Option-3-Two-Blogs)

## Option 1: One Blog, One Post

하나의 블로그에서 다국어를 사용하는 방식입니다. 신경쓰지 않는 분이라면 상관없지만, 개념을 짚어보면 별로 추천할 만한 방식이 아닙니다.
예를 들어 국문, 영문을 혼용하는 블로그라고 하면 늘 국,영문의 포스팅을 동시에 하는 경우는 그리 많지는 않을거라 추측해 봅니다. 그리고 있다고 하더라도 영어권에서 접속한 유저들에게 읽지도 못하는 국문의 포스트는 의미도 없을 뿐더러 글을 읽는 행동에 제약을 거는 하나의 요인이 될 수 있기 때문에 추천할 만한 방식은 아니라고 생각됩니다.

## Option 2: One Blog, Two Posts

Option 1과 마찬가지로 하나의 블로그에서 다국어를 사용하는 방식이지만, Option 1보다 체계적으로 관리가 가능한 방식이고 Option 3처럼 두개의 블로그 관리가 힘들다고 여겨지는 분들에게 추천할 만한 방식이라고 생각됩니다. 초기 셋팅만 잘 해두면 나머지는 크게 신경쓸 부분이 없어질거라 예상됩니다.

방식은 복잡할것 같으면서도 의외로 단순합니다. 카테고리분류와 사용자메뉴를 잘 버무리면 가능합니다.
요약해보자면, 아래 4가지 방식으로 셋팅을 하면 됩니다.

- [Step 01 사용될 언어 카테고리 생성](#Step-01-사용될-언어-카테고리-생성)
- [Step 02 블로그에서 사용할 카테고리를 언어별로 하나씩 생성](#Step-02-블로그에서-사용할-카테고리를-언어별로-하나씩-생성)
- [Step 03 언어별 메뉴 생성](#Step-03-언어별-메뉴-생성)
- [Step 04 사이드바에 표시방식 지정](#Step-04-사이드바에-표시방식-지정)
- [Step 05 첫페이지 지정](#Step-05-첫페이지-지정)

하나씩 확인해 보도록 하겠습니다.

### Step 01 사용될 언어 카테고리 생성

첫번째 할일은 사용할 언어용 카테고리를 생성하는겁니다.
국문과 영문을 제공할 예정인 블로그라서 국, 영문용 카테고리를 생성해 두었습니다.

![카테고리 ‹ WP-DEMO — 워드프레스](https://farm8.staticflickr.com/7648/16968481808_72183ab2f2_o.png)

### Step 02 블로그에서 사용할 카테고리를 언어별로 하나씩 생성

두번째로 각각의 언어별로 사용할 카테고리를 생성합니다.
예제라서 구분되기 쉽도록 en, kr등을 붙여서 추가시켜 두었습니다. 당연한 거지만, 국문의 경우는 한글로 적어도 상관없습니다.

![카테고리 ‹ WP-DEMO — 워드프레스](https://farm9.staticflickr.com/8708/16536100213_8c89877b7e_o.png)

### Step 03 언어별 메뉴 생성

세번째로 외모 &gt; 메뉴페이지에서 각 카테고리에서 사용할 세트를 '메뉴 생성'으로 만들어둡니다.

- language라는 메뉴를 생성하여 english, korean 이라는 두개의 카테고리를 추가시킵니다.
- english 메뉴를 생성하여 en-sample01, en-sample02와 같은 영문용 카테고리를 추가시킵니다.
- korean 메뉴는 english와 마찬가지로 국문에서 사용할 kr-sample01, kr-sample02 카테고리를 추가시킵니다.

![메뉴 ‹ WP-DEMO — 워드프레스](https://farm8.staticflickr.com/7708/16968481908_3f14851d56_o.png)
위의 예시는 language 메뉴입니다.

![메뉴 ‹ WP-DEMO — 워드프레스](https://farm8.staticflickr.com/7674/17154647482_93ea08a103_o.png)
위의 예시는 english에 en-sample01, en-sample02를 추가시킨 상태입니다.

### Step 04 사이드바에 표시방식 지정

네번째로 외모 &gt; 위젯 &gt; 사용자 정의 메뉴를 추가하여 해당 카테고리에서 표시할 메뉴세트를 지정하는 방식으로, english를 예로 설명해 보겠습니다.

- 사용자 지정메뉴를 표시시키고자 하는 사이드바나 푸터를 지정
- 메뉴 선택: english를 선택
- 공개설정 - 보이기
- 선택하기 - 카테고리 선택
- english에서 사용될 en-sample01을 선택
- 추가하기 - 카테고리 선택 - en-sample02를 선택

이상의 방법으로 english쪽에서 보여져야 할 메뉴를 카테고리 또는 페이지를 지정하여 해당영역에서만 보이게끔 하는 방법입니다.

![위젯 ‹ WP-DEMO — 워드프레스](https://farm9.staticflickr.com/8793/16536100203_96d8115274_o.png)
이렇게 의외로 쉽게 화려(?)하진 않지만 다국어서비스가 가능해집니다.

### Step 05 첫페이지 지정

이방식의 유일한 단점이라고 생각되는 부분은 첫페이지에 있습니다. 이미 언급했듯이 Option 2의 경우, Option 1과 같은 One Blog입니다. 등록되는 포스트는 하나의 블로그에서 관리되고 있는거죠. 즉 시간순으로 글이 저장되기 때문에 첫 페이지, 처음 접속하는 사람의 언어에 최적화된 페이지를 보여주지 못하게 됩니다. 그래서 어쩔 수 없이 Static Post형식을 취해야 합니다. 즉, 고정페이지를 두는거죠. 흔히 사용되는 About페이지 정도가 무난하겠죠?

![설정 ‹ WP-DEMO — 워드프레스](https://farm8.staticflickr.com/7685/16987116850_65dbe3994e_o.png)
설정 &gt; 읽기 &gt; 전면 페이지 : 기본값을 최근 글에서 정적인 페이지로 변경후에 보여줄 페이지를 지정

### 글작성시 주의점

Option 2의 방식으로 글을 작성할때의 주의할점이 한가지 있습니다. 글 작성시에 카테고리를 잊지말고 해당 카테고리선택을 해 두어야 한다는 것입니다. 영문을 예로 들어보면 en-sample01에 작성하는 글일 경우, english도 같이 선택을 해 주어야 한다는 겁니다.

### 기타..

누군가는, 웹일을 조금 해보신 분들은 이쯤에서 iframe을 사용해서 Page를 만들고 최신글등을 보여주거나 하는 방식으로 꾸미면 되지 않겠느냐는 발상을 할 수 있을것이라 생각됩니다. 예.. 그래서 해볼려고 했더니 무시되더군요. 어쩌면 당연한 조치이긴 합니다. 다시 [本家에서 제공되는 가이드](https://en.support.wordpress.com/code/)를 확인해보았습니다. 아래 태그가 .com에서 활용가능한 HTML Tag목록이니 참고하시기 바랍니다.

<blockquote><b>HTML Tags</b>

WordPress.com allows the following HTML code in your posts, pages, and widgets:

address, a, abbr, acronym, area, article, aside, b, big, blockquote, br, caption, cite, class, code, col, del, details, dd, div, dl, dt, em, figure, figcaption, footer, font, h1, h2, h3, h4, h5, h6, header, hgroup, hr, i, img, ins, kbd, li, map, ol, p, pre, q, s, section, small, span, strike, strong, sub, summary, sup, table, tbody, td, tfoot, th, thead, tr, tt, u, ul, var</blockquote>
위 Tag 리스트에 등록되어 있지 않은 Tag들은 기본적으로 보안 문제상 지원하지 않고 있습니다.

<blockquote>embed, frame, iframe, form, input, object, textarea</blockquote>

## Option 3: Two Blogs

어찌보면 가장 당연한 방식입니다. 각 언어용으로 블로그를 따로 운영하는 방식이죠. 관리면에서 살짝 귀찮을 수는 있지만, 해당 언어별로 URL을 지정해두면 접속한 유저도 편하게 사용가능하진 않을까요?
URL도 서브도메인을 각 언어에 맞게끔 지정해 두면 다국어 지원에 제일 합당한 방식이라 생각되기도 합니다. 그저, 단점이라면... 언어별로 관리자가 있어야 무난한 운영이 가능할것 같다는 생각이 들기도 합니다. 사정상 혼자서 운영해야 한다면 그나마 Option 2가 무난할거라 생각되는군요.

![Screen](https://farm9.staticflickr.com/8690/17166298622_1c3fb279db_o.png)
language가 실제 블로그에서 보이는 화면의 예시이며 [이쪽](https://thisisdemosite.wordpress.com/)에서 확인 가능합니다.

**참고:**

- [https://en.support.wordpress.com/set-up-a-multilingual-blog/](https://en.support.wordpress.com/set-up-a-multilingual-blog/)
- [https://en.support.wordpress.com/code/](https://en.support.wordpress.com/code/)
