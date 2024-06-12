---
title: Nunjucks + beautify + tailwind + imagemin를 적용한 Gulp 5 설정 관련 기록
pubDate: 2024-06-11
tags:
  [
    'Gulp',
    'Gulp 5',
    '설정',
    'tailwind',
    'tailwindcss',
    'tailwind warn content',
    'imagemin',
    '이미지 파손 에러 해결',
    'csscomb',
    'Nunjucks',
    'nunjucks-render',
		'pretty-html',
    'beautify',
		'stylelint',
		'stylelint recommended',
  ]
description: 지적호기심으로 작업하고 있는 Gulp세팅. Gulp를 5로 설정하며 Nunjucks + beautify + tailwind + postcss + imagemin를 설정하여 마크업 환경을 최대한 편하게 자동화하기.
categories: gulp
heroImage: 'https://live.staticflickr.com/65535/53784308163_917bd2a5ff_o.png'
---

<!-- <img src="https://live.staticflickr.com/65535/53784308163_f10aa8426f_o.png" width="1024" height="640" alt="title_gulp"/> -->

## 간만의 Gulp 업데이트

최근 몇 년간 VSCODE 확장툴이 잘 나와서 굳이 Gulp까지 사용하지 않아도 풀리는 경우가 많았기에 실제 프로젝트에서 활용하기보다는 지적호기심을 채우는 목적으로 Gulp 설정을 작업하고 있는 중이지만, 실용성 위주로 최대한 자동화를 목적으로 하고 있다.

최근 프로젝트가 연이어 리액트를 사용했기 때문에 한동안 Gulp를 제대로 들여다보지 않고 있었다. 지금 참여 중인 프로젝트에서 시작하자마자 약 2주 정도 달려서 급한 불은 일단락되었기에 언제 또 사용하게 될지 모를 Gulp를 정비하기 위해 프로젝트를 열어봤는데 그 사이 **Gulp가 5로 업데이트** 되어있었다. 그래서, 그동안 image 압축을 적용시키지 못하고 있었던 **imagemin** 적용과 여기저기서 많이 사용되고 있는 **tailwind**도 함께 적용해 보기로 했다.

이번에 가장 큰 변화는 `const` 에서 `import` 형식으로 바뀐 게 가장 큰 차이점이라 생각된다.

```js
// "gulp": "^4.0.2",
const gulp = require('gulp');

// "gulp": "^5.0.0",
import gulp from 'gulp';
```

## Nunjucks + beautify 도입

기존에는 gulp-file-include를 사용하여 include 기능을 적용시키고 있었다. 이 기능을 처음 알게 되었을 때도 신세계였는데 당시에는 Mustache문법이 익숙하지 않아 패스했던 Pug 등을 사용할 생각을 못했었는데 그 사이 조금은 익숙해졌기에 이번에 Nunjucks을 설치하기로 했다.

기존에는 따로 문법에 대해선 크게 신경을 쓰지 않고 있었는데 이번에 htmlhint를 반영시켜 두었다. html생성에는 gulp-file-include만 사용을 했었고 include시 들여 쓰기가 정리되지 않는 문제는 그냥 무시하고 있었는데 lint 쪽으로 찾아보니 pretty-html(js-beautify)가 있어 적용을 해보게 되었다.

### gulp-nunjucks-render

모질라에서 만든 템플릿. html문법을 그대로 사용 가능하며 `{% block contents %} ... {% endblock %}` 형식으로 사용하며 if, for 등도 사용 가능하기 때문에 다양한 작업이 가능하다.

### gulp-pretty-html

include 되는 파일은 들여 쓰기 문제가 남아있다. 이런 문제를 해결해 주기 위해 js-beautify를 사용하여 `.njk`에서 `.html`로 저장 시, 정렬을 깔끔하게 해 준다.

<details>
<summary>nunjucks + pretty-html</summary>
<script src="https://gist.github.com/sapjil/057b0ff828d942c1c5269ecd4605051e.js"></script>
</details>

## SCSS 주변정리 + tailwind 도입

버전 5에서는 이전에 적용시켰다가 제외시켰던 postcss, stylelint를 다시 적용 시켜두었다. postcss는 tailwind, stylelint를 적용시키는데 필요해서 추가시킨 케이스.

### stylelint

CSS 작업시 나올 수 있는 오류사항들을 체크해 주고 문제 되는 지점을 알려준다. `.stylelintrc.json`에는 standard가 아니라 recommended를 설치하고 tailwindcss와의 궁합을 위해 stylelint-config-tailwindcss/scss도 설치를 해 주었다.(standard 설치 시 tailwindcss와의 궁합이 좋지 않았다.)

```json
"stylelint-config-recommended",
"stylelint-config-recommended-scss",
"stylelint-config-tailwindcss/scss"
```

### tailwind

HTML에 직접적으로 클래스명을 길게 작성하는 방식은 호불호가 가리게 되지만, 작업하다 보면 익숙해지는 부분이 있다. 특히 컴포넌트 단위 작업을 위주로 하는 React, Vue계열은 이러한 부분이 거의 신경 쓰이지 않는 수준이라 생각된다. HTML생성에 Nunjucks를 사용하면서 유사한 작업이 가능하기에 일단 도입해 두기로 했다.

이번 작업에서 가장 시간을 잡아먹은 곳이 tailwind 설정이었는데 `postcss.config.js`도 `tailwind.config.js`의 경로 설정도 문제가 없음에도 CSS는 반영이 되는 것이 확인되는데 HTML에서 적용시키면 반영이 되지 않는 반쪽짜리 엉성한 tailwind였다.

> warn - The `content` option in your Tailwind CSS configuration is missing or empty.

초반, `content` 에러를 조우하게 되니 `tailwind.config.js`에서 계속 경로만 검토하고 또 검토하고 바꿔보고 별 난리 부르스를... 반쪽짜리라는 점에서 빨리 눈치를 챘어야 했는데..

Gulp의 설정에서 하기 코드처럼 njk, css를 동시에 바라보면서 html과 scss를 순차적으로 랜더링 하고 브라우저를 리로드 시켜주면 해결되는 문제였다. 조금 머리를 식히고 바라보니 너무 가까운 곳에 답이 있었다는.. 머리 나쁘면 고생한다더니..

```js
gulp.watch(
  [paths_src.njk, paths_src.css],
  series(compileSass, html, browserReload)
);
```

<details>
<summary>scss + tailwind</summary>
<script src="https://gist.github.com/sapjil/6ec21e0aff4a43c45b804b1f15c1f35d.js"></script>
</details>

## imagemin 도입

이미지 용량은 줄일수록 좋은 게 기본이다. 이전에는 매번 이미지를 열어서 압축률을 확인하면서 작업을 했었는데 갈수록 인터넷 속도도 빨라지고 있고 점점 이미지 용량을 신경 쓰는 사람들은 거의 없어지고 있는 기분이 든다.

gulp 특성상 저장 시 매번 이미지를 압축하는 불필요한 동작이 발생하는 부분을 회피하기 위해 기본적으로는 이미지를 복사하는 태스크를 반영하고 이미지 압축은 별도 명령어로 관리하는 설정으로 작업했다. PNG의 압축률에 해당하는 `optimizationLevel` 옵션이 올라갈수록 압축에 걸리는 시간이 꽤 소요되어서 1로 설정을 해두고 있다.

imagemin도 버전문제인지 Gulp4에서는 답을 찾지 못해 방치하고 있었던 녀석이라서 이번에는 꼭 적용시켜 두고 싶었다. 이번에는 설치는 되었고 동작도 잘하는 것처럼 보였지만, 압축된 이미지를 확인할 수 없는 문제가 있었다. 이미지 용량이 오히려 배가 되고 썸네일도 확인 불가하고 이미지 자체를 열어 볼 수 없는 파손된 상태였음. 해당 문제는 gulp5의 [changelog](https://github.com/gulpjs/gulp/issues/2777#issuecomment-2036776560)에 답이 있었는데 `.src`에 `{ encoding: false }`를 추가시켜 주면 되는 문제였다.

```
.src(paths_src.image, { encoding: false })
```

<details>
<summary>imagemin</summary>
<script src="https://gist.github.com/sapjil/9c7d9f2b72168cacd566d6a00722bb81.js"></script>
</details>

## 남은 과제

큰 틀에서는 일단 기능적용은 일단락되었지만 현시점, 2가지 과제가 남은 것 같다.

- 폐쇄망 프로젝트에서도 사용가능하도록 offline 패키지 작업. 기존 작업물은 잘 동작하는데 새로 작업한 것들이 동작하질 않고 있다.
- 그동안 잘 동작하던 csscomb와 tailwind를 설치하니까 충돌하면서 프로세스가 종료되어 버린다. csscomb와 stylelint의 문제인지 tailwind와의 문제인지는 좀 더 만져봐야 알 수 있을 것 같다.

## 참고

https://qiita.com/nao_t/items/56d1d5859374fe58da03
