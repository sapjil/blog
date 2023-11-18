---
title: 모바일 웹페이지 디버깅에 적합한 weinre
pubDate: 2016-01-01
tags:
  [
    '모바일',
    '웹페이지',
    '디버깅',
    '노드JS',
    'iPhone',
    'Android',
    'Debugging',
    'weinre',
    'mobile',
    'web page',
    'nodejs',
    'sapjil',
  ]
description: 모바일 웹페이지를 작업할 경우, node.js기반의 weinre를 사용하게 되면 케이블을 연결할 필요도 없고 iPhone/Android의 OS나 여타 단말기 종류에도 제한을 받지 않는 방식으로 디버깅 작업이 가능합니다.
categories: coding
# heroImage: '/blog-placeholder-2.jpg'
---

메모차원의 포스팅입니다.

모바일쪽 웹페이지를 조금 만지작거리면서 불편한 것이 PC처럼 브라우저를 통해 디버깅을 하기가 수월하지 않다는 점입니다.

(맥을 사용하는 관계로...)맥 + 아이폰 + Safari의 경우는 맥과 케이블을 연결하여 맥용 Safari의 디버깅 툴을 통해 가능하지만...맥 + 아이폰 + Chrome의 경우는 전혀 어떻게 해볼 방법이 없습니다. Chrome을 통해서 어느정도는 가능하지만, 실제 단말기가 아닌이상 제대로 된 동작확인은 하기가 힘든 현실입니다. 안드로이드도 마찬가지고..

결국, 예전부터 언젠가는 한번 사용해 봐야지 했었던 [weinre](http://people.apache.org/~pmuellr/weinre/docs/latest/Home.html)를 사용하여 작업해 보게 되었습니다. 결론적으로는 덕분에 풀리지 않던 문제도 한가지 풀었고 상당히 마음에 드는 툴입니다.

## Install node.js

![Node.js](https://farm2.staticflickr.com/1569/23716551309_fdbef00302_o.png)

weinre는 우선 [node.js](https://nodejs.org/en/)가 인스톨되어 있어야 하니까 terminal을 열고 npm을 인스톨합니다.

```
sudo npm install -g n
```

stable로 안정판을 인스톨 하거나, 최신판을 사용하기 위해서는 latest를 사용합니다.

```
sudo npm stable
```

최종적으로 버전확인을 해보죠.

```
node -v
```

<blockquote>
이미 인스톨 되어 있다면 혹시 모르니 버전확인과 업데이트를 하시길 권장합니다.
캐쉬를 먼저 삭제해준후...
`sudo npm cache clean -f`

npm을 업데이트 시켜줍니다.
`sudo npm update -g npm`
`sudo npm update -g`만을 사용하게 되면 전체 Global packages를 업데이트 시키게 됩니다.

</blockquote>

## Install weinre

![weinre](https://farm6.staticflickr.com/5638/24001504511_110a052815_m.jpg)

기본 바탕을 준비했으니 weinre를 인스톨해줍니다.

```
sudo npm -g install weinre
```

네. 이걸로 끝입니다.

## Running weinre

```
weinre --boundHost 192.168.0.x
```

기본적으로 터미널 창에서 `weinre`만 치시면 `localhost:8080`으로 실행이 되지만, 상기와 같이 boundHost옵션을 사용하여 자신의 localhost의 IP주소를 설정해 줍니다. <mark>weinre는 기본적으로 localhost로만 접속이 가능한 관계로 boundHost를 사용하여 현재 할당되어 있는 IP주소를 지정해준후, 다른 디바이스에서 접속가능한 상태를 만들어줄 필요가 있습니다.</mark>

<blockquote>
만약 자신의 IP주소를 모르겠다면, terminal창에서
`ifconfig`를 사용하여 IP주소를 확인합니다. ifconfig은 PC의 ipconfig와 같은 기능입니다.
</blockquote>

weinre만 실행한 결과

![minamiland — node /usr/local/bin/weinre — 80×24](https://farm6.staticflickr.com/5622/24058677316_7e3ff61d91_o.png)

```
weinre: starting server at http://localhost:8080
```

boundHost를 사용하여 실행한 결과(유동IP를 사용중이어서 포스팅 시점에 저의 IP주소는 192.168.200.167입니다.)

![minamiland — node /usr/local/bin/weinre --boundHost 192.168.200.167 — 80×24](https://farm2.staticflickr.com/1454/23976635752_de362f6673_o.png)

```
weinre: starting server at http://192.168.200.167:8080
```

이제 서버가 제대로 사용가능한지 확인하기 위하여 브라우저를 실행후, 지정된 `http://192.168.0.x:8080`으로 접속하면 아래와 같은 화면을 확인하실수 있게 됩니다.

![weinre server home](https://farm6.staticflickr.com/5805/23458062203_a17a3e2024_z.jpg)

## weinre 디버깅 준비 - PC

페이지상의 Target Script에서 보여지는 script를 복사하여 디버깅 작업이 필요한 페이지에 붙여둡니다.
<mark>이번 테스트를 진행하면서 확인한 결과, 이작업은 패스해도 상관없었습니다.</mark>

![weinre - target script](https://farm2.staticflickr.com/1566/24002388371_643dff19d8_o.png)

## weinre 디버깅 준비 - Mobile

PC쪽 작업이 완료되었으면 이제 모바일쪽에서 필요한 설정을 할 차례입니다.
모바일브라우저를 띄우고 weinre서버에 접속합니다.

---

![weomre-mobile-01](https://farm6.staticflickr.com/5739/23466086984_d9e278fe5c_n.jpg)
`http://192.168.200.167:8080`에 접속하여 Target Bookmarklet의 textarea영역에 있는 js소스를 복사합니다.

---

![weomre-mobile-02](https://farm2.staticflickr.com/1697/24011730651_e687f96e5f_n.jpg)
아무페이지나 북마크를 한후에 편집모드에 들어가서 복사해둔 js를 url영역에 붙여두고 저장합니다.

이로서 모든 준비작업은 완료가 된것 같습니다.

## weinre 디버깅

이제 모든 준비가 끝났으니 실제 디버깅작업을 시작해 보겠습니다.

---

PC측 브라우저의 <mark>Access Points의 <b>debug client user interface</b>를 통해 디버깅화면에 접속</mark>할 수 있습니다.

![weinre - access points](https://farm2.staticflickr.com/1504/23789316450_4bd9be45a3_o.png)

---

현재 접속된 상태에서는 디버깅 대상이 접속하지 않은 상태여서 Target이 none상태입니다.

![weinre: target not connected](https://farm2.staticflickr.com/1565/24012430831_568cf18ce0_o.png)

(\*\*포스팅중에 잠시 시간차를 두었더니 IP가 192.168.200.104번으로 바뀌었습니다..)

테스트를 위해 네이버에 접속해 봅니다. 디버깅이 필요한 페이지에 접속후 이전 작업에서 저장해 두었던 Bookmarklet을 실행시켜주면...

![weomre-sample01](https://farm6.staticflickr.com/5829/23468414463_7454748178_n.jpg)

단말기에서 접속했다는 것을 확인할 수 있습니다.

![weinre: http://m.naver.com/](https://farm2.staticflickr.com/1599/23987138202_67f8348a0e_o.png)

Elements탭을 클릭하여 소스를 확인후 수정을 해보겠습니다.

![weinre: http://m.naver.com/](https://farm2.staticflickr.com/1497/24069291176_4db9c8ec32_o.png)

'뉴스'를 '경제'로 바꾸면...

![weinre: http://m.naver.com/](https://farm2.staticflickr.com/1545/24012776481_15e82c67e1_o.png)

모바일화면에서 바로 확인 할 수 있게 됩니다.

![weomre-sample02](https://farm2.staticflickr.com/1549/23987103872_0b77be0c1a_n.jpg)

이상입니다.
이제 필요한 부분의 동작을 확인하거나, 콘솔로 로그를 확인하여 제대로 동작하는지 등을 확인하면 PC상의 브라우저로는 동작확인이 제한되는 부분을 실제 단말기에서 문제점을 확인하며 작업을 진행 할 수 있게 됩니다.

우연찮게 새해 첫날 포스팅이 되었습니다.
새해 복 많이 받으세요~~
