---
title: Github Action으로 편리해진 Firebase 호스팅
pubDate: 2023-11-04
updatedDate: 2023-11-05
tags: ['firebase', 'sapjil', 'hosting', '정적사이트']
description: Github에서 사용하던 블로그를 firebase로 옮기면서 Action을 통해 사용하기 쉬워진 배포시스템의 덕을 볼 수 있었다.
categories: firebase
heroImage: https://live.staticflickr.com/65535/53786362586_188527e299_o.png
---

## Firebase Hosting 사용

정말 개인이 사용하는 사이트는 Firebase로 충분하지 않을까 싶은 생각이 들었다. 도메인에 대한 욕심이 없다면 도메인 비용, 호스팅 비용을 모두 공짜로 사용가능한 방법은 티스토리나 네이버 블로그 등도 있지만, 이상하게도 IT 진영에 있는 사람들은 자기 손으로 만들거나 관리할 수 없는 것에 대한 미묘한 저항이 있는 것 같다는 생각이 들기도 한다.

Gridsome을 사용하던 때는 github에서 모든 것을 관리했었는데 이번에 Astro로 넘어오면서 Firebase로 이사를 시켰다. 별다른 이유는 없고 다른 블로그(<a href="https://react.sapjil.net/">리액트 공부 기록</a>)를 작성하는 데 사용 중인 방식을 그대로 적용시켜 본 경험이 가장 크다.

문제는 인간은 망각의 동물이라고 하던가. 본 내용은 과정이 잘 기억이 나질 않아 기록차원의 포스팅이 되겠다. 이전에 다룬 적이 있던 <a href="/blog/changed-gridsome/">Gridsome 배포과정</a>과 비교하면 정말 너무 쉬워진 것 같다. 그때나 지금이나 자동화 배포에 관한 지식은 없는데도 꾸역꾸역 해나가고 있지만 그 과정이 쉬워진걸 느끼니...

## 설정방법

```
# firebase hosting 미설치한 경우
firebase init hosting

# firebase hosting 설치한 경우 :github 추가
firebase init hosting:github
```

실행하게 되면 명령어가 달리며 다음과 같은 질문들을 하지만 대체로 알아서 찾아주고 어렵지 않은 내용들이다.

| #   | 질문                                                                            | 질문                                                  | 답변                                            |
| --- | ------------------------------------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------- |
| 1   | For which GitHub repository would you like to set up a GitHub workflow?         | Action을 설정할 레파지토리                            | sapjil/firebase-hosting-sapjil-blog             |
| 2   | Set up the workflow to run a build script before every deploy?                  | 호스팅 전에 빌드과정여부                              | 사전 빌드 과정이 필요한 경우 → Y / 반대라면 → N |
| 3   | What script should be run before every deploy?                                  | 빌드에 사용될 스크립트                                | npm ci && npm run build                         |
| 4   | Set up automatic deployment to your site's live channel when a PR is merged?    | 풀 리퀘스트나 머지시 운영 서버에 머지 시킬것인지 여부 | Y / N                                           |
| 5   | What is the name of the GitHub branch associated with your site's live channel? | 운영 서버에 머지시 사용할 브런치                      | main                                            |

하나씩 답변을 해주면 최종적으로 `/.github/workflows/` 폴더가 생성되며 배포를 위한 설정파일들이 생성된 것을 확인할 수 있게 된다.

이 과정을 통해 앞으로는 로컬에서 테스트를 통해 화면에 어떻게 보이는지 확인 작업을 하고 깃으로 push만 해주면 자동으로 깃에서 Action이 돌아가며 Firebase로 배포를 해주게 된다. 파일의 크기, 콘텐츠의 양에 따라 빌드시간이나 배포시간에 차이는 있겠지만 이 과정이 모두 무료로 제공되고 있으니 아주 만족스럽다.

## 참고

https://zenn.dev/watarukun/articles/8f3e318bacf97cabf879
