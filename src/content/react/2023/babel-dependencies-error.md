---
title: babel dependencies 문제
pubDate: 2023-10-09  15:21:22
tags: blog, 리액트, react, babel, dependencies, error
description: 거의 모든 문제의 해결법은 인터넷에 공개되어 있다.
---

## babel dependencies

설치 및 테스트 과정에서 `babel dependencies` 처럼 라이브러리 종속 관련 문구가 보일 경우가 있다.

```js
One of your dependencies, babel-preset-react-app, is importing the
"@babel/plugin-proposal-private-property-in-object" package without
declaring it in its dependencies. This is currently working because
"@babel/plugin-proposal-private-property-in-object" is already in your
node_modules folder for unrelated reasons, but it may break at any time.

babel-preset-react-app is part of the create-react-app project, which
is not maintianed anymore. It is thus unlikely that this bug will
ever be fixed. Add "@babel/plugin-proposal-private-property-in-object" to
your devDependencies to work around this error. This will make this message
go away.
```

해결법은 라이브러리를 하나 추가시키면 가능하다.

```js
npm install --save-dev @babel/plugin-proposal-private-property-in-object
```

## record 12

### 알아야 한다.. 사소한 것도

거의 모든 문제의 해결법은 인터넷에 공개되어 있다. 이걸 잘 찾느냐 못 찾느냐로 나의 시간을 얼마나 줄일 수 있는지가 판가름 난다. 검색도 능력이다.
