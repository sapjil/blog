---
title: 워드프레스 - 한글(2byte) 인식 문제
pubDate: 2016-07-26
tags: 404, error, url, search, htaccess, search console, googlebot, crawling errors, solve, 크롤링 에러, 구글 봇, 서치콘솔, 에러 페이지, URL오류, 문제해결
description: 한글(2byte)의 특성으로 생기는 문제라고 생각되는 구글 Search Console에서 크롤링오류가 있었습니다. URL오류의 문제를 인식하는 부분에서 생기는 것으로 파악되었으며, htaccess의 수정으로 일부 해결할 수 있었습니다.
categories:
  - solve
# heroImage: '/blog-placeholder-2.jpg'
---

![wp-2byte-404](https://c2.staticflickr.com/8/7563/27846910513_d616ae1dc0_c.jpg)

구글 Search Console에서 계속 크롤링에러에서 'URL오류'가 많이 검출되고 있습니다.

## 크롤링 오류

![Search Console - 크롤링 오류](https://c7.staticflickr.com/9/8893/28357567622_5742137f1b_c.jpg)

딱 보기에도 한글이 깨지는 현상이 생기고 있는데요.
이 상태로 링크를 클릭하면 404페이지로 넘어가 버리고 말아버립니다.

![Search Console - 크롤링 오류](https://c1.staticflickr.com/8/7693/28429955296_dfaf583bee_c.jpg)

한글이 깨지는 문제도 문제이지만, '내 페이지로 링크된 도메인'을 선택후의 한글주소로의 링크를 선택하여도 404페이지로 가는 것이었습니다.

![Search Console - 크롤링 오류](https://c3.staticflickr.com/9/8379/28357567722_6a0a5c054e_c.jpg)

![Search Console - 크롤링 오류](https://c4.staticflickr.com/9/8814/28462297555_9ff31f8526_c.jpg)

Oops!

> “URL이 존재하지 않는 페이지를 가리키고 있어서 Googlebot이 이 URL을 크롤링하지 못했습니다. 일반적으로 404는 사이트의 검색결과 게재순위를 낮추지 않으며, 오히려 이를 활용하여 사용자 환경을 개선할 수 있습니다.”

다행하게도 Search Console에서는 404페이지에 대해서 다음과 같은 안내를 해주고 있었기에 크게 고민을 하고는 있지 않았었지만 슬슬 문제를 해결해야 겠기에 여기저기 구글링을 하다가 드디어 단편적이긴 하지만 해결방법을 발견하였습니다.

일단 문제는 서버환경이었다는 것을 알게 되었습니다.

![Search Console - 크롤링 오류](https://c3.staticflickr.com/8/7622/28430206106_63d4c9cba2_c.jpg)

이상한것이 제가 사용중인 서비스의 환경에는 UTF-8로 지정되어 있다는 거였죠.
이러면 문제가 없어야 하는데 문제가 있었던 겁니다.

기술적인 부분까지는 모르겠지만 우선 .htaccess의 설정을 수정하여주었습니다.
.htaccess에 대해서도 공부해야 겠습니다…

```
<IfModule mod_url.c>
ServerEncoding UTF-8
ClientEncoding EUC-KR
</IfModule>
```

그리고 수정한 파일을 FTP로 업로드하고 한글로 된 테그를 클릭했더니 ‘짜~잔’ 무사히 링크가 되는걸 확인 할 수 있었습니다.

**참고**

- [워드프레스 한글 태그 검색시 404 오류 해결하기](http://www.dodofafa.co.kr/%EC%9B%8C%EB%93%9C%ED%94%84%EB%A0%88%EC%8A%A4-%ED%95%9C%EA%B8%80-%ED%83%9C%EA%B7%B8-%EA%B2%80%EC%83%89%EC%8B%9C-404-%EC%98%A4%EB%A5%98-%ED%95%B4%EA%B2%B0%ED%95%98%EA%B8%B0/)
