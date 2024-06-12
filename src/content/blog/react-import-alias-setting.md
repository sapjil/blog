---
title: import에 상대경로대신 절대경로를 사용하고 싶었다
pubDate: 2023-10-14
tags: ['blog', '리액트', 'react', 'jsconfig.json', '별칭']
description: import에 절대경로를 사용하기 위한 jsconfig.json 설정. Simple is Best.
categories: react
heroImage: https://live.staticflickr.com/65535/53786731980_9e364eb565_o.png
---

리액트를 공부하고 프로젝트에서 경험을 하면서 마주하게 되는 것 중에 import 할때 `../../polder/path/`처럼 상대경로가 지정되는 경우가 있다. 페이지에 불러오는 것이 몇개 없을때면 크게 상관 없는데 컴포넌트가 많아지다 보면 여간 어지럽고 보기에 흉한 경향이 있다(?)

그래서, 대체로 `@`나 `~`로 `root` 경로를 지정해서 깔끔하고 쌈빡하게 보여주는게 좀 있어 보이는(?) 것 같아 작업할때 도입하려고 했던 공부에 대한 기록이고 결론부터 말하자면 난 `jsconfig.json` 설정으로 100%는 충족시키지 못했지만 나름 만족스러운 결과를 얻었다.

## Auto Import - VSCODE Extension

우선 최근의 어지간한 환경은 거의가 VSCODE를 사용하고 있을 거라 생각된다. 파일명을 입력하면 자동으로 import를 시켜주니 경로를 찾는 부담이 줄어든다. 필수 설치 추가기능이 아닐까.

[auto-import](https://marketplace.visualstudio.com/items?itemName=NuclleaR.vscode-extension-auto-import)

## jsconfig.json로 설정

개인적으로 현재 내 작업환경을 생각하면 이 이상의 시간을 들이는 것이 무의미한 것 같아 최종으로 결정한 방법은 가장 심플한 방법이다.

```json
// jsconfig.json
{
  "compilerOptions": {
    "baseUrl": "src"
  },
  "include": ["src"]
}
```

이렇게 적용시킬 경우 결과는 다음과 같이 나오게 된다. 가장 근본적인 방법인것 같다.

```js
// 적용 전
import Sample from '../Components/Sample';

// 적용 후
import Sample from 'Components/Sample';
```

## ETC.

시도했던 방법 중 한가지도 나쁘지 않았는데.. 이상하게 설정이 적용되었다 풀렸다해서 포기했다.

```json
// jsconfig.json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"],
      "@Components/*": ["./src/Components/*"],
      "@Pages/*": ["./src/Pages/*"],
      "@Views/*": ["./src/Views/*"]
    }
  },
  "include": ["src"],
  "exclude": ["node_modules"]
}
```

paths에 `"@/*": ["./src/*"]`를 추가시키면 `@/Components` 처럼 표기된다.

```js
// 추가시키기 전
import Sample from '@Components/Sample';

// 추가시킨 후
import Sample from '@/Components/Sample';
```

가상경로에 대한 검색을 했을 때 가장 많은 검색결과는 단연 `craco`였다. 처음엔 나도 이걸로 이리저리 해 봤지만 뭔가 틀렸다... 이리저리 해보다 버리는 수로 결정. 아직 이런걸 건드리기엔 많이 부족하다는 것을 알았다.

## record 13

### 기초가 중요하다.

이번 설정을 건드려 보며 느낀건 기본도 없이 해석도 잘 되지 않는 인터넷상의 정보를 보면서 따라해봐야 큰 의미가 없다는 거였다. 불필요한 삽질만 죽어라 한듯하다.
