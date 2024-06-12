---
title: 포털이여 열려라!
pubDate: 2023-06-03
tags: ['blog', '리액트', 'react', 'portal', '모달', 'modal', 'popup', '접근성']
description: 리액트에서 팝업을 다루는 방법. 그것은 포털을 여는 것!
categories: react
heroImage: https://live.staticflickr.com/65535/53786731980_9e364eb565_o.png
---

맞다. 다. 나는 지금 리액트를 공부하는 중이다. 우연한 기회로 원하던 프로젝트에도 참가하고 있다. 프론트앤드는 언감생심. 일단은 퍼블리싱 파트로 프로젝트에 참여하고 있는데 이전 작업자들이 만들어 놓은 소스를 분석하는 것도 힘겹다. 그래도 재미는 있다.

## 인터넷 강의의 도움

프로젝트에 들어오기 전, 이전 프로젝트가 끝나고 일이 잡히지 않아 강제 휴가를 보내는 동안 udemy에서 [리액트 강의](https://www.udemy.com/course/best-react/)를 구매한 뒤 조금씩 차례대로 듣는 중이었다. 그 와중에 Portal에 대해 알게 되었고 마침 프로젝트에서 신경이 쓰였던 부분과 매칭되어 가려운 곳을 긁을 수 있었다.

## 리액트와 팝업, 그리고 접근성

현시점, 아직 리액트를 활용한 접근성 프로젝트는 오롯이 혼자의 힘으로는 해결하지 못할 것 같다는 생각이 들고 있다. 일단 스크립트를 다루기 위해 선결되어야 하는 각종 Hook에 대해서도 해롱거리는데 무슨.

어쨌건, 리액트를 처음 접하고 팝업에 대한 고민을 하게 된 경위는 최대한의 공통요소를 Component화 시켜서 돌려쓰는 것을 주목적으로 하고 있는데 팝업의 경우 사용자의 사이트 사용에 영향을 주는 alert형과 정보 입력과 상호작용을 위한 modal형으로 나눌 수 있을 것 같은데 alert형은 최상단 부모(App)에서 관리하는 것이 적당할 것 같지만 modal형은 각 페이지 단위로 관리하는 게 일반적인 프로젝트 진행방식이다.

문제는…. 기존 방식의 코딩은 html로 한 장씩 만들어내는 과정과 공통으로 뽑아 놓은 레이아웃(Header, Main, Footer등) 기본으로 잡고 작업할 때와 달리 리액트의 경우 개별 페이지 단위로 접근해서 작업할 때 팝업들이 놓이게 되는 위치가 애매하게 된다.

아무리 Component로 구분을 한다고는 해도 CSS를 적용하는 그렇고 뭔가 고전적인 방식과의 차이로 껄끄럽다. 이런 생각을 하던 와중에 Portal을 알게 되었으니 기쁘지 아니한가!

## 이런게 있었구나! createPortal!

### 개념

[점퍼](<https://ko.wikipedia.org/wiki/%EC%A0%90%ED%8D%BC_(%EC%98%81%ED%99%94)>)를 봤을 때도 그랬지만, [닥터 스트레인지](https://ko.wikipedia.org/wiki/%EB%8B%A5%ED%84%B0_%EC%8A%A4%ED%8A%B8%EB%A0%88%EC%9D%B8%EC%A7%80)가 게이트를 만드는 걸 본 뒤로 항상 제일 가지고 싶은 아이템 중 하나라고 생각하게 되었다. 어디든 갈 수 있다니!!!

알고 있는 지식 선에서 설명하자면 Portal의 개념도 비슷하다. '**이곳과 저곳을 연결하는 통로**'.

정리해 보자면 다음과 같을 것 같다.

- Modal Component 생성
- A Component로 페이지 생성해서 Modal Component를 import
- A Component에서 import한 Modal Component를 해당 Component가 아닌 다른 Component(Portal)에 전달

### 구성 방법

react.dev : [createPortal](https://react.dev/reference/react-dom/createPortal)에서 다루고 있으니 참고

#### 0. 초기 구성 확인

초기에는 `root`만 존재한다.

![portal 001](https://live.staticflickr.com/65535/52946451534_a001a373f7.jpg)

#### 1. modal-root 배치

`modal`요소들을 모아둘 임의의 DIV(`modal-root`)을 생성한다.

![portal 002](https://live.staticflickr.com/65535/52946451544_264f7a0420.jpg)

```html
<div id="modal-root"></div>
// 추가
<div id="root"></div>
```

#### 2. createPortal 작업

Modal을 원하는 곳(modal-root)에서 보여주기 위한 작업을 진행한다.
Modal Component에서 `react-dom`을 설정하고, 콘텐츠를 다룰 `Modal`을 생성하고, Modal을 위치시킬 `createPortal`을 구성하는 방식이다.

```js
// Modal.js
import { createPortal } from 'react-dom';

// Modal Component 구성
const Modal = () => {
  return (
    <div className='modal'>
      <h3>Modal</h3>
      <p>textContent</p>
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

소스를 보면 이해가 되겠지만, createPortal 은 다음과 같은 구조로 이루어지는데 `children`에서 대상을 import하고, `container`에 위치시킬 곳을 지정시키는 방식이다.

```js
{
  ReactDOM.createPortal(children, container);
}
```

모든 작업이 끝난 뒤 다시 확인해보면 `.modal`이 제대로 `#modal-root`에 위치하는 것을 확인할 수 있다.

![portal 003](https://live.staticflickr.com/65535/52945711302_e59ff50576.jpg)

이로써 Modal 작업은 하나의 페이지에서 동일하게 작업하면 되고 Portal을 통해 기존과 같이 Modal들만을 따로 구성시킬 수 있게 되었다. 훌륭하다!

## record 8

### 새로운 것을 알게 되었는데 기쁨과 걱정이 함께 커진다.

특히 적재적소에 필요한 것을 알게 되었을 때 더욱 좋은 것 같다. 알면 알수록 알아야 하는 것들이 많아지니 걱정도 함께 커지는데 기쁨과 걱정이 함께 커지는 상황이라고 할까.

현재 프로젝트를 통해 좀 더 다양하게 현장에서 사용 가능한 것들을 익힐 수 있었으면 좋겠다. 아무래도 혼자 무언가를 하기보다 실제 움직이는 소스를 통해 건드려보면서 익히는 것만큼 좋은 건 없는 것 같다. 그래서 다들 사이드 프로젝트를 하라고 하는 것 같다.
