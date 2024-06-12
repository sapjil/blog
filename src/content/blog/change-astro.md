---
title: Changed to Astro
pubDate: 2023-11-03
updatedDate: 2023-11-18
tags: ['sapjil', '삽질', 'Astro']
description: Gridsome에서 Astro로 넘어오게 된 이야기
categories: www
# heroImage: '/blog-placeholder-about.jpg'
# heroImage='/blog-placeholder-about.jpg'
heroImage: 'https://live.staticflickr.com/65535/53786675855_ed3dc09c60_o.png'
---

<img src="https://live.staticflickr.com/65535/53308273903_1d6030c9d0_b.jpg" alt="blog-placeholder-astro"/>

그동안 Gridsome을 사용해서 그나마 남겨놓고 있던 Sapjil이지만, 일년전인가 한번, 그리고 몇달전에 다시 한번 업데이트를 위해 작업을 하려 할때마다 오류와 맞딱뜨리며 그때마다 포기를 하게 되었다.

새로 설치를 해도 실행이 되질 않는데 이유는 모르겠고 되지도 않는 Gridsome을 해결하기 위해 머리를 감싸고 외국 사이트를 돌아다니는 것보다 최근 Astro에 관심이 생기고 이쪽이 스트레스를 받지 않을 것 같아 Astro로 옮기기로 했다. 이사 자체는 어렵지 않았다.

## 기존 Gridsome

```md
---
title: Changed to Astro
description: Gridsome에서 Astro로 넘어오게 된 이야기
date: 2023-11-03
tags: ['sapjil', '삽질', 'Astro']
---
```

## Astro

```md
---
title: Changed to Astro
description: Gridsome에서 Astro로 넘어오게 된 이야기
pubDate: 2023-11-03
tags: ['sapjil', '삽질', 'Astro']
---
```

`.md` 파일의 기본적인 부분의 수정, `date`를 `pubDate`로 바꾸기만 해도 일단 페이지 표시에는 문제가 없었으며 카테고리나 페이지간 이동등 몇몇 부분은 좀 더 익혀봐야 겠지만 현재로선 마음에 드는 것 같다.

### 2023-11-18 update

astro의 `tag` 표시 방법의 일부를 알게 되어서 업데이트. 처음부터 알았다면 두번 작업할 일이 없었을 건데..(-\_-)
