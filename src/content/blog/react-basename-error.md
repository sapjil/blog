---
title: (error) Cannot destructure property 'basename' of 'react~~.useContext(...)' as it is null.에러가 나왔을 때
pubDate: 2023-06-10
tags: ['blog', '리액트', 'react', 'js', 'error', 'basename', 'useContext']
description: Cannot destructure property 'basename' of ... 관련 에러가 나올때 대응법
categories: react
---

## basename property 관련 에러

> Uncaught TypeError: Cannot destructure property 'basename' of 'react**WEBPACK_IMPORTED_MODULE_0**.useContext(...)' as it is null.

## 발단

열심히 공부중인데 갑자기 에러가 나오면 당황스럽다. 또 내가 뭘 잘못한 것인가 싶어서.. 사무실에서 공부하며 진행했던 코딩을 복기를 위해 동일하게(?) 해보던중에 에러가 나오니 더 당황스러울 밖에..

![basename-error](https://live.staticflickr.com/65535/52963185299_a1a7d7404b_c.jpg)

## 발견

에러가 발생시점을 찾기 위해 원복을 시키면서 발견한 건 `<Link>`를 사용하면서다. 그럼 `Route`와 관련 있는 것 같다.

사무실과 집에서 차이가 있다면 결국 근본적으로는 버전 문제인것 같은데 아직 그 근본적인 이유까지는 알 수 없는 수준이라서 일단 구글링. 문제 해결 방법은 [stackoverflow](https://stackoverflow.com/questions/75728532/uncaught-typeerror-cannot-destructure-property-basename-of-react2-usecontext)를 통해 확인할 수 있었고 `index.js`에 `BrowserRouter`를 추가해주면 되는 거였다.

## 해결

문제가 되던 초기 코드는 다음과 같았다.

```jsx
// index.js
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

그리고 정상 작동하는 수정된 코드.

```jsx
// index.js
root.render(
  <React.StrictMode>
    <BrowserRouter>
      {' '}
      // BrowserRouter 추가
      <App />
    </BrowserRouter>
  </React.StrictMode>
);
```

`BrowserRouter`로 감싸주니 해결되었다. 이로서 에러 해결 능력 스킬 +1
