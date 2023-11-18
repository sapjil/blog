---
title: (error) 리액트 작업 중 권한에러 발생시 대응 방법
pubDate: 2023-05-18
tags: ['blog', '리액트', 'react', 'js', 'error', 'VSCODE', '권한 문제']
description: VSCODE 작업 중, 권한 문제가 발생했을때 대응 법
categories: react
---

## 이런 문제는 왜 생기는지 근본적인 원인은 모르겠지만..

잘 동작하다가 꼭 내가 모르는 어떤 설정을 건드려서 생기는 문제가 있다.
이유를 전혀 모르니 더 문제다.

![error](https://live.staticflickr.com/65535/52907250818_4b82f85e35.jpg)

> Failed to save Insufficient permissions. Select 'Retry as Sudo' to retry as superuser.

이런 에러가 나오면서 저장할때, 삭제할때 모든 경우에 경고창을 보여주며 화를 내는 상황이 연출되고 있었다.

다행히 [stackoverflow](https://stackoverflow.com/questions/51674627/insufficient-permissions-in-vscode) 를 통해서 해결!

해결 방법은 폴더에 걸려 있는 권한을 풀어주면 되는 거였다.

```dos
sudo chmod -R 777 folder_name
```

적용하니 잘~ 돌아간다.

## record 7

### 리액트~ 리액트~

꽤나 긴 시간을 퍼블리셔로 지내오다 차세대 프로젝트라 불리는 react, vue등이 등장하면서 퍼블리셔라는 직군의 존재 가치가 없어져가는 시점임을 체감하고 있다. 한편으론 슬프지만, 이미 아이폰이 세상에 나오면서 플래시가 사라져 버린걸 목도한 경험이 있는 입장에서 시대의 흐름이라 생각되지만 빠르게 대응하지 못한 스스로를 다그치고 있는 실정이다. 이제는 조금만 더 시간이 지나면 퍼블리셔라는 직군이 사라지고 말 것 같다. 극소수의 한정된 곳에서는 분명 필요한 직군이고 일거리가 있겠지만 상대적으로 단가도 내려갈 것이라 예상된다. 결국 살아 남으려면 프론트엔드로 전향해야 하는데 과연 이 산을 넘어설 수 있을지 잘 모르겠다.
