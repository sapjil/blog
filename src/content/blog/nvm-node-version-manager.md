---
title: nvm으로 node 버전 관리하기
pubDate: 2023-11-15
# updatedDate: 2023-11-10
tags: node, nvm
description: 그동안 굳이 사용할 필요성을 느끼지 못했던 nvm 인데.. 버전 관리를 해볼 필요가 생겨서 적용해봄
categories:
  - www
# heroImage: '/blog-placeholder-2.jpg'
---

nvm의 존재는 알고 있었지만 그동안 딱히 사용할 일이 없었는데 이번에 사무실에서 기존 작업자가 html로 만들어 두었던 업무 가이드 문서를 vuepress로 바꾸어 보려고 하던 차에 운영 업무로 사용 중인 노드버전과 맞질 않아서 진행을 하지 못하고 있었다. 문제를 해결하기 위해 nvm을 도입해서 설치까지 마치고 일단 가이드 문서의 컨버팅(?)까지 마무리했다.

일단 까먹기 좋아하는 관계로 기록용 포스팅.

## nvm 설치, node 버전 관리하기

mac에서는 brew가 필요한 관계로 우선 brew 설치

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

설치 잘 된건지 확인

```
brew -v
```

nvm 설치

```
$ sudo curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.1/install.sh | bash
```

확인해보면 `command not found` 가 나올 수 있음

```
$ nvm ls
zsh: command not found: nvm
```

vi로 편집 창으로 접근해서

```
vi ~/.bash_profile
```

다음 내용을 기입

```
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm
```

그리고 저장

```
source ~/.bash_profile
```

다시 확인

```
$ nvm ls
```

기본 다음과 같이 설정된게 없다고 나오면 OK

```
->       system
node -> stable (-> N/A) (default)
iojs -> N/A (default)
```

16버전을 설치. 16까지만 입력하면 해당 버전의 가장 높은 버전을 설치해 줌

```
nvm install 16 => 16.20.2
```

`ls` 명령어로 각 버전의 설치여부를 확인할 수 있다.

```
->     v16.20.2
         system
default -> 16.20.2 (-> v16.20.2)
node -> stable (-> v16.20.2) (default)
stable -> 16.20 (-> v16.20.2) (default)
iojs -> N/A (default)
lts/* -> lts/iron (-> N/A)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.17.1 (-> N/A)
lts/carbon -> v8.17.0 (-> N/A)
lts/dubnium -> v10.24.1 (-> N/A)
lts/erbium -> v12.22.12 (-> N/A)
lts/fermium -> v14.21.3 (-> N/A)
lts/gallium -> v16.20.2
lts/hydrogen -> v18.18.2 (-> N/A)
lts/iron -> v20.9.0 (-> N/A)
```

설치된 버전을 확인

```
node -v
```

여기까지가 설치 과정이고..

## 사용법

주로 사용하는 명령어.

```
nvm ls : 확인
nvm current : 현재 사용중인 버전 확인
nvm use {node version} : 설치된 버전간 변경
nvm install {node version} : 해당 버전 설치
nvm uninstall {node version} : 해당 버전 삭제
```

Astro는 18버전부터 사용가능하고, vuepress(1.9.xx)는 16부터 사용가능한 상황인 것 같다. 진작에 사용할 것을...
