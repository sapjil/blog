---
title: 리액트에서 '\n' 줄바꿈 방법
pubDate: 2023-04-22
tags: ['blog', '리액트', 'react', 'component', 'white-space', '줄바꿈']
description: 리액트에서 '\n'로 줄바꿈이 적용되지 않을때 해결 방법.
categories: react
---

## 리액트 텍스트 줄바꿈 문제

리액트에서 줄바꿈 된 내용을 어떻게 해결하면 좋을까.
`<br>`을 사용하면 쉬울 줄 알았지만.. 그대로 `<br>`이 함께 나오니 해결 방법을 찾아야 했다.

`dangerouslySetInnerHTML`이란걸 사용하면 해결 될까 싶었지만, 이건 접근 방향이 틀린것 같다.
이 방법은 공식 사이트에서도 보안상 주의가 필요하다고 하는 만큼 넘기는 것이 좋을 것 같다.

> dangerouslySetInnerHTML은 브라우저 DOM에서 innerHTML을 사용하기 위한 React의 대체 방법입니다. 일반적으로 코드에서 HTML을 설정하는 것은 사이트 간 스크립팅 공격에 쉽게 노출될 수 있기 때문에 위험합니다. 따라서 React에서 직접 HTML을 설정할 수는 있지만, 위험하다는 것을 상기시키기 위해 dangerouslySetInnerHTML을 작성하고 \_\_html 키로 객체를 전달해야 합니다.

```code
{
	text: '텍스트 줄바꿈<br>텍스트 줄바꿈'
},
{
	text: '텍스트 줄바꿈\n텍스트 줄바꿈'
}
```

기본적으로 `<br>`을 사용하면 그대로 <br>까지 포함된 텍스트로 표시된다.

```code
텍스트 줄바꿈<br>텍스트 줄바꿈
```

## white-space 사용

해결 방법은 CSS의 `white-space` 속성을 사용해서 해결 가능하다.

```css
white-space: pre-wrap;
white-space: pre-line;
```

둘 중에 하나를 사용하면 `\n`을 사용한 곳에서 제대로 줄바꿈이 적용된다.

```code
텍스트 줄바꿈
텍스트 줄바꿈
```

[MDN:white-space](https://developer.mozilla.org/ko/docs/Web/CSS/white-space)
