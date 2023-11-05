---
title: 생각보다 쉬운 Git 사용해보기
pubDate: 2016-09-10
tags: 백업, 버전관리, 깃, 깃허브, 비트버킷, 온라인, 오프라인, 커밋, commit, origin, reset, master, bitbucket, github, hard, push, init, ignore
description: 업무에서 백업용으로만 사용하던 git. 혼자서 작업할 경우 필요하다고 생각되는 생각보다 쉬운 사용법(?)을 정리해봤습니다.
categories:
  - www
# heroImage: '/blog-placeholder-2.jpg'
---

이번에는 “git”에 대해서 전문적인 부분이 아닌, 삽질을 조금이나마 줄일 수 있는 기본적인 <mark>백업용도에 대한 사용법</mark>에 대하여 다루려 합니다. 이전부터 “git”은 사용해 왔었습니다만, 백업용으로만 사용해 오고 있었는데… 슬슬 프로젝트에도 제대로(?) 도입을 시켜보기 위해 이런저런 사용법을 조금씩 익히고 있는 중입니다. git, 생각보다 쉬워요. 네. 저도 사용하고 있는걸요.

![sapjil-git](https://farm9.staticflickr.com/8453/29423992182_8bd228d4af_c.jpg)

> “git”을 이미 사용중이신 분은 읽어 보실 필요 없다고 생각되며, 전혀 사용해 본적이 없는데 어떻게 사용해 보면 좋을지 모르겠다는 저보다 초보분들을 생각하면서 정리해봤습니다. 이 포스트를 읽는데는 약 3분 정도의 시간을 필요로 합니다.

기본적으로 **[Github](http://github.com/)**를 사용하면 좋겠지만, Private을 희망할 경우 유료입니다.. 아무리 허접한 소스라도 누군가가 볼 수도 있다는 거부감에 유료. 그래서 저는 무료로 사용가능한 **[Bitbucket](http://bitbucket.com)** 서비스를 사용하여 Private 모드로 백업하고 있습니다.

그저 백업에 중점을 두고 사용해 왔었기 때문에 “git” 에 대해서 전체적으로 다룰 정도로 알고 있지는 않다는 걸 다시한번 상기하시면서…

**table of contents**

1. [Bitbucket에 저장소 만들기](#Bitbucket에-저장소-만들기)
2. [git의 작업흐름](#git의-작업흐름)
3. [commit 해보기](#commit-해보기)
4. [태그 걸어보기](#태그-걸어보기)
5. [commit을 잘못했다면](#commit을-잘못했다면)
6. [gitignore 설정하기](#gitignore-설정하기)

## Bitbucket에 저장소 만들기

당연한 수순이지만, 온라인상에 파일을 저장해야하니 서비스를 이용하기 위해서 우선은 사이트를 방문하여 계정을 생성합니다. Bitbucket 은 무료로 Private 설정이 가능한 Github 라고 생각하시면 좋을 것 같습니다.

[http://bitbucket.com](http://bitbucket.com)

회원가입을 완료하신후 상단 메뉴에서 Repository를 통해 Repository를 생성시킵니다.
![Create a repository](https://c7.staticflickr.com/9/8885/29529917366_658105fae4_b.jpg" 'Create a repository — Bitbucket')

생성된 이후에 Command line 아래의 I'm starting from scratch을 선택하시면 아래와 같은 형식의 고유의 주소가 생성 되어 있는것을 확인 하실 수 있을겁니다.

![_sapjil - Bitbucket](https://c5.staticflickr.com/9/8219/28938609284_12fcb02deb_b.jpg" '_sapjil — Bitbucket')

이 주소는 나중에 필요하니 따로 적어 두시거나 주소의 확인이 필요한 경우를 위해 메뉴 위치를 기억해 두시게 좋을것 같습니다.

## git의 작업흐름

“git”은 순차적으로 진행 하였을 경우, 기본적으로 다음과 같은 순서를 경유하게 됩니다.

| 단계  | 저장소              | 비고                          |
| ----- | ------------------- | ----------------------------- |
| step1 | Working directory   | 실제 작업폴더                 |
| step2 | Index(Staging area) | git에 등록하기 전의 준비 영역 |
| step3 | HEAD                | 최종본을 등록해 두는곳        |
| step4 | master              | 온라인 저장소                 |

step1 의 작업폴더에서 step2 의 준비영역(staging area)로 파일을 등록합니다. 그리고 step3 으로 최종확정본(commit)을 등록을 하게 됩니다. step3 까지는 오프라인상에서 이루어지는 작업이며 step4 의 `push`를 통해 온라인상의 `master`에 등록하게 되면 일련의 작업이 끝나게 됩니다. 쉽죠?

다시 정리하면.. <mark>step3 까지는 오프라인, step4 부터는 온라인</mark>으로 구분된다고 보시면 됩니다. 즉, 굳이 온라인 저장소에 저장할 필요는 없지만, 버전관리가 필요한 경우 오프라인에서 작업을 진행해도 상관없다고 할 수도 있겠습니다.

## commit 해보기

우선, 프로젝트를 생성합니다.
터미널을 열고 작업할 폴더(Working directory)를 찾아갑니다.

```
$ cd Working-directory
```

그 다음으로 `init` 명령어를 사용하여 해당 폴더가 작업영역임을 지정합니다.

```
$ git init
```

`add <파일명>` 명령어로 작업한 내용을 임시저장소에 등록합니다만, 만일 작업내용 전체를 등록할 경우는 `add *`를 사용합니다.

```
// 해당 파일만 등록할 경우
$ git add 파일명

// 작업전체를 등록할 경우
$ git add *
```

다음에는 작업한 내용에 관한 메모를 `-m`명령어를 사용하여 기록합니다.

```
$ git comment -m "first comit"
```

이제 마지막으로 Bitbucket 에 저장한 내용을 등록할 차례입니다. `push`명령어를 사용하여 온라인 저장소에 등록을 시작합니다.

```
$ git push origin master
```

> `origin`, `master`
> “master” 에는 특별한 의미가 있는 것은 아니며 `init`명령이 자동으로 생성시키는 이름입니다. 또한 “origin” 역시 특별한 의미가 있는 것은 아니라 `clone` 명령이 자동으로 만들어주는 리모트 이름입니다.
> [Git 브랜치 - 리모트 브랜치](https://git-scm.com/book/ko/v2/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%A6%AC%EB%AA%A8%ED%8A%B8-%EB%B8%8C%EB%9E%9C%EC%B9%98) 참조

만약 등록이 이루어지고 있지 않다면 온라인 저장소를 지정해주지 않은 것이 예상되는 경우입니다. 이때는 `remote` 로 온라인 저장소를 지정해줄 필요가 있습니다.

```
$ git remote add origin 온라인 저장소의 URL
```

위와 같이 저장소를 지정해준 후에 다시 상기의 `push` 명령어를 실행하시면 업로드 상황을 파악할 수 있습니다.

## 태그 걸어보기

계속 작업을 하다보면 중요한 업데이트가 있었던 때에 표식을 남겨둘 필요가 있습니다. 이력이 길어지면 어디에 어떤 식으로 `commit` 을 했는지 찾기가 힘들어지기 때문에 중요한 업데이트, 심각한 버그의 수정, 오픈일 등등.. 그럴때 사용하면 좋을 기능입니다.

```
$ git tag 태그명
```

## commit을 잘못했다면

가끔 발생하는 일 입니다만… 실수로 파일을 `commit` 하였거나 업데이트가 불가능한 경우. 이유도 잘 모르겠다 싶은 경우가 생깁니다. 비슷한 경험들이 있으시겠지만, 이럴때는 가장 최근 작업으로 완전히 돌아가서 작업하는게 속 편할때가 있습니다.
`fetch`, `reset` 으로 깨끗하게(?) 최신이력으로 돌려버립니다.

```
$ git fetch origin
$ git reset --hard origin/master
```

> `reset`, `--hard`
> 간단히 설명하면(?) “--hard” 옵션은 “reset” 을 할경우 어디까지 되돌리는지를 결정하는 옵션중의 하나입니다. 또한, “--hard”은 “git” 의 세가지 저장소(HEAD, Index, Working directory)에서 되돌리는 과정중 가장 강력한 옵션입니다. 이처럼 강력한 옵션인 만큼 주의도 필요합니다.
> [Git 도구 - Reset 명확히 알고 가기](https://git-scm.com/book/ko/v2/Git-%EB%8F%84%EA%B5%AC-Reset-%EB%AA%85%ED%99%95%ED%9E%88-%EC%95%8C%EA%B3%A0-%EA%B0%80%EA%B8%B0) 참조

## gitignore 설정하기

`ignore` 파일을 업데이트 시켜야 하는데 이미 `commit` 을 해버린 뒤라면 `ignore` 파일을 작성하여도 적용되지 않는 문제가 발생함으로 이러한 경우는 해당 파일의 체크를 해제한후 `ignore` 파일에 무시할 규칙을 적용시킨뒤에 다시 `commit` 하면 문제를 해결 할 수 있습니다.

```
$ git rm --cached .DS_Store
$ git commit -m 'untrack .DS_Store'
```

이제 파일을 추적하지 않게 되었음으로 `.gitignore`파일에 필요한 내용을 추가 시킨후 `commit` 해 주면 됩니다.

파일이 아닌 폴더를 지정하고 싶은 경우라면 `/.DS_Store` 처럼 잡아주면 가능합니다. 주로 맥으로 작업을 하다보니 기본적으로 설정해 두는 내용은 아래 정도입니다.

```
.DS_Store
Thumbs.db
desktop.ini
```

이외에도 `zip`, `rar`같은 압축파일이나 `psd`, `ai` 같은 이미지 파일을 적용시켜두기도 합니다.

## 마치며

지금까지 날림이긴 합니다만 제가 사용중인 “git”의 사용법에 대해서 언급해 보았습니다. 프로그래머나 자주 사용하시는 분들이 보시기엔 별 도움이 되지 않겠지만, 아직까지 “git”을 사용해 본적이 없었던 분들에게 조금이나마 도움이 되었으면 좋겠습니다.
