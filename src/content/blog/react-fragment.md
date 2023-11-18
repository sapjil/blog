---
title: React.Fragment
pubDate: 2023-10-24
tags: ['blog', '리액트', 'react', 'fragment', 'map', 'array']
description: React.Fragment로 key 관련 에러에서 빠져나오자
categories: react
---

## key 관련 에러

`key`와 관련된 에러는 자주 출몰한다. 그리고 해결도 쉬운 편이고 해당 에러는 대체로 다음과 같은 내용을 담고 있다.

> Each child in an array should have a unique "key" prop. Check the render method of KeyTrap.

> Encountered two children with the same key, Child keys must be unique

대충 다음과 같은 방식으로 `map`을 사용하여 배열을 나열시킬 경우 유니크한 `key` 값을 지정할 필요가 있음을 상기시켜주는 내용이다.

```js
const dummyItem = [{ name: 'Mr.Hong' }, { name: 'Mr.Park' }];
```

다음과 같이 작성하면 문제가 되지만,

```js
<div className='box'>
  {dummyItem.map((item) => (
    <div>
      <span>{item.name}</span>
    </div>
  ))}
</div>
```

`key`를 지정해주면 문제는 해결된다. 심플한 방법으로 `index`를 추가시켜서 잡아주는 방식도 있는데 이건 다들 추천하지는 않는편이라 보여지는데 유니크한 `id`의 경우 수정과 정렬이 용이한 반면, 단순 `index`의 경우는 유니크한 기준이 약해서 문제가 발생할 소지가 크다.

```js
<div className='box'>
  {dummyItem.map((item, index) => (
    <div key={index}>
      <span>{item.name}</span>
    </div>
  ))}
</div>
```

## key 관련 에러 해결법 1

결국 유니크한 값을 지정해 주기 위해 `id`를 추가시켜서 유니크한 값을 제공해주면 된다.

```js
const dummyItem = [
  { id: 0, name: 'Mr.Hong' },
  { id: 1, name: 'Mr.Park' },
];
```

정의된 `id`를 `key`에 반영시켜주면 되는 것.

```js
<div className='box'>
  {dummyItem.map((item) => (
    <div key={item.id}>
      <span>{item.name}</span>
    </div>
  ))}
</div>
```

## key 관련 에러 해결법 2

기본적으로 첫번째 방법으로 더이상 뭘 하지 않아도 된다. 하지만 의미없는 `div`요소가 생성되어 렌더링 되는 관계로 레이아웃을 잡거나 할때 영향을 미치게 될 수 있다.

이 문제의 개선 방법은 `<></>`나 `<React.Fragment></React.Fragment>`를 사용하는 방법이다. 단순히 블럭요소를 잡을때는 비어있는 `<></>`를 사용해도 되지만, `key`를 부여할 경우는 `<React.Fragment></React.Fragment>`를 사용해야 한다. 이렇게 하면 실제 렌더링 될때 `key`값은 있지만 렌더링에는 영향을 미치지 않는 결과를 얻게 된다.

```js
<div className='box'>
  {dummyItem.map((item) => (
    <React.Fragment key={item.id}>
      <span>{item.name}</span>
    </React.Fragment>
  ))}
</div>
```

## record 15

### 적재적소에 적합한 대응을 해야 한다.

그러려면 이것저것 많이 알고 있어야 한다. 공부를 통해 알게 된 것을 알고 있다고, 기억하고 있다고 착각하게 만드는 경우를 여러번 경험했다. 모르던 것을 알게 되었을 때의 기록, 궁금해서 알아본 내용들을 기록하는 건 지난한 과정이지만 발전을 하는데 있어 필요한 과정이라 생각된다.
진짜 아는건지..
