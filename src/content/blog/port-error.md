---
title: (error) port error가 문제였다고
pubDate: 2023-03-11
updatedDate: 2023-03-14
tags:
  [
    'blog',
    '리액트',
    'react',
    'port',
    'error',
    'WebSocket',
    'WDS_SOCKET_PORT',
    'react-script',
		'sudo kill'
  ]
description: 작업중 포트 에러가 나올때 대처법. 차분하게 에러를 잘 확인하자.
categories: coding
---

- [update] 2023-03-14

## 에러가 계속 나오는 상황

![port-error-01](https://live.staticflickr.com/65535/52740497738_a2388ae79e_z.jpg)

학습중에, 잘 따라한 것 같은데도 에러가 계속 나왔다. 재기동도 해봤지만 적용이 되지 않는 현상이 지속되었다. 뭐가 문제인가..

`WebSocket connection to 'ws://127.0.0.1/' failed:`

### WDS_SOCKET_PORT로 해봐요

이 에러는 무엇인가요.. 구글링을 열라게 하니 대체적으로 프로젝트에 `.env` 파일이 없다면 만들고 `WDS_SOCKET_PORT=0`을 추가시키면 해결 된다고 하는 편이었는데.. 나한테는 통하지 않는 방법이었다. 443이나 0을 추가시키거나 같이 적용 시키면 된다고 하던데 통하지 않았다.

```
WDS_SOCKET_PORT=443
WDS_SOCKET_PORT=0
```

### react-script 버전을 조정해봐요

다음으로 접근해 본건 `react-script` 버전에 따라 동일하게 `WebSocket` 오류가 나올 수 있다고 한다. 대체로 나오던 정보들은 v3인 경우의 예제들이 많았는데 현재 버전이 v5.0.1이었기 때문에 실질적으로 도움이 되지 않았었다. 검색을 하던 와중에 v5.0.0 이상부터 문제가 있는 케이스가 있다고 해서 버전도 다운시켜 봤는데.. 이것도 소용이 없었다.

### package.json을 수정해봐요(2023-03-14)

이것도 저것도 먹히지 않는다면 포트를 바꾸는 방법이 있었다.

```
"scripts": {
	"start": "react-scripts start",
},
```

다음과 같이 `POTR=3006` 원하는 포트 번호를 추가시켜두면 `WebSocket` 오류가 발생하지 않았다. 어쩌면 이 방법이 가장 확실한 방법일 것 같아 보인다.

```
"scripts": {
	"start": "POTR=3006 react-scripts start",
},
```

- [stackoverflow.com](https://stackoverflow.com/questions/40714583/how-to-specify-a-port-to-run-a-create-react-app-based-project)

## 잠깐, 포트가 사용되고 있다고?

![port-error-02](https://live.staticflickr.com/65535/52740419185_42cf824fe9_z.jpg)

터미널에서 작업하다 에디터에서 명령어를 실행하니 먼저 해결되었어야 할 문제에 대해 메시지를 보내주고 있었다.

`Somethig is already running on port 3000. Probably: ~~~ (pid 93467)`

3000번 포트가 사용되고 있는데 어쩔꺼냐는 이야기 맞는거지? yes를 누르면 3001번으로 리액트는 실행되지만 `WebSocket connection` 에러가 계속 나온다. 터미널이 중복으로 떠서 그런것일 수도 있을 것 같아 열고 닫고를 몇번 해봤지만 역시 의미 없는 행동이었다.

## 그럼 포트를 죽여야지?!

포트가 문제라면 포트를 죽이면 해결되는 문제 아닐까?! 인터넷에는 정말 모든 정보가 존재하는 것 같다. 양질의 정보를, 나한테 맞는 정보를 찾는데 드는 시간을 무시할 수 없지만..

![port-error-03](https://live.staticflickr.com/65535/52740010421_bc5a33268e_z.jpg)

먼저 터미널에서 다음 명령어를 실행해서 현재 내 컴퓨터에서 사용되고 있는 포트를 일괄적으로 확인하는 작업이 필요하다.

`sudo lsof -PiTCP -sTCP:LISTEN`

전체 목록을 확인한 뒤 해당 문제가 되는, 이번에는 3000번 포트를 확인할 수 있다. 에러 메시지에서도 보여줬던 `pid 93275`와 일치하는 걸 확인할 수 있다.(스샷은 확인차 돌려본거라 번호가 상이하다)

이제 이 녀석을 죽이면 되는거겠지? `kill` 명령어로 해당 포트를 다운 시켜준다.

`sudo kill -9 93275`

다운 시키고 다시 `npm run start` 명령어를 날려주니 브라우저에서 소켓 에러가 더이상 나오지 않게 되었다. 이유는 모르겠지만, 이걸로 해결된 것 같다.

## record 2

### 에러는 잘 확인하자

결국 문제의 해결 방법은 가까운 곳에 있었다. 어디선가는 차분하게 실마리를 알려주고 있다. 초보가 흔히 하는 실수 중 하나인건지.. 어쨌건 이로서 리액트에서 맞이할 수 있는 수많은 에러중 한가지에 대해서는 해결을 위한 접근 방법을 알게 되었다 생각된다.

브라우저에서 내보내는 에러가 나를 헷갈리게 만든 케이스였다. 아직도 이해가 잘 가지는 않는데 브라우저의 디버깅시 알려주는 에러와 실제로 서버를 기동시키는 테미널에서의 오류 내용이 다르다는 거였다.
