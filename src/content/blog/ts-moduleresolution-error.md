---
title: Did you mean to set the 'moduleResolution' option ... 에러와 조우하다.
pubDate: 2023-11-08
# updatedDate: 2023-11-08
tags:
  [
    'paths',
    '타입스크립트',
    'tsc',
    'typescript',
    'error',
    'moduleResolution',
    'nodenext',
  ]
description: 나의 첫 타입스크립트 오류, moduleResolution 설정으로 문제를 해결하다.
categories: typescript
# heroImage: '/blog-placeholder-2.jpg'
---

## 나의 첫 타입스크립트 에러

뭐 하나 제대로 익히고 있지 않으면서 조급한 마음에 이리저리 기웃거리고 있는 중이다. 인강을 따라하며 타입스크립트 입문을 시작했는데... 어찌 이리 에러와 자주 만나는지..

**Did you mean to set the 'moduleResolution' option to 'nodenext', or to add aliases to the 'paths' option?**

대충 `moduleResolution` 옵션을 설정하거나 `paths` 옵션에 aliases을 추가하려고 했냐는 질문같은데.. 그래서 어쩌라고..

## 해결방법

이리저리 검색하다 발견한 해결책, `tsconfig.json`에 하기 설정을 추가해 주면 해결 된다는 것을 알았다.

```ts
"moduleResolution": "node"
```

답을 구하고 나서 에러를 다시 보니 이해가 된다. 결국 moduleResolution 옵션 설정이 필요하다는 것이었으니까.

## 참고

https://github.com/microsoft/TypeScript/issues/35876
