---
title: Gridsome을 Git Action으로 GitHub Pages에 배포하기
pubDate: 2020-01-13
tags:
  [
    '블로그',
    '변경',
    'Gridsome',
    'Git Action',
    '헥소',
    'hexo',
    'GitHub',
    'GitHub Pages',
  ]
description: Git Action을 사용해서 Gridsomse을 GitHub Pages에 배포하는 과정을 다루고 있습니다. 새해를 맞이해서 Vue에 대해 공부해보겠다는 욕심으로 블로그를 hexo에서 Gridsome으로 변경해보면서 정리한 내용입니다.
categories:
  - www
# heroImage: '/blog-placeholder-1.jpg'
---

**개발적인 지식이 모자라기 때문에 인터넷 뒤져가며 찾아본 거라 중구난방인 부분이 있습니다. 이 코드가 왜 필요한지에 대한 부분까지는 이해하지 못한 상태에서 문제를 해결해나갔다는 점은 인지해 주셨으면 합니다.**

![Gridsome + Git Action + GitHub Pages](https://live.staticflickr.com/65535/49387463722_f6f1e97ce0_c.jpg)

**table of contents**

- Hexo에서 Gridsome으로
- Front Matter 수정
- URL 설정
- Disqus 추가
- Source Code
- Page Title
- 404 page
- Github Action
- 남은 과제

## Hexo에서 Gridsome으로

어쩌다 보니 새해 첫 글이 되었네요.. 얼마 전에 [Gridsome](https://gridsome.org/)이라는 녀석을 알게 되었습니다. [Vue](https://vuejs.org/)를 기반으로 정적 html을 생성하는 프로그램인데요.

이쪽에 관심이 생기면서부터 이것저것 기웃거리고 있는데 예전 프로젝트에서 Vue를 접해 보고 마음에 들어하고 있었습니다. 단지 당시에는 Vue를 사용한 블로그가 가능한 프로젝트를 못 찾았었는데 이번에 Gridsome이란 것을 알게 된 것이죠. 아직까지 버전(현재 v0.7.12)이 v0.x 인걸 보면 메이저 업데이트까지는 아직 되지 않은 것 같지만 제가 쓰기에는 충분하고도 남는 기능들이라 보여서 선택에 무리는 없었습니다. 갈수록 좋아질 것이 기대됩니다.

현재 블로그도 Gridsome을 공부하면서 개량을 해나가면서 사용해보는 중간 과정중의 결과물입니다. Gridsome에서 제공되는 [Starter](https://gridsome.org/starters/)가 있기 때문에 쉽게 전체 기능이 제공되는 것을 사용하는 것이 쉬운 방법이긴 한데요. 그냥 조금씩 공부하면서 이것저것 추가시켜 나가는 방법을 사용해 보기로 했습니다. [hexo](https://hexo.io/)에서 뭔가 재미를 느끼지 못한 부분도 하나의 이유이긴 합니다.

## Front Matter 수정

그동안 사용했던 hexo의 Markdown 파일에서 사용하던 [Front Matter](https://hexo.io/ko/docs/front-matter.html)를 그대로 사용하는 것이 가장 좋은 것 같아서 우선은 가장 기본적인 것만 사용하며 추가가 필요한 부분은 나중에 하기로 했습니다.

기본 설정으로는 **Invalid date** 라고 출력되며 에러가 나오거나 컴파일이 멈추어 버리는 경우도 있어서 확인을 해보니 `date`의 값 문제인 것을 알고 '시:분'을 제거하여 '년-월-일'만 남게끔 수정해서 문제를 해결했습니다.

만일 동일한 날에 한 개 이상의 포스팅을 했을 때 어떤 식으로 정렬되는지(아마도 알파벳순?) 모르겠지만 현재로선 하루에 한 개 이상 포스팅할 일은 전무하기 때문에 시:분은 쭈욱~ 사용하지 않을 것 같습니다.

<iframe width="100%" height="230" src="//jsfiddle.net/minamiland/vhdLtjx9/embedded/html/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

기존 hexo에서 사용하던 `tags` 와 `categories`는 hexo 방식을 그대로 두어도 에러가 나오지 않기에 우선은 방치해 두고 적용시키는 방법은 업데이트해 보려 하고 있습니다. 뭔가 새로 글을 쓸 때마다 고민되기도 하고 새로 만들기도 해야 하는 등 분류작업 자체도 고민이 되는 경우가 있어서 카테고리를 아예 없애는 방법도 고민해 보고 있는 중입니다.

## URL 설정

Front Matter에 `:slug`값을 추가시킬까 하다가 hexo에서 사용하던 방식을 그대로 사용하기 위해(`.md`파일명을 그대로 주소로 사용하는 방식) `gridsome.config.js`를 수정해 주었습니다. 이로서 기존과 동일한 퍼머링크를 가지게 된 것 같습니다.

<iframe width="100%" height="300" src="//jsfiddle.net/minamiland/n4dbkcw5/embedded/js/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

## Disqus 추가

댓글을 아예 없애는 방법도 고민을 하긴 했지만, 혹시나 하는 생각에 기존에 사용하던 [disqus](https://disqus.com/)를 그대로 유지하기로 했습니다. 다행히 인지도가 있는 만큼 Gridsome에서도 [disqus 설치 가이드](https://gridsome.org/docs/guide-comments/#install-vue-disqus)를 제공하고 있어 특별한 문제없이 설치를 마무리했습니다.

## Source Code

[gist](https://gist.github.com/)를 사용해 보려 했는데 플러그인을 설치하고 몇 가지 설정을 해줘도 제대로 작동을 하지 않아서 소스코드는 우선 [jsfiddle](https://jsfiddle.net/)을 사용, `iframe`을 적용하는 방법을 사용했습니다. 차후 문제점을 파악해서 성공하면 그때부터는 gist를 사용할 예정입니다.

지금까지 자주 사용하기도 했었던 [highlight.js](https://highlightjs.org/)를 사용하는 방법도 있긴 한데요. 뭐랄까, 자주 바꿔버리는(?) 문제로 매번 highlight.js를 인스톨시키거나 CDN 코드를 삽입해야 하는 약간의 번거로움이 있다는 것을 느끼고 있었습니다. 잊어버리고 있다가 나중에 설치한 적도 있고 해서 이제부터는 gitst 같은 서비스를 사용해서 어떤 식으로 바꿔도 문제가 없는, 굳이 신경 쓰지 않아도 되는 방향을 선택한 겁니다.

`iframe`이 좋지 않다는 지적도 있지만, 개인 블로그에서 그런 것까지 신경 쓸 필요가...

## Page Title

페이지 타이틀(`<title>`) 이 제대로 동작하지 않는 문제가 있어서 이 부분을 해결하기 위해 `Post.vue` 파일을 수정했습니다.

<iframe width="100%" height="200" src="//jsfiddle.net/minamiland/zd1e4ywu/embedded/js/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

## 404 page

build를 마치면 404 페이지가 만들어지긴 하지만 CLI 설치 후에 기본 설정으로만 Gridsome을 설치한 경우에는 404 페이지는 존재하지 않습니다. 가이드에 따라 `src/pages/`에 `404.vue`를 추가시켜주면 원하는 모양의 페이지를 만들 수 있습니다.

## Github Action

[Sapjil](https://sapjil.net) 블로그는 [Wordpress](https://wordpress.org/)에서 [Github](http://github.com/)로 이동해 온지 대충 1년 정도 되는 것 같습니다. 그 정도로 갱신을 하지 않았다는 거지만.. 무엇보다 따로 호스팅 비용을 필요로 하지 않아서 다행인 곳이죠. Gridsome으로 변경하기로 맘먹은 뒤 만드는 건 좋은데 동일하게 Github에서 사용 가능한가?라는 의문이 있었습니다. 당연히 가능하겠지만, 문제는 그 방법을 내가 혼자 해결할 수 있을까? 였습니다. 그때 생각난 것이 [GitHub Action](https://github.com/features/actions)이였습니다.

예전에 [GitLab](https://gitlab.com/)을 사용해서 [gitbook을 Firebase에 배포하는 과정](https://blog.minamiland.com/337)을 통해 삽질을 해본 적이 있어서 CI툴을 다루어 본 경험으로 또 삽질을 도전해 보기로 한 겁니다.

최근 들어 [Netlify](https://www.netlify.com/)를 많이들 사용하는 것 같아 보였는데요. 다음에 다른 작업으로 도전해 보기로 하고 우선은 GitHub에서 진행했습니다.

배포를 위한 설정은 다음과 같습니다.

- Event
- Checkout, Setup
- Gridsome CLI
- Npm Install, Build
- Deploy

### Event

처음엔 잘 이해가 되지 않았던 부분이 있었는데요. 테스트용으로 새로운 계정을 만들어서 페이지까지 만들어 내는 모든 과정을 마치고 났지만 정작 github.io 에 올리는 작업에 시간이 걸렸었습니다. 처음엔 이유를 잘 몰랐습니다만.. 작업 브런치를 기본적으로 `master`로 두고 있었기 때문이었습니다. 이 부분을 소스들이 있는 브런치(`source`)로 바꿔주고 나서야 모든 과정이 에러 없이 진행되었습니다.

<iframe width="100%" height="150" src="//jsfiddle.net/minamiland/huwvd1cy/1/embedded/js/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

### Checkout, Setup

뒤쪽에 `@v1`이 뭘 뜻하는지는 모르겠습니다만.. 대체로 작업 진행을 위해 미리 받아두는 요소들입니다. `with`로 node의 버전을 지정합니다.

<iframe width="100%" height="200" src="//jsfiddle.net/minamiland/d9r1wgzx/4/embedded/js/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

### Gridsome CLI

Gridsome 설치를 진행합니다.

<iframe width="100%" height="150" src="//jsfiddle.net/minamiland/owj6fm4L/embedded/js/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

### Npm Install, Build

Node를 인스톨하고 Build 까지의 과정입니다.

<iframe width="100%" height="250" src="//jsfiddle.net/minamiland/v7gat428/embedded/js/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

### Deploy

배포 과정입니다만 세어보니 이 과정만 대략 20번 정도는 실패를 한 것 같습니다.

![gridsome deploy error](https://live.staticflickr.com/65535/49386818038_b13e7453b1_c.jpg)

최종적으로는 [peaceiris/actions-gh-pages@v2](https://github.com/peaceiris/actions-gh-pages)라는 것을 사용했습니다. 실패를 계속하면서 몇 가지 다른 것들을 적용해보다가 이걸로 바꾼 뒤 문제가 잘 풀렸거든요.

<iframe width="100%" height="200" src="//jsfiddle.net/minamiland/ko4w3jrh/embedded/js/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

- 사용 중인 GitHub Page에서 `ACTIONS_DEPLOY_KEY`를 생성해서 적용합니다. 보안적인 문제도 있고 배포 과정에 필요한 과정입니다.
- `PUBLISH_BRANCH`에 `master`를 지정합니다. 이래야 `source`에서 `.md`파일을 등록(커밋)하면, Action을 통해서 일련의 과정을 거쳐서 `master`에 배포를 하게 됩니다.
- `PUBLISH_DIR`의 `dist`는 Gridsom에서 `build`를 하게 되면 생성되는 폴더입니다.

이상의 과정으로 굳이 오프라인에서 작업하지 않아도 Github에 접속이 가능만 하다면 언제나 블로깅이 가능한 환경이 조성되었습니다!!! 하면 어떻게든 되네요. ㅎㅎ

현재 설정으로는 `source` 브런치에서 어떤 파일이건 수정만 되면 무조건 `Deploy`과정까지 쭈욱 논스톱으로 진행한 후에 `master`브런치에 push를 해서 페이지를 업데이트시켜버립니다. 이 부분은 현재 딱히 신경 쓰고 있지 않습니다만 차후에는 바꿀지 생각해 봐야겠습니다.

## 남은 과제

배포하는 과정까지 문제없이 이루어졌으니 일단 기초 과제는 클리어한 것 같습니다. 이제 다음으로 해결해야 할 과제는 다음과 같은 정도가 아닐까 생각되네요.. Gridsome에서 제공하는 Stater를 직접 사용하지 않고 다른 Stater를 깔아보고 소스를 뒤져보면서 필요한 기능들을 추가시키는 과정을 통해 공부해 볼 예정입니다. 잘 될지는 모르겠지만..

- gist 사용을 위한 작업
- 리스트에 커버 이미지 표시
- tag
- category
- SCSS 적용
- ~~Google 관련(analytics, adsense)~~
- SEO 관련 설정(주로 meta 설정)

딴 건 모르겠지만 가장 맘에 걸리는 부분은 확실히 SEO 적인 부분입니다. 기본적으로 URL에 변화가 생기는 것은 아니지만 기존에 설정해 두었던 여러 자잘한 것들이 제대로 동작하지 않거나 아예 불가능할 수도 있기 때문에 그나마 어찌어찌 우연히 찾아오시던 분들도 못 들어오게 될까 하는 걱정이긴 하지만, 공부 부족으로 생기는 문제인 만큼 감내해야 할 부분인 것 같습니다.
