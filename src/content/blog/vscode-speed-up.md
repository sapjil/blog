---
title: disable-hardware-acceleration로 VSCODE가 버벅거릴때 해결법
pubDate: 2024-05-19
tags: ["blog", "VSCODE", "속도개선", "버벅거림 해결"]
description: VSCODE 작업 중, 반응속도가 느려서 울화통이 터질뻔...
categories: vscode
---

## 이런 문제는 왜 생기는지 근본적인 원인은 모르겠지만..

최근들어 VSCODE가 무척 반응이 느려졌다. 이런저런 방법을 동원해도 잘 해결되지 않고 있었고 CPU를 많이 잡아먹고 있는 것 같았다. 방법을 찾다 보니 `"disable-hardware-acceleration": true`를 설정하면 좋아진다고 해서 적용시켰다.
실질적으로는 조금 좋아진것 같기도 하고 아닌것 같기도 하고 애매함.

- Ctrl+Shift+P로 커맨드 팔레트 기동
- `Configure Runtime Arguments`를 입력 하여 `argv.json` 편집
- `"disable-hardware-acceleration": true`를 기입
- VS Code 재기동

참고: https://stackoverflow.com/questions/37334148/launch-vs-code-with-disable-gpu-flag-by-default

잘 동작하다가 꼭 내가 모르는 어떤 설정을 건드려서 생기는 문제가 있는 것 같다. 잘 사용하지 않는 확장팩은 다 삭제.
이유를 전혀 모르니 더 문제다.
