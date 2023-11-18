---
title: Invalid input (items)에러 메세지가 나왔다. rss.xml.js의 문제로 build 실패 후 해결
pubDate: 2023-11-18
# updatedDate: 2023-11-10
tags: ['astro', 'Invalid input', 'rss.xml.js', '빌드 실패', 'error']
description: description
categories: astro
# heroImage: '/blog-placeholder-2.jpg'
---

이것저것 옵션을 건드려보면서 하나씩 알아보는 와중에 대충 소스 정리가 마무리된 것 같아 커밋을 하고 기다려도 빌드가 성공하지 않고 있었다. 깃허브 액션에 들어가 보니 에러로 막혀 있었다. 앞으로는 무조건 로컬에서 빌드 테스트를 한 후에 올려야겠다. 너무 안일하게 하고 있는 것 같다.

```astro
[RSS] Invalid or missing options:
  Invalid input (items)
  File:
    src/pages/rss.xml.js
```

해결 방법은 공식 사이트를 참고하여 해결할 수 있었는데 일단 문제가 되었던 소스는 `... post.data` 부분이었다. astro를 블로그 옵션으로 설치 후 수정하는 과정에서 생긴 문제라 생각된다.

```astro
return rss({
	title: SITE_TITLE,
	description: SITE_DESCRIPTION,
	site: context.site,
	items: posts.map((post) => ({
		...post.data,
		link: `/${post.slug}/`,
	})),
});
```

결국 해당 부분을 하나씩 직접 지정하니 문제가 해결되었다.

```astro
return rss({
	title: SITE_TITLE,
	description: SITE_DESCRIPTION,
	site: context.site,
	items: posts.map((post) => ({
		title: post.data.title,
		pubDate: post.data.pubDate,
		description: post.data.description,
		customData: post.data.customData,
		link: `/${post.slug}/`,
	})),
});
```

추측하건대 카테고리 출력 부분을 건드려 보며 좀 더 자세히 설정해야 하는데 몰라서 그 부분을 넘어가고 빌드 과정에서 해당 문제가 발목을 잡는 게 아닌가 싶다. 그래서 그 부분을 직접 하나씩 잡아주는 방법으로 회피시킨 게 아닐까... 그런 추측이다.
