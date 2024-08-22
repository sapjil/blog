---
title: Windows에서 키보드 매핑하여 사용하기
pubDate: 2024-08-22
# updatedDate: 2024-08-16
tags:['Windows','윈도우즈','PowerToys','Screen Capture','Mac']
description: 윈도우즈에서 맥과 같은 키보드 배열로 작업을 하고자 할 경우 PowerToys가 해결책이라 생각된다. 세상 진짜 좋아졌다.
categories: utlity
heroImage: 'https://live.staticflickr.com/65535/53784308163_917bd2a5ff_o.png'
---

## PowerToys를 사용하게 된 계기

그동안 근 10년동안 프로젝트에 참가하는 동안은 HHKB Lite를 사용해 오고 있었고 집에서는 애플 순정 키도를 사용하고 있었는데 이번에 혹시나 마우스를 사용하면서 아픈 손목에 도움이 될까 싶어 빨콩이 사용 가능한 ThinkPad Keyboard를 영입하면서 새로운 키보드에 익숙해지기 위해 노력하는 중이었다.

![](https://live.staticflickr.com/65535/53938381122_cefd3514db_o.png)
![](https://live.staticflickr.com/65535/53939537648_3384c0f0ea_o.png)

당연하게도 너무나 익숙했던 HKKB Lite의 키 배열과도 다르고 애플 순정 키보드와도 다른 키 배열이 계속해서 익숙해지지 않으며 살짝 힘들어 하고 있었다. 그러다 맥에서 잠시 사용했었던 Karabiner와 같은 키매핑 프로그램이 윈도우에도 있을 것이라 생각하고 검색해보니 PowerToys라는 것이있었다. 더구나 마이크로소프트에서 나름 관리해주고 있어서 믿음도 가기에 당장 설치.

![](https://live.staticflickr.com/65535/53938341532_79b842efbd_o.png)
![](https://live.staticflickr.com/65535/53938341537_445b4cdc41_o.png)
![](https://live.staticflickr.com/65535/53939699280_fba1ea228c_o.png)

![](https://live.staticflickr.com/65535/53938402307_8630b0961d_o.png)

```shell
Alt -> Win
Win -> Ctrl
Ctrl -> Alt
```

사진처럼 배치를 바꿔주니 한결 익숙한 환경에 근접한 경험을 할 수 있었다. 운영체제의 차이가 있기 때문에 100% 일치는 하지 않지만 이정도면 정말 준수하다 생각된다.

기본적인 기능키에 더해서 Thinkpad 키보드의 CapsLock 에는 맥과 같은 언어변경 기능을 적용했고 PgUp, PgDn 키에는 방향키를 배정했다. 이 키보드의 PgUp, PgDn의 경우 방향키와 너무 붙어있어서 의도하지 않게 페이지를 위아래로 이동시켜 버리는 문제가 있어서 키매핑에서 방향키로 바꾸고 기본 기능은 무시를 시켰다. 평소에도 PgUp, PgDn 키는 잘 사용하지 않고 있기 때문에 큰 불편은 없는 상황이다.

![](https://live.staticflickr.com/65535/53939699285_b3bf01cebd_o.png)

꽤 마음에 드는 기능 중 한가지가 미리보기 기능이었다. 맥에서 사용하는 Alfred 처럼 사용가능한 기능이어서 무척 마음에 든다.
