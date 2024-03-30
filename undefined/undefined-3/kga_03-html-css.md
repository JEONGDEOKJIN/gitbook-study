---
cover: >-
  https://images.unsplash.com/photo-1585064210818-8b7af20d03b4?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw1fHxjaGFuZ2V8ZW58MHx8fHwxNzExMjY3NTgwfDA&ixlib=rb-4.0.3&q=85
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# 3. 새로고침 시 access token 유실에 따른, 로그인 풀리는 현상

## 문제 상황&#x20;

```
다 된줄 알았으나... 새로고침을 하게 되면 로그인이 풀린다... 
정확히 '모든 인가 api' 의 정보가 초기화 된다.
```



왜 인가 api 데이터가 사라지게 되는거지?&#x20;

그리고, 어떻게 해결해야 하는건가?







* 브라우저, 프론트엔드 그리고 백엔드의 관계

```bash
1. 브라우저는 프론트에 요청함 
2. 프론트 서버는 html, css, js 를 브라우저에게 전달함 (아마도, SSR 기준?) 
3. 브라우저는 렌더링 함 
```



```javascript
- 새로고침을 한다는 건, 해당 페이지에 대해서 새롭게 'enter' 를 치는 것과 같음 
- enter 를 치면 -> 브라우저는 프론트 서버에게 '새로운 요청' 을 하게 됨
- 프론트 서버는, 브라우저에게, '완전히 깨끗한' js, html, css 를 전달함 
- recoil, const, let 같은 경우, 모두, 'heap? 메모리?' 에 저장하고 있었음. 
- 따라서, '새로고침 시 완전히 깨끗' 해지는 js의 특징을 피해갈 수 없었음. 
- 따라서, access token 을 저장하고 있는 recoil 의 data 가 모두 사라지고 
- access token 이 없으니, 인가 api 인 userFetch 도 못 하게 되는 것 임. 

```







