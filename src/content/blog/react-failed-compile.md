---
title: 컴파일 실패
pubDate: 2023-03-13  14:45:25
tags: blog, 리액트, react, Failed to compile, WebSocket
description: Failed to compile라면서 컴파일 관련 에러가 나왔을 때 확인해야 할 사항
---

## Failed to compile.

![failed-compile-00](https://live.staticflickr.com/65535/52744562879_a03f58c97e_z.jpg)

`Failed to compile`에러가 발생했다. 이유가 뭐지? 이리저리 계속 찾아봐도 모르겠더라. 보고 있는 책에서도 별다른 언급도 없고. 판단 가능한 이유는 현재 버전과 다른, 이전 버전의 예제를 보면서 따라 해서 그런 건가 생각된다.

급변하는 속도를 따라가지 못한 후발주자의 어려움이겠지.. 우선은 Failed to compile 부터 차분히 접근해 가자.

```
Failed to compile.

Attempted import error: './App' does not contain a default export (imported as 'App').
ERROR in ./src/index.js 12:33-36
export 'default' (imported as 'App') was not found in './App' (possible exports: App)

webpack compiled with 1 error
```

## 문제였던 부분

지금까지 리액트를 공부하면서 `App.js`에서 보게 된 케이스가 몇 가지 있는데(더 있을까?)

1. `function`로 활용(App.js)

```
function App() {}
```

3. `const`로 활용(App.js)

```
const App = () => {}
```

3. `export`로 활용(App.jsx)

```
export const App = () => {}
```

여러 가지 문제로 동일한 에러가 나올 수 있겠지만, 이번 문제는 3번 형식으로 작업했을 경우에 생긴 문제였다. 뭐 방법의 차이일 것이고 초기 프로젝트 환경을 세팅한 사람의 경험치에 따라서 달라지는 부분이니 이런건 케바케로 몸으로 익히는 것 말고는 방법이 없을 것 같다.

## 해결법

해결법은 메시지에 나와 있는 그대로였는데 `'./App' does not contain a default export`
번역해 보자면.. "**App에 기본 내보내기가 포함되어 있지 않다.**"인데 결국, 문제는 나의 영어 실력 만으로는 해결되지 않는 import, export의 개념적인 문제가 진짜 문제였던 것.

문제의 원인을 다시 보자면...

```
export const App = () => {}
```

`App.jsx`에서 `export const App`으로 export를 시킨 걸 사용하려면 `import App from`이 아니라
`import {App} from`처럼 사용해야 하는 거였다.

## 어라, 그런데 또 WebSocket 에러?

에러는 해결했는데 또 WebSocket 에러가 나오면서 무한정으로 에러를 보내고 있었다.
이번엔 포트 문제가 아니었는데 이전에 경험했던 것이 있어서 빨리 대처가 가능했다.
역시 실수는 사람을 성장시키는 것 같다.

`WebSocket connection to 'ws://127.0.0.1/' failed:`

이번에도 `WDS_SOCKET_PORT`을 먼저 적용해 봤지만 실패. 두 번째로 `react-script` 버전을 v5.0.1에서 v5.0.0으로 내려주니 제대로 동작하는 것을 확인 할 수 있었다.

## 참고

- [qiita.com](https://qiita.com/keita_ogawa/items/356f3f2e7f8679ee5146)
- [teratail.com](https://teratail.com/questions/332113)
- [react.sapjil.net](/port-error/)

## record 3

### 정말 하나부터 열까지 모르는 것투성이다.

어떤 곳은 그냥 `.js` 확장자를 사용해서 진행하는데 또 어떤 곳은 `.jsx`를 기준으로 설명을 진행한다. 어떤 것이 맞는 건지 학습자 입장에서는 어렵다. 이것도 프로젝트 리더에 따라 다른 거겠지? 통밥으로 점쳐보자면 최근에는 `.jsx`를 더 사용하는 추세인 것 같아 보인다. 아님 말고.
