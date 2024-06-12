---
title: createPortal로 모달 팝업 관리하기. show, hide 또는 remove
pubDate: 2024-04-16
tags:
  [
    'blog',
    'react',
    'portal',
    'show',
    'hide',
    'remove',
    'modal',
    'popup',
    '리액트',
    '모달',
    '접근성',
  ]
description: 포털을 다루는 방법을 좀더 고민해 봤다.
categories: react
heroImage: https://live.staticflickr.com/65535/53786731980_9e364eb565_o.png
---

작년 12월을 끝으로 일을 잡지 못해 계속 백수생활 중이다. 2월말 어머니를 모시고 일주일정도 여행을 다녀와야 해서 일을 찾지 못한 것도 있지만, 근 4개월을 놀고 있으니..한동안 코딩을 하지 않고 여행 다녀오고, 그림(낙서)그리고, 넷플릭스 보며 시간을 보냈다.

이러다 큰일날 것 같아 정신 차리고 다시 코딩을 하면서 컴포넌트를 잘 다루는 방법에 대해 고민을 해봤다. 분명히 어디선가 누군가는 좀 더 좋은 방법으로 작업하겠지만, 현재 내 수준에서 그나마 써먹을 수 있겠다 생각이 든 방법으로 데이터를 물고 다니는 건 대체로 캐시를 사용해서 넣었다 뺐다 하는 경우가 대부분이지만.. 이런 경우도 있지 않을까라는 생각에서 시작된 공부이니 딴지는 사양하겠다.(분명 더 좋은 방법, 바른 길이 있기 할 텐데...)

![portal 001](https://live.staticflickr.com/65535/53655999712_7a2e1714f9_o.png)

기본적으로 모달팝업은 크게 2가지 쓰임새가 있을 것 같아 보인다.(복합적으로 사용되기도 한다..)

- 데이터가 필요 없는 경우
- 데이터가 필요한 경우
  - 데이터가 단순한 경우
  - 매번 데이터를 넣었다 뺐다 하기 부담되는 경우

1번의 경우 매번 DOM을 넣었다 뺐다 하는 것이 소스상으로는 이상적이지만, 데이터에 따라선 항상 정보를 가지고 다니기 부담스러운 경우도 있을 수 있기 때문이라 여겨진다.

### 구성 방법

이전 포스팅했던 [포털이여 열려라!](/react-portal)에서 다루고 있는 내용과 마크업상의 구조는 비슷하다.

#### 1. modal-root 배치

우선 `modal`요소들을 모아둘 임의의 DIV(`modal-root`)을 생성해 둔다.

![portal 002](https://live.staticflickr.com/65535/52946451544_264f7a0420.jpg)

#### 2. createPortal 작업

하나의 소스로 true, false로 제어를 하고 싶었지만, 이걸 해결하지 못해 결국 2벌이 필요하게 되었다.
자기 합리화.. 이긴 하지만, 생각해 보면 용도가 다르기 때문에 별도로 작성하는 게 적합하다는 생각도 든다. true, false로 이런저런 옵션을 주다 보면 실제 컴포넌트가 복잡해지는 경향도 있을 수 있겠다는 생각이 들었다.

부모 측에서는 `createPortal`을 불러오지 않고 팝업의 상태 관리를 위해 `useState`로 관리만 한다. 1번 코드를 사용하게 되면 페이지가 로딩되는 시점부터 페이지에 렌더링 되어 있게 되며, 2번 코드를 사용하게 되면 DOM을 생성했다가 제거하게 된다.

2개 소스의 다른 점은 2번의 `ExampleModal`을 감싸는 `{Modal &&...}` 부분이다.

```js
// Parent.js
const [Modal, setModal] = useState(false)

<button onClick={() => setModal(true)}>Open</button>

// [1] DOM render
<ExampleModal isOpen={Modal}
  closeModal={() => setModal(false)} />

// [2] DOM mount & unmount
{Modal && <ExampleModal isOpen={Modal}
    closeModal={() => setModal(false)} />}
```

Modal은 [포털이여 열려라!](/react-portal)와 동일한 형식을 사용한다. Modal 페이지 내에서 컴포넌트를 생성해서 작업할지 말지만 정해서 작업하면 된다.

```js
// Modal.js
import { createPortal } from 'react-dom';

// Modal Component 구성
const Modal = () => {
  return (
    <div className='modal'>
      <div>Content</div>
      <button>close</button>
    </div>
  );
};

// Portal 구성
const Modal = () => {
  return (
    <>
      {createPortal(
        <Modal />, // Modal Component 배치
        document.getElementById('modal-root') // Modal 위치
      )}
    </>
  );
};
```

앞서 언급한 내용이지만, Modal 자체는 내용에 따라 다양하게 바뀔 수 있는 여지가 있다. 팝업의 크기, 위치, 데이터 유무, 컬러 등등 여러 옵션을 제어해야 한다. 대체로 어느 프로젝트나 팝업에 대한 제어로 트러블이 생기는 경우를 여러 번 경험했기 때문에 이런 생각을 하게 된 건지 모르겠다.

## record 16

### 아는 만큼 보인다. = 내가 아는게 정말 없구나.

정말 말처럼, 아는 만큼만 보인다. 그래서 공부를 많이 해야 하고 경험을 많이 해야 하는 것 같다. 모르는 게 있으니 알기 위해 공부를 하는 건데 뭘 모르는지 모르니 그게 문제다. 좀 더 멋진 해결 방법이 있을 것 같은데...
