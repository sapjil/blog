---
title: nvm으로 node 버전 관리할때 nvmrc로 자동화시켜 귀차니즘 탈출하기
pubDate: 2023-11-15
updatedDate: 2023-12-01
tags: ['node', 'nvm', 'nvmrc', 'brew', 'Homebrew', '버전관리', '자동화']
description: 그동안 굳이 사용할 필요성을 느끼지 못했던 nvm 인데.. 버전 관리를 해볼 필요가 생겨서 적용하고 궁극에는 nvmrc를 사용하여 프로젝트별로 노드 버전을 자동으로 적용해주는 자동화 설정까지 마무리해서 귀차니즘에서 탈출하는 과정
categories: node
# heroImage: '/blog-placeholder-2.jpg'
---

nvm의 존재는 알고 있었지만 그동안 딱히 사용할 일이 없었는데 이번에 사무실에서 기존 작업자가 html로 만들어 두었던 업무 가이드 문서를 vuepress로 바꾸어 보려고 하던 차에 운영 업무로 사용 중인 노드버전과 맞질 않아서 진행을 하지 못하고 있었다. 문제를 해결하기 위해 nvm을 도입해서 설치까지 마치고 일단 가이드 문서의 컨버팅(?)까지 마무리했다.

일단 까먹기 좋아하는 관계로 기록용 포스팅.

- [`nvm` 설치, node 버전 관리하기](#nvm-설치-node-버전-관리하기)
- [`nvm` 사용법](#nvm-사용법)
- [`.nvmrc` 설치 및 활용(23-11-22)](#nvmrc-설치-및-활용)
- [`.nvmrc` 프로젝트별 노드버전 자동적용(23-12-01)](#nvmrc-프로젝트별-노드버전-자동적용)

## nvm 설치, node 버전 관리하기

mac에서는 brew가 필요한 관계로 우선 brew 설치

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

설치 잘 된건지 확인

```shell
brew -v
```

만약 `brew`를 찾지 못할 경우

```shell
zsh: command not found: brew
```

`.zshrc`에서 직접 path를 설정해 줘야 함

```shell
vi ~/.zshrc
```

다음의 내용을 기입하고 저장한뒤 종료(`:wq`)후 터미널을 재실행

```shell
export PATH=/opt/homebrew/bin:$PATH
```

설치 잘 된건지 다시 확인 후

```shell
brew -v
Homebrew 4.1.21
```

nvm 설치

```shell
$ sudo curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.1/install.sh | bash
```

확인해보면 `command not found` 가 나올 수 있음

```shell
$ nvm ls
zsh: command not found: nvm
```

vi로 편집 창으로 접근해서

```shell
vi ~/.bash_profile
```

다음 내용을 기입

```shell
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm
```

그리고 저장

```shell
source ~/.bash_profile
```

다시 확인

```shell
$ nvm ls
```

기본 다음과 같이 설정된게 없다고 나오면 OK

```shell
->       system
node -> stable (-> N/A) (default)
iojs -> N/A (default)
```

16버전을 설치. 16까지만 입력하면 해당 버전의 가장 높은 버전을 설치해 줌

```shell
nvm install 16 => 16.20.2
```

`ls` 명령어로 각 버전의 설치여부를 확인할 수 있다.

```shell
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

```shell
node -v
```

여기까지가 설치 과정이고..

## nvm 사용법

주로 사용하는 명령어.

```shell
nvm ls : 확인
nvm current : 현재 사용중인 버전 확인
nvm use {node version} : 설치된 버전간 변경
nvm install {node version} : 해당 버전 설치
nvm uninstall {node version} : 해당 버전 삭제
```

Astro는 18버전부터 사용가능하고, vuepress(1.9.xx)는 16부터 사용가능한 상황인 것 같다. 진작에 사용할 것을...

## `.nvmrc` 설치 및 활용

`nvm`을 설치하고 잠시동안은 편했으나 결국 수작업으로 버전을 바꿔줘야 하는 불편함이 있었다. 편해지면 더 편한것을 찾게 되는건 어쩔 수 없는 것 같다. 방법을 찾아 보니 역시 있었다. 그 방법은 `nvmrc`를 사용하는 것.

방법은 무척 쉽다. 각 프로젝트의 루트 폴더에 `.nvmrc` 파일을 만들어 두고 각 파일에 프로젝트에서 사용되는 노드 버전만 기입해 두면 끝이다.

```shell
.nvmrc
> 16.20.2 또는 lts/gallium
```

그리고 프로젝트에 접근해서 `nvm use`만 타이핑 해주면 사용가능하다.

```shell
nvm use
```

이 방법으로 이전보다 조금 더 수월하게 프로젝트를 관리할 수 있었다. 하지만 이것도 계속 하다보면 귀찮...

## `.nvmrc` 프로젝트별 노드버전 자동적용

위에는 위가 있는 법. 최종형태는 역시 자동대응. [Deeper Shell Integration](https://github.com/nvm-sh/nvm#deeper-shell-integration)을 설정하여 프로젝트마다 처음에 `.nvmrc` 파일만 설정해 두면 다음부터는 노드버전 변경이나 실행(`nvm use`)를 타이핑 할 필요가 없어진다.

페이지에 접근하면 설정 코드를 제공하고 있으니 복사해서 `.zshrc`파일에 적용하면 끝.

```shell
# nvm을 자동으로 확인 및 적용, 없으면 설치까지 자동대응
autoload -U add-zsh-hook
load-nvmrc() {
  local node_version="$(nvm version)"
  local nvmrc_path="$(nvm_find_nvmrc)"

  if [ -n "$nvmrc_path" ]; then
    local nvmrc_node_version=$(nvm version "$(cat "${nvmrc_path}")")

    if [ "$nvmrc_node_version" = "N/A" ]; then
      nvm install
    elif [ "$nvmrc_node_version" != "$node_version" ]; then
      nvm use
    fi
  elif [ "$node_version" != "$(nvm version default)" ]; then
    echo "Reverting to nvm default version"
    nvm use default
  fi
}
add-zsh-hook chpwd load-nvmrc
load-nvmrc
```

최종적으로 프로젝트를 왔다갔다 해보면 잘 적용된 것을 확인 할 수 있다. 중간에 버전 표시가 없는 건 16버전을 사용중인 프로젝트인데 nvm에서 default로 16을 지정해 둔 상태여서 버전 표시가 되지 않는 것이고, 나머지는 18버전이 자동으로 잘 적용되고 있다.

![pic](https://live.staticflickr.com/65535/53367396012_4b974d9cb0_o.gif)
