---
title: node 지우기, 아주 깔끔하게 지우기
pubDate: 2023-11-23
# updatedDate: 2023-11-23
tags: ['node', 'clean', 'brew', 'Homebrew', 'nvm', '지우기', '초기화']
description: 뭔가 잘 동작하지 않거나 지저분한 node 환경을 깔끔하게 지우고 새로운 마음으로 설치하자
categories: node
---

사무실에서 사용 중인 node는 버전 16인데 업무가 비는 공백시간에 개인 공부를 좀 해보려고 했더니 노드 버전에 문제가 있었다. `node -v`로 확인하면 기본으로 깔려 있는 노드는 19. 프로젝트에서 사용 중인 기준은 16. 내가 공부하는 건 18. 뭐 대충 이런 느낌인데.. 애매한 19?를 지우고 깔끔하게 16과 18만을 사용하기 위해 우선적으로 Node를 깔끔하게 지우고 싶었다.

## nodejs.org에서 실행파일로 설치한 경우

가장 많은 경우에 해당하는 실행파일로 설치한 경우, 다음을 실행시켜 주면 설치된 노드가 깔끔하게 지워진다.

```
sudo rm -rf /usr/local/lib/node
sudo rm -rf /usr/local/lib/node_modules
sudo rm /usr/local/lib/dtrace/node.d
sudo rm /usr/local/share/man/man1/node.1
sudo rm -rf /usr/local/share/doc/node
sudo rm -rf /usr/local/share/systemtap/tapset/node.stp
sudo rm -rf /usr/local/include/node
sudo rm /usr/local/bin/node
sudo rm /usr/local/bin/npm
sudo rm /usr/local/bin/npx
```

## Homebrew를 사용해서 설치한 경우

```
brew uninstall node
brew doctor
brew cleanup
```

## 지웠으면 이제 nvm을 설치

다 지워진것을 확인하고 16과 18을 설치하기 위해 [nvm을 설치](/nvm-node-version-manager/)했다.
당연히 업무가 우선이기 때문에 기본 버전은 16을 지정해 두었다.

```
nvm alias default 16
```
