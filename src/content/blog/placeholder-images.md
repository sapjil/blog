---
title: 샘플이미지를 간단하게 삽입하기 - Placeholder images
pubDate: 2016-07-21
tags:
  [
    'placeimg',
    'ipsumimage',
    'placehold',
    'lorem ipsum',
    'demo',
    'generator',
    'placeholder image',
    'random image',
    'sample image',
    'dummy image',
    '랜덤 이미지',
    '더미 이미지',
    '샘플 이미지',
    '무료',
  ]
description: 데모사이트를 만들때 분위기를 맞추기 위하여 이미지툴로 무의미한 이미지를 제작하거나 웹상에서 아무 이미지나 다운받아 사용하곤 했다면 간편하게 사용가능한 Placeholder images 서비스를 사용하여 보시기 바랍니다.
categories: www
# heroImage: '/blog-placeholder-2.jpg'
---

![sapjil-placeholder-images](https://c2.staticflickr.com/9/8874/27787597153_a6db36a2d9_b.jpg)

이전에는 데모사이트를 만들때 분위기를 맞추기 위하여 무의미한 이미지를 다운받아 사용하곤 했습니다. 요새는 경우에 따라 다르기도 하고 자주 사용하는것은 아니지만, 필요한 경우 Placeholder images 서비스를 사용하곤 합니다. <mark>은근 편한 서비스여서 소개해 봅니다.</mark>

```
<img src="서비스주소/옵션" />
```

기본 형식은 어느서비스나 닮은꼴을 하고 있으며, <mark>플러그인등의 설치가 필요없이 html에 URL형식의 정보를 입력하기만 하면 서비스를 바로 사용할 수 있습니다.</mark>

**table of contents**

- [텍스트형식 서비스](#텍스트형식)
  - [가장 간편하게 사용할 수 있었던 Placehold.it](#가장-간편하게-사용할-수-있었던-Placehold.it)
  - [키워드 제공이 눈에 띄는 ipsumimage.appspot.com](#키워드-제공이-눈에-띄는-ipsumimage.appspot.com)
- [이미지형식 서비스](#이미지형식)
  - [카테고리 지정이 가능한 placeimg.com](#카테고리-지정이-가능한-placeimg.com)

## 텍스트형식

### 가장 간편하게 사용할 수 있었던 Placehold.it

우선 기존에 사용하던 서비스는 placehold라는 곳입니다.
텍스트 형식을 제공하고 있어 속도적인 측면에서 우수하다고 생각됩니다.
정사각형의 이미지가 필요한 경우는 수치를 한변만 입력하면 됩니다.

```
<img src="http://placehold.it/320x100" />
<img src="http://placehold.it/100" />
```

<img src="http://placehold.it/320x100" />
<img src="http://placehold.it/100" />

텍스트로 된 정보를 제공할 필요가 있을때 사용하는 옵션이 있으며,
배경색을 적용하고 싶을 경우에는 먼저 배경색을 지정후에 텍스트 색상을 지정해 주어야 합니다.

```
<img src="http://placehold.it/320x100?text=sample" />
<img src="http://placehold.it/320x100/E8117F/ffffff?text=sample" />
```

<img src="http://placehold.it/320x100?text=sample" />
<img src="http://placehold.it/320x100/E8117F/ffffff?text=sample" />

[http://placehold.it](http://placehold.it)

### 키워드 제공이 눈에 띄는 ipsumimage.appspot.com

cga, qvga, vga, skyscraper등의 키워드([DummyImage standard image size](http://dummyimage.com/#standards))를 사용하면 이미 지정되어 있는 사이즈의 이미지를 사용할 수 있습니다.

```
<img src="http://ipsumimage.appspot.com/qvga" />
```

<img src="http://ipsumimage.appspot.com/qvga" />

텍스트 사용이 필요할 경우 문장에 '|'를 사용하여 줄바꿈을 줄 수도 있습니다.

```
<img src="http://ipsumimage.appspot.com/320x100" />
<img src="http://ipsumimage.appspot.com/320x100?l=Ipsum+Image|Hosted+on+GAE" />
```

<img src="http://ipsumimage.appspot.com/320x100" />
<img src="http://ipsumimage.appspot.com/320x100?l=Ipsum+Image|Hosted+on+GAE" />

[http://ipsumimage.appspot.com](http://ipsumimage.appspot.com/)

## 이미지형식

### 카테고리 지정이 가능한 placeimg.com

두번째는 이미지형식의 placeholder 서비스를 제공하고 placeimg입니다.
placehold와 같은 텍스트 형식은 지원하지 않는 것 같으며 임의로 특정이미지를 지정할 수는 없습니다.

이미지 사이즈 뒤에 이미지의 카테고리를 설정해 줍니다.
디폴트는 any로 되어 있으면, Animals, Architecture, Nature, People, Tech의 5개의 카테고리에 Grayscale, Sepia형식의 필터 2가지의 조합으로 된 서비스입니다.

우선 기본값인 any의 적용상태로 페이지를 새로 고침할때마다 새로운 이미지가 표시됩니다.

```
<img src="https://placeimg.com/320/100/any" />
```

<img src="https://placeimg.com/320/100/any" />

grayscale, sepia 필터를 적용해본 예입니다.

```
<img src="https://placeimg.com/320/100/any/grayscale" />
<img src="https://placeimg.com/320/100/any/sepia" />
```

<img src="https://placeimg.com/320/100/any/grayscale" />
<img src="https://placeimg.com/320/100/any/sepia" />

[https://placeimg.com](https://placeimg.com)
