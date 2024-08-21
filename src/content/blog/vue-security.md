---
title: Vue 시작부터 보안오류라고? PSSecurityException
pubDate: 2024-08-21
# updatedDate: 2024-08-16
tags: ['Vue', 'PSSecurityException']
description: Vue를 오랜만에 하면서 처음 경험하는 오류
categories: vue
heroImage: 'https://live.staticflickr.com/65535/53937394093_4043ef8c67_o.png'
---

## 간만의 Vue 프로젝트

이번에 들어갈 프로젝트는 Vue 프로젝트다. Vue를 해본 적은 있지만, 대충 5년 전... 아~~ 주 옛적에 해본 게 다여서 쉬는 동안 어디 휴가를 가기도 힘들고 놀면서 Vue나 공부해야겠다는 생각을 했었는데 생각보다 OTT나 보며 놀기만 하고 Vue를 들여다보지도 않아서 설치라도 해보자는 생각으로 프로젝트에 가지고 들어갈 노트북의 윈도즈를 밀고 새로 설치부터 시작해서 Node도 새로 깔면서 설치는 완료했다. 장비 가지고 들어가는 것도 오랜만인듯.

우선 설치는 되었다. 혹시 몰라서 vite를 설치하고 실행을 시켜보니 잘 돌아가는 것까지는 확인이 되었다. 그러다 별생각 없이 터미널을 통해 `vue --version`로 설치된 버전을 확인해보려 하니 에러가 나왔다.

```shell
# ERROR
vue : 이 시스템에서 스크립트를 실행할 수 없으므로
파일을 로드할 수 없습니다. 자세한 내용은 about_Execution_Policies
(https://go.microsoft.com/fwlink/?LinkID=135170)를 참조하십시오.
위치 줄:1 문자:1
+ vue --version
+ ~~~
+ CategoryInfo          : 보안 오류: (:) [], PSSecurityException
+ FullyQualifiedErrorId : UnauthorizedAccess
```

보안오류라니 이게 무슨 일인가.

해당 문제는 PowerShell 스크립트 실행 권한이 부여되어 있지 않다는 내용임을 확인하였다. 해결방법은 PowerShell을 관리자 권한으로 실행해서 다음 명령어를 적용하던가 VSCODE 터미널에서 적용하면 해결된다.

```shell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

일단 터미널 보안 문제 해결.
