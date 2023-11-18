---
title: Gatsby - 날짜 형식 변경
pubDate: 2023-03-15
tags: ['blog', '리액트', 'react', 'Gatsby']
description: formatString을 수정해서 Gatsby에서 제공되는 날짜 형식을 연월일 순으로 변경
categories: react
---

## 영미권 년월일은 보기 불편하다.

당연히 영어 울렁증 때문이기도 하지만, 근본적으로는 년-월-일 순이 아니면 읽기가 거시기하다. 어떤 옵션을 건드려야 될까? 기본적으로 어떤 프로그램이던 날짜 형식을 사용할 경우 YYYY, MMMM, DD를 주로 사용한다.

Gatsby 테마에 따라 사용되는 파일들에 차이가 있을 것 같은데 지금 사용 중인 테마는 `gatsby-starter-blog`. 소스 검색을 하니 두 개의 파일(index.js, blog-post.js)에서 `formatString`으로 날짜 형식을 관리하고 있었다.

수정 전

```
date(formatString: "MMMM DD, YYYY")
> March 13, 2023
```

수정 후

```
date(formatString: "YYYY.MM.DD")
> 2023.03.13
```

일단 눈에 익숙한 정감 가는 순서로 정렬되었다.

## record 5

### 잘 모르니 헤매는 건 당연한 건데..

들어도 모르고, 읽어도 모르고, 다시 봐도 모르고 이해가 잘 가질 않으니 다른 게 눈에 들어오니 그쪽으로 시간을 할애해 버리고 있다.
맘을 다잡아야 하는데 쉽지도 않고. 분발하자.
