---
title: Props로 생길 수 있는 Prop drilling의 문제, 적재적소에 Provider / Inject를 활용하자
pubDate: 2024-12-22
# updatedDate: 2024-08-16
tags: ['Vue', 'provider', 'inject', 'emit', 'props', 'prop drilling']
description: Vue에서 Provide & Inject 사용법 익히기
categories: vue
heroImage: 'https://live.staticflickr.com/65535/53937394093_4043ef8c67_o.png'
---

## 우선은 개념부터. Provider? Inject? 뭣에 쓰는 물건인고?

아직은 그냥 따라 하며 사용하는 수준이기 하지만, 각 용어에는 각각의 의미하는 바가 있기 마련이고.
우선은 사전적 의미를 이해해 볼 필요가 있겠다.

```
provider: 공급자, 제공자, 조달자, 부양자
inject: 주입하다, 넣다, 투입하다, 끼워넣다, 추가하다
```

[공식 가이드](https://ko.vuejs.org/guide/components/provide-inject.html)를 보면 시각적으로 바로 이해가 되긴 한다.

즉, 컴포넌트를 사용한 개발과정에서 Props를 이용하면 자식을 거쳐 손자까지 정보를 넘겨줄 수는 있다.
그저 이 과정이 귀찮기도 하거니와 사이트가 복잡해지면 일부 수정과정에서 정보를 전달하는 상위 컴포넌트 모두를 수정해야 하기 때문에 공수가 많이 들어가는 것이 문제다.

![](https://ko.vuejs.org/assets/prop-drilling.HScJJCgJ.png)

이 시점에서 작업의 효율성을 위해 Provider(제공)와 Inject(주입)의 개념/기능이 필요해진다는 것을 알게 된다.

![](https://ko.vuejs.org/assets/provide-inject.COj2H-vl.png)

개인적으로 지금까지는 마크업을 하며 이런 부분까지는 신경을 쓰지는 않아도 되었다.
이유는 마크업의 경우 단순 페이지를 만들어 개발에 넘기게 되면 필요에 따라 조합, 분해를 하고 로직에 맞도록 개선을 해서 최종적으로 완성을 하게 되기 때문이다.
전체적인 개발 프로세스는 대체적으로 이 과정을 거치게 된다. 마크업 과정에서 이런 부분까지 작업이 가능하다면 개발 속도도 향상될 것이고 프로젝트에서도 마크업의 기여도가 상승될 것은 자명하다.

## Provider, Inject

그런데 이걸 어디에 사용할까? 개념은 이해를 했는데 개발용어로 변환시키는 과정 즉, 이걸 내 머리로 온전히 이해하고, 코드로 만들어내는 과정은 별개의 이야기..

이번 프로젝트에서는 공통으로 사용될 Toast, Modal 위주로 사용해 볼 수 있었다.
기본적인 레이아웃을 정하고, 각 페이지에서 다루게 되는 메시지나 알럿등을 위해 공통 모달을 페이지 마다 배치하는 건 비효율적이다.
해당 페이지에서 필요한 별도 모달은 개별로 추가시키고 공통으로 사용될 요소들을 구분시키면 좋다는 것을 알았다.

우선은 Provider의 설정

```js
export default {
  data() {
    message: 'Hello!';
  },
  provider() {
    return {
      message: this.message,
    };
  },
};
```

다음은 Inject의 설정

```js
export default {
  inject: ['message'],
  data() {
    return {
      fullMessage: this.message,
    };
  },
};
```

우선은 이 정도의 공식 가이드에서 다루는 개념과 사용법만 잘 인지하고 있어도 지금 내가 하고 있는 저수준 개발정도라면 많은 도움이 된다는 것을 알 수 있었다.
어떤 의도로 개발을 진행한 것인지 알 수 있고 실제 개발 과정에서도 도움이 되었다.
특히 공통 요소나 데이터를 전달하는 작업에서 Prop drilling의 단점을 개선할 수 있다는 것이 매력적이라 생각되었다.
이걸 모르던 시절에는 죄다 Props로 내려주고 있었으니.. 아직은 활용을 많이 하고 있지 않아 익숙하지 않지만 익숙해지면 좀 더 자연스럽게 여러 곳으로 응용 가능할 것 같다.

가이드를 보면 Symbol, Computed 등의 사용도 가능한데 아직 그 수준까지의 기능을 사용할 일은 없는 것 같다. props, emit, ref, provider, inject 등 배우는 것도 많이 있지만, 배워야 할 것이 더 많은 상황.
적재적소에 필요한 기능을 사용하기 위해선 더 많은 경험이 필요할 것 같다. 확실히 실제 프로젝트를 통해 체감하는 것이 가장 빠른 지름길인 것 같다.

## record 21

### Props만 알아도 되는 시절이 있었었었지

마크업을 생업으로 하는 경우, 레거시 프로젝트라면 상관없지만, 차세대 프로젝트를 진행할 경우에는 데이터를 컴포넌트로 내려주는 Props에 대한 이해만 있어도 무난하게(매우 만족스럽진 않지만 업무상 트집 잡힐 정도는 아닌) 프로젝트를 진행할 수 있었다.(대략, 1~2년 전까기만 해도..) 적정 수준의 스크립트 이해력과 디자이너와 협의하면서 개발친화적인 컴포넌트 설계가 가능할 정도의 개념을 탑재한 수준이면 일 인분의 업무는 충분히 소화할 수 있었다.

그런데 이제는 이것만으로는 매리트가 없어졌다. 정확히 표현하자면 이런 수준에 멈추어 있다 보면 저수준의 프로젝트만 전전하다가 시장에서 제명이 될 것 같은 위기감을 느끼게 되었다는 것이 좀 더 명확한 표현이 아닐까 생각된다. 이런 위기감에서 비롯된 경각심은 여러 사람을 강제로 프런트앤드로 전향하도록 만들었고 그런 기조에서 살아남은 사람과 그렇지 못한 사람으로 또다시 경계가 나누어지고 있는 시장이 지금이라고 생각된다. 뭔가 프런트 영역은 항상 과도기인 것 같은 느낌이 든다. 난 살아남을 수 있을까 아니면 도태되어 가는 일원 중 한 명이 될까. 지금 그 시험을 받고 있는 중이다.
