---
title: CNAME을 활용해서 GitHub Pages에 커스텀 도메인 고정 시키기
pubDate: 2020-01-21
tags: 커스텀 도메인, CNAME, Custom Domain, Domain, GitHub Pages
description: GitHub Pages 커스텀 도메인을 등록했는데도 불구하고 배포 후에 404 페이지가 떠서 매번 주소를 다시 지정해 줘야 하는 경험을 해보신적이 있으신가요? 이 경우 CNAME을 지정하고 파일을 등록해 놓으면 이런 문제가 깔끔하게 해결됩니다.
categories:
  - www
# heroImage: '/blog-placeholder-2.jpg'
---

![GitHub Pages + Custom Domain](https://live.staticflickr.com/65535/49421742256_d2f522cfd7_c.jpg)

## 배포할 때마다 도메인을 다시 잡아 줘야 한다면

### 문제점

초반, GitHub Pages에서 `.io` 도메인을 사용한 페이지 작업을 완료했는데도 불구하고 배포를 한 뒤에 접속해 보면 매번 이렇게 404가 떴습니다. Setting에 들어가서 Custom domain을 잡아주면 문제는 해결되긴 했지만 근본적인 문제점은 모르는 상태였습니다.

![CNAME](https://live.staticflickr.com/65535/49417616392_69a710f745_c.jpg)

새롭게 배포 작업을 할 때마다 Custom domain에 도메인을 입력해야 하는 문제점은 이 작업 자체가 은근히 귀찮다 보니 조금씩 이런저런 이유를 들면서 블로그 작성도 미루곤 했었습니다.

### CNAME으로 해결

이번에 Gridsome으로 변경하면서 다시 한번 GitHub Pages의 설정 관련 정보들을 취합해 보며 알게 된 부분이 CNAME이었습니다. 이전 방식인 CNAME의 설정 전에도 배포가 된 뒤에는 CNAME이 생성된 것을 확인할 수 있었는데요. GitHub Pages 측에서 Custom domain을 사용할 때 이 파일을 생성한다는 것을 모르고 있었던 거였습니다. 로컬 작업에서는 당연히 생기지 않는 파일이다 보니 배포 후에는 딱히 생성된 파일에 관심을 두지 않았던 것이 원인이었습니다.

![CNAME](https://live.staticflickr.com/65535/49416927048_d1fddaf8d0_c.jpg)

일반적으로는 도메인 관리 쪽에서 도메인에 대한 `user.github.io`에 대해 CNAME을 설정하는 방식으로 잡고 있었습니다. 이것도 맞는 거지만 제가 진행한 방법은 단순히 배포한 뒤에 생성되는 CNAME 파일을 배포 전의 소스 파일 쪽에 받아 두고 그대로 배포를 진행하는 것이었습니다. 배포하면 배포되던 자리에 복사가 될 테니깐요.

제가 문제를 해결한 방법은 다음과 같습니다.

1. `github.io`에 배포 과정을 진행합니다.
2. Custom domain에 보유하고 있는 도메인을 입력 후 저장합니다.
3. 배포된 파일리스트를 확인해서 CNAME 파일이 있는지 확인합니다.
4. 해당 파일을 다운로드하거나 내용을 복사해 둡니다.
5. 배포된 파일 구조에 배포되도록 CNAME 파일을 소스 측의 적정 위치에 저장합니다.
6. 다시 배포 뒤 문제없이 잘 돌아가는지 확인합니다.

## CNAME 설정

일단 작업은 이전 단계에서 배포 시 생성된 파일을 소스파일 쪽에 두는 것으로 마무리가 되긴 했습니다.

<mark>여기서부터는 작업 진행 중에 공식 가이드를 보고 알게 된 내용에 대한 기록 같은 성격이라서 그냥 넘기셔도 좋을 듯합니다.</mark>

**GitHub Pages의 공식 가이드**: [https://help.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site](https://help.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site)

CNAME 설정 초반에 `www.domain.com` 식으로 도메인 관리 쪽에서 지정이 필요하다는 가이드를 보고 알게 된 내용입니다. 기본적으로 서브 도메인 쪽을 공란으로 두면 설정을 진행할 수 없기 때문이기도 하고 대표 도메인인 만큼 일반적인 `www`를 지정하는 방식을 기준으로 잡았습니다.

![CNAME](https://live.staticflickr.com/65535/49417616427_c0ab050130.jpg)

전 지금까지 `www`를 제외한 도메인을 주로 사용하고 있었기 때문에 추가적으로 `www`를 붙인 CNAME을 생성해 두었습니다만 결과적으로 CNAME의 `www`의 유무는 크게 영향은 없는 것 같습니다. 시험 삼아 이전 방식의 배포 당시 CNAME 파일을 열어 보니 `www`가 빠져 있기에 딱히 문제는 없어 보였습니다.

이 설정 부분은 자세한 설명 등은 GitHub Pages의 공식 가이드 문서에서도 확인 가능하니 참고하시기 바랍니다.

간단히 요약하면 다음과 같습니다.

1. 도메인 CNAME 관리 창에서 설정을 마칩니다.
2. CNAME을 설정한 후에는 `dig` 명령어로 도메인과 제대로 연결이 되어 있는지 확인 작업을 진행합니다.
3. GitHub Pages의 설정 화면의 Custom domain에 원하는 도메인을 지정합니다.

```
dig www.example.com +nostats +nocomments +nocmd
```

상기 명령을 통해 CNAME과 GitHub Domain IP가 제대로 연결이 되어 있는지를 확인합니다.

```
; <<>> DiG 9.10.6 <<>> WWW.EXAMPLE.COM +nostats +nocomments +nocmd
;; global options: +cmd
;WWW.EXAMPLE.COM.			IN	A
WWW.EXAMPLE.COM.		7200	IN	CNAME	example.github.io.
example.github.io.	3600	IN	A	185.199.110.153
example.github.io.	3600	IN	A	185.199.111.153
example.github.io.	3600	IN	A	185.199.109.153
example.github.io.	3600	IN	A	185.199.108.153
```

제대로 GitHub와 연결된 것을 확인할 수 있다면 성공입니다.
새롭게 연결을 시켜 주었을 경우 HTTPS설정이 적용되려면 시간이 좀 걸리는 편이니 몇 시간 뒤에 다시 재접속을 해보시면 됩니다. 보통 몇 시간 내로 가능하긴 한데요 최대 하루 정도는 생각하시는 게 맘 편하실 겁니다.
