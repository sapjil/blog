---
title: Github Action + Firebase Hostiong
pubDate: 2023-03-14
tags:
  [
    'blog',
    '리액트',
    'react',
    'Github Action',
    'Firebase Hostiong',
    'Firebase',
    'Hostiong',
		'파이어베이스',
		'호스팅',
		'무료'
  ]
description: Github Action과 Firebase Hostion을 사용해서 자동 배포 설정
categories: git
heroImage: 'https://live.staticflickr.com/65535/53786479953_c2b2fcff2e_o.png'
---

## 이왕이면 다홍치마, 배포 자동화 도전

아마 조금이라도 IT에 발을 담그고 있을 경우 대체로 자기계발이나 기록이라는 명목으로 Github 같은 형상관리 서비스와 Firebase 같은 무료 호스팅 서비스를 사용하고 있을 것이라 생각되는데 이렇게 사용할 경우 두 곳에다 배포를 해야 하는데 소스커밋과 배포를 따로 해야 하니까 귀찮은 게 사실이다. 이럴 때 자주 사용하는 것이 Github에서 제공하는 Action기능을 이용해서 커밋이 완료되면 자동으로 호스팅서버로 배포해 주는 신공이다.(이제는 일반적?)

이전에, 한참 전에 GitLab을 사용해서 삽질하면서 설정을 했었는데 어느날부터 막히는 일이 생겼었지만 지식부족으로 재설정을 포기하고 있었다. 시간이 흘러 흘러 이제는 좀 더 쉽게 환경 구성이 가능해진 것을 알 수 있었다. 이번엔 Github다.

React는 그대로 배포해도 의미가 없으니 빌드된 정적 파일을 배포해야 한다. 이번에 새로운 방법을 배우면서 확인 한 내용을 정리하고자 한다.

## 연결

Git과 Firebase를 연결시켜주는 작업이 간소화되었다. 터미널에서 필요한 명령어를 입력해 주면 자동으로 설정 파일을 생성해 준다!

```
(Firebase 호스팅을 사용한 적이 없을 경우)
$ firebase init hosting

(Firebase 호스팅을 사용 중인 경우)
$ firebase init hosting:github
```

다음 질문들에 필요한 정보를 입력해 주면 된다.

| #   | 질문                                                                            | 응답                                                        |
| --- | ------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| 1   | For which GitHub repository would you like to set up a GitHub workflow?         | 본인의 레파지토리를 입력                                    |
| 2   | Set up the workflow to run a build script before every deploy?                  | 호스팅시 사전에 빌드 실행여부를 결정                        |
| 3   | What script should be run before every deploy?                                  | 빌드를 할 경우 필요한 스크립트 입력 npm ci && npm run build |
| 4   | Set up automatic deployment to your site's live channel when a PR is merged?    | 풀 리퀘스트 완료 후 호스팅서버에 머지여부 결정              |
| 5   | What is the name of the GitHub branch associated with your site's live channel? | main                                                        |

과정을 완료하고 커밋하면 자동으로 Action이 실행된다. 재미~ 신기~

## 배포 완료

![git-action-ci-01](https://live.staticflickr.com/65535/52746585533_772b4a7b4d_z.jpg)

약 1분 정도가 소요된 후 배포가 완료되면 잠시 후에 Firebase에서도 반영된 것을 확인할 수 있다.

### 그런데 Node.js 12를 지원하지 않는다고?

배포는 완료되었다. 이리 기쁠 수가. 궁금해서 태스크를 열어보니 거슬리는 문구가 보였다. 더 이상 Node.js 12를 지원하지 않는다며 업데이트를 하란다. 이런 거 다 해주시는 거 아니었나요...?

`.yml` 설정파일을 수정해줄 필요가 있었다.

```
steps:
      - uses: actions/checkout@v2
```

`checkout@v3`으로 바꾸고 `node-version: "16"`을 추가시켜 주는 작업을 진행

```
steps:
      - uses: actions/checkout@v3
        with:
          node-version: "16"
```

모든 작업이 완료되었다. 이제는 Firebase에 따로 deploy를 할 필요가 없이 Git에 커밋만 하면 자동으로 배포까지 일사천리.

## 참고

- [zenn.dev/watarukun](https://zenn.dev/watarukun/articles/8f3e318bacf97cabf879)
- [qiita.com/masato_makino](https://qiita.com/masato_makino/items/3edde8e5f1a782a5c7ea)

## record 4

### 당연하게도 가능한 자동화 설정은 해두는 것이 좋다

자동화는 그만큼 불필요한 일을 줄여주는 만큼 자동화가 가능한 부분은 모두 자동화를 해두는 것이 정답이라 생각된다. 사람이 동일한 작업을 생각하며 가끔씩 나오는 실수가 치명적일 경우가 있다. 이런 자동화 가능한 것들은 알아두면 득이 된다.

이런 환경이니 실제로 블로그 운영에 들어가는 돈은 도메인 비용정도다. 어쩌면 도메인 비용도 필요 없을 것 같지만 몇 년 동안 사용하고 있는 거고 그리고 이왕이면 스스로를 나타낼 수 있는 일종의 브랜드? 티스토리도 운영하고 있지만 그쪽은 말 그대로 잡동산. 여기선 관련 기술만 다루기로 맘먹었다.

### 초반엔 조금 알 것 같더니 점점 어렵다

리액트 공부 하다가 옆길로 빠졌다. 다시 공부해야 하는데 개념 잡기가 잘 되지 않는 것 같다. 특히 모든 과정들이 리팩토링까지 진행하면서 한방에 알려주려고 하니 따라 하다 보면 뭔가 삼천포로 빠지는 기분까지 든다. 어디까지가 현실이고 어디부터 환상인가..(ㅠ\_ㅠ)

차근차근.. 일단은 한번 완주가 목표. 다시 처음으로 왔다 갔다 해야지.
