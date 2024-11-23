---
title: Vue SASS 설정
pubDate: 2024-08-22
# updatedDate: 2024-08-16
tags: ['Vue', 'SASS', 'SCSS', 'CSS', 'style', 'vue-cli']
description: Vue에서 SASS 설정 방법
categories: vue
heroImage: 'https://live.staticflickr.com/65535/53937394093_4043ef8c67_o.png'
---

## 간만의 Vue, SASS 설치

간만에 Vue를 작업하니 정말 기억이 새롭다. 모든것이 새롭다. 기록해 두지 않으면 또 잊어버릴것이 분명하기에 Vue에서 sass를 사용하기 위한 설치과정을 기록.

npm이나 yarn으로 `sass`와 `sass-loader`를 설치

```shell
yarn add sass sass-loader
```

## Vue에서 SASS 설정

### SASS 설정 1: main.js

일반적으로 가장 익숙한 작업 방식으로 `style.scss`을 설정 후 나머지 파일을 `@import` 시키거나 컴포넌트에 따라선 `scope`로 컴포넌트에 국한되도록 설정하면 된다.

```shell
# main.js
import './path/to/style.scss';
```

### SASS 설정 2: vue.config.js

sass에서 사용가능한 변수($) 모음 파일을 만들고 설정해 두면 이후부터는 어느 파일에서건 참조해서 사용가능하게 된다.

- [passing options to pre processor loaders](https://cli.vuejs.org/guide/css.html#passing-options-to-pre-processor-loaders)

```shell
# variables.scss
$pc: 1080px;
$mb: 480px;
$primary: #c00;
$second: #c0c;
```

```shell
# vue.config.js
const { defineConfig } = require('@vue/cli-service');
module.exports = defineConfig({
  publicPath: '',
  css: {
    loaderOptions: {
      scss: {
        additionalData: `"@import "@/path/to/variables.scss";`
      }
    }
  }
});
```

## record 18

### 시간이 빠르게 흐른다.

Vue를 사용해 본 것이 4년정도 이전의 이야기이다. 그사이 뷰에도 많은 변화가 있었는데 별로 접할 수 있는 기회가 없었다.
