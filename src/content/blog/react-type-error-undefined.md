---
title: TypeError Cannot read properties of undefined
pubDate: 2023-10-22
tags: ['blog', '리액트', 'react', 'TypeError', 'undefined', '에러']
description: 아 놔.. TypeError Cannot read properties of undefined는 또 뭐냐고
categories: react
heroImage: https://live.staticflickr.com/65535/53786731980_9e364eb565_o.png
---

```
TypeError: Cannot read properties of undefined
```

공부하는 중에 에러가 나왔다.

## 원인

원인은 다음과 같은 코드에 대해 `id`를 찾지 못하겠다고 화를 내는 건데.. 나한테 왜...?

```
useEffect(() => {
	setActiveItem(list[0].id)
}, [list])
```

```
Uncaught TypeError: Cannot read properties of undefined (reading 'id')
```

기본적으로 내용을 추가하고 로컬스토리지에 담고 가져오고 등등은 전혀 문제가 없지만, 리스트를 모두 초기화하고 백지상태에서 페이지에 접근하면 에러가 난다는 것이다. 뭔가 억울하다. 열심히 따라한 것뿐인데 강의는 초기상태로 돌린 뒤로의 재실행까지는 하지 않고 끝났단 말이지.

## 해결

언제나 그렇듯이 초심자는 구글 선생을 통해 답을 찾는다. 해당코드에 대해 조건문을 하나 적용해 주면 해결된다는 것을 알았다.

```
useEffect(() => {
	if (typeof list[0] !== 'undefined') {
		return setActiveItem(list[0].id)
	}
}, [list])
```

이로써 문제가 하나 해결되었다. 자축.

## 해결은 해결인데..

해결된 내용을 조금 생각해 보게 되었다.

- 해당코드...어쨌든 첫 번째 것을 찾아서 표시한다는 뜻인데.
- 표시할 아무것도 없으면 당연히 찾을 수 없게 되는 상태인 거겠지?
- 그럼 그 상태를 해결해주는 코드를 작성하면 된다는 것이고
- 결국 `type`과 `undefined`에 대한 이해가 되어 있어야 한다는 결론이 나오게 될 것 같다.
- `length`도 답이 될 수 있을것 같은데..
- 평소의 내 사고 방식으로 유추해 보면 `type`보다 `length`에 집중했을 것 같다. 결론적으로는 `list.length !== 0`로도 동일하게 문제가 해결된다는 건 확인을 할 수 있었다.

검색을 해서 문제를 해결하는 것도 좋은데 이런 사고의 전개를 체득하는게 더 중요할지도 모르겠다.

## record 14

### 갈길은 멀고 할 일은 많고, 해보고 싶은 것도 많은데... 하기는 왜 이리 ~~싫은지~~힘든지

인간의 간사한 마음이 하루종일 괴롭힌다. 스마트폰에 빠져 공부는 뒷전. 어제는 오래간만에 토요 스터디에 참가하려고 했는데 외출했다 들어오면서 갑자기 식은땀과 복통이 생겨서 급하게 볼일 보고 집에 들어와선 스터디 참가를 포기했다. 공부를 하기 싫은 것이었던 것인가... 하는 착각이 들었다.

겨우 맘을 추스르고 인강 공부를 했는데 잘 따라 하며 잘 만들었는데 마지막 확인하는 과정에서 튀어나온 에러가 공부를 강제시켰다.
어떻게든, 뭐든 하게는 되는구나..
