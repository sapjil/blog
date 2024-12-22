---
title: 작업이 완료되면 rebase로 브런치 이력을 깔끔하게 해서 전달하자
pubDate: 2024-11-24
# updatedDate: 2024-08-16
tags: ['git', 'squash', 'merge', 'rebase']
description: rebase 사용하는 방법
categories: git
heroImage: 'https://live.staticflickr.com/65535/53786479953_c2b2fcff2e_o.png'
---

## Rebase를 사용하게 된 계기

그동안 프로젝트를 하면서 rebase를 사용할 일이 없었다. 혼자 작업을 하건 팀 작업을 하건 크게 신경 쓰지 않고 진행을 했었다. 이유는 딱히 누가 요청을 하지도 않거니와 그냥 필요한 사람이 알아서 가져가기에 신경 자체를 쓰지 않았는데 지금 생각해 보면 참 편하게 일했던 것 같다. 개발소스에 크게 영향을 미치지 않는 마크업 작업을 위주로 해서 그런 것이라 생각된다. 그런데, 이번 프로젝트에서는 단순 마크업이 아니라 초급 프런트앤드 업무를 약간 겸업을 하게 되면서 좀 더 git 활용이 많아짐에 따라 주의가 필요했다.

처음 프로젝트에 참가했을 때는 마크업도 dev 브런치에 바로 push를 하면서 작업을 진행했었지만, 기존 소스의 정리가 어느 정도 되면서 Git Flow를 재정의 하는 작업이 있었고 이후로는 마크업을 직접 dev에 push 하는 일이 없어졌다. JIRA에서 발급된 티켓을 기준으로 브런치를 만들고 마크업이 필요한 경우도 동일한 티켓을 기준으로 작업이 진행되었다.

평소처럼 별도 브런치에서 작업된 내용과 함께 해당 브런치를 알려주니 squash로 묶어서 작업 파일 목록을 확인할 수 있도록 하나로 달라는 요구를 받았던 것이 시작이다. 개발자로선 당연히 작업 진행 내역을 모르기도 하거니와 `merge --squash`로 당겨가는 것도 귀찮을 수 있는 일이라 생각되었다. 최종 하나만 가져가면 해결되니 가져가는 사람도 편하고, 작업했던 나 역시 작업 이력을 정리하게 되고 브런치도 깔끔해진다. 우리 모두 happy~ 그렇게 머리로 이해하고 작업을 하는 것과 달리 기록을 해둔 적이 없었기에 작업을 시작했다.

## Rebase 과정

크게 작업은 5단계로 나뉜다고 생각된다. 만약 git에 대한 이해가 별로 없다면 이 그림이 뭔지 이해하기 어려울지도...

![](https://live.staticflickr.com/65535/54159372253_852de83306_o.png)

### 1. main에서 checkout

main에서 작업 브런치인 feature1을 checkout

```
git checkout -b feature1
```

### 2. feature1에서 작업진행

신나게 작업 후, 작업 내용을 날리지 않도록 주의하면서 자주 커밋.
작업이 마무리된 이후는 작업 내용을 정리하는 작업을 진행. 이 경우 3단계의 작업 이력이 있다고 가정하겠다.

### 3. 작업 완료 후 rebase

개인적으로는 VSCODE의 Git Graph와 GitLens 플러그인(UI)을 애용하는 편이다. 기본적인 명령어는 터미널 사용이 편하긴 한데 이상하게 Vim은 익숙해지지 않는다는 난점이..
터미널에서 해당명령어를 실행하면 VSCODE가 실행되고 GitLens가 실행되면서 터미널이 아닌 UI를 통해 squash 과정을 진행할 수 있다.

```
git rebase -i HEAD~3
```

#### 3-1. Git 기본 사용 시

기본 화면으로 사용할 경우는 first에 squash 해주기 위해 second, third의 pick을 squash로 바꿔주면 squash가 진행된다.

![](https://live.staticflickr.com/65535/54160497819_73ed5700ef_o.png)

#### 3-2. GitLens 사용 시

상기 과정과 동일한 방법을 UI를 통해 작업할 수 있는데 개인적으로는 이쪽을 선호하는 편이다. squash를 선택하고 우측하단의 start rebase를 하면 된다.

![](https://live.staticflickr.com/65535/54160642255_c0d047e781_o.png)

작업이 마무리되면 신규 commit을 남길 수 있게 된다.

![](https://live.staticflickr.com/65535/54160463013_aa33cb40b1_o.png)

### 4. rebase완료된 내용을 feature1에 강제 push

rebase 과정이 완료된 뒤에는 브런치가 feature1에서 잠시 분리되어 있는 상황이 된다. 이때 `push -f`로 현재 이력을 강제로 `origin/feature1`로 push 해준다. 맘 놓고 강제로 push 하는 이유는 해당 브런치는 나만 작업하고 있는 독립된 브런치이기 때문인데 개발은 모든 이력이 정리된 마지막 브런치만 가져가면 되는 상황이라 서로 문제가 생긴 경우는 아직까지 없었다.

```
git push -f
```

### 5. 내 작업은 끝

이후 작업은 개발자가 알아서 당겨가면서 작업하면 된다. 상기 내용을 그림으로 정리하면 다음과 같을 것 같다. 나름 정리한다고 한 그림... 이해하지 못하는 사람은 없겠지...? 만약 틀린 곳이 있다면 당신이 옳습니다..
![](https://live.staticflickr.com/65535/54159372253_852de83306_o.png)

## record 19

### 도전의 연속

서두에 잠시 언급했지만 약간 초급 프런트앤드 비슷한(?) 업무를 병행하고 있다. 간과하고 있었던 노트북의 메모리 문제라던지, 하드 파티션이라던지 DB를 돌리면서 작업하는 과정은 확실히 장비빨이 필요하다는 것을 알 것 같은 요즘이다. 항상 로컬에서 마크업용으로 Dummy.js이나 json 파일을 만들어서 작업하다 보니 확연한 차이를 느낄 수 있었다. 무겁다. 무척. 그래도 새로운 기회가 열린 것이라 생각하고 나름 즐겁게 진행 중이다. 이 기회를 살릴 수 있는지는 이제 두고 봐야만 알 수 있는 일.