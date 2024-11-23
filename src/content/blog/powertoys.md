---
title: Windows에서 PowerToys로 Mac 기능키 배열 매핑하여 사용하기
pubDate: 2024-08-27
# updatedDate: 2024-08-16
tags:
  [
    'Windows',
    '윈도우즈',
    'PowerToys',
    'Screen Capture',
    'Mac',
    '매핑',
    '키보드매핑',
		'씽크패드',
		'트랙포인트',
    'ThinkPad TrackPoint Keyboard II',
  ]
description: 윈도우즈에서 맥과 같은 키보드 배열로 작업을 하고자 할 경우 PowerToys가 해결책이라 생각된다. 세상 진짜 좋아졌다. ThinkPad TrackPoint Keyboard II에 맥 키보드 배열 매핑하기
categories: utlity
heroImage: 'https://live.staticflickr.com/65535/53938439602_403986fc89_o.png'
---

## PowerToys를 사용하게 된 계기

그동안 근 10년동안 프로젝트에 참가하는 동안 HHKB Lite를 사용해 오고 있었고 집에서는 애플 순정 키보드를 사용하고 있었는데 이번에 혹시나 마우스를 사용하면서 아픈 손목에 도움이 될까 싶어 빨콩이 사용 가능한 ThinkPad TrackPoint Keyboard II를 영입하면서 새로운 키보드에 익숙해지기 위해 노력하는 중이었다.

![](https://live.staticflickr.com/65535/53938381122_cefd3514db_o.png)

<!-- ![](https://live.staticflickr.com/65535/53939537648_3384c0f0ea_o.png) -->

당연하게도 너무나 익숙했던 HKKB Lite의 키 배열과도 다르고 애플 순정 키보드와도 다른 키 배열이 계속해서 익숙해지지 않으며 살짝 힘들어 하던차에 맥에서 잠시 사용했었던 Karabiner와 같은 키매핑 프로그램이 윈도우에도 있을 것이라 생각하고 검색해보니 PowerToys라는 것이 있었다.

## PowerToys

### PowerToys 다운로드

마이크로소프트에서 나름 관리해주고 있기 때문에 믿음도 가기에 당장 설치. 대시보드를 보면 알겠지만 꽤 다양한 기능을 제공하고 있다. 확실히 윈도우즈도 많이 좋아지고 있다는 것을 느낄 수 있다.

다운로드: [https://github.com/microsoft/PowerToys](https://github.com/microsoft/PowerToys/releases/tag/v0.83.0)

![](https://live.staticflickr.com/65535/53938341532_79b842efbd_o.png)
![](https://live.staticflickr.com/65535/53938341537_445b4cdc41_o.png)

### Keyboard Manager

딴건 관심없고 가장 기대가 큰 Keyboard Manager!

기본적인 기능키에 더해서 Thinkpad 키보드의 <kbd>CapsLock</kbd>에는 맥과 같은 언어변경 기능을 적용했고 <kbd>PgUp</kbd>, <kbd>PgDn</kbd> 키에는 방향키를 배정했다. 페이지 업다운의 경우 방향키와 너무 붙어있어서 의도하지 않게 페이지를 위아래로 이동시켜 버리는 문제가 있었다.

키매핑에서 방향키로 바꾸고 기본 기능은 무시. 평소에도 페이지 업다운은 잘 사용하지 않아서 아직까지는 이것 때문에 불편은 없는 상황이다.

![](https://live.staticflickr.com/65535/53939699280_fba1ea228c_o.png)

<kbd>Alt</kbd>를 <kbd>Win</kbd>로 이동시키고,

<kbd>Win</kbd>를 <kbd>Ctrl</kbd>로 이동시키고,

<kbd>Ctrl</kbd>를 <kbd>Alt</kbd>로 이동시키면 완료.

![](https://live.staticflickr.com/65535/53938402307_8630b0961d_o.png)

사진처럼 배치를 바꿔주니 한결 익숙한 환경에 근접한 경험을 할 수 있었다. 운영체제의 차이가 있기 때문에 100% 일치는 하지 않고 다른 동작을 하는 경우도 있지만 이정도면 정말 준수하다 생각된다. 키보드를 사자마자 방출시켜야 하나 고민했었는데 다행.

### PowerToys Run

![](https://live.staticflickr.com/65535/53939699285_b3bf01cebd_o.png)

Keyboard Manager 이외에 꽤 마음에 드는 기능 중 한가지가 PowerToys Run 기능이었다. 맥에서 사용하는 Alfred 처럼 사용가능한 기능이어서 무척 마음에 든다.
