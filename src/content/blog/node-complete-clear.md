---
title: node 깔끔하게 지우기
pubDate: 2023-11-23
# updatedDate: 2023-11-23
tags: ['node', 'clean', 'brew', 'Homebrew', '지우기', '초기화']
description: 뭔가 잘 동작하지 않거나 지저분한 node 환경을 깔끔하게 지우는 방법을 알아 보게 되었다.
categories: node
---

Node 사이트에서 실행파일을 통해 설치한 경우

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

Homebrew를 사용해서 설치한 경우

```
brew uninstall node
brew doctor
brew cleanup
```
