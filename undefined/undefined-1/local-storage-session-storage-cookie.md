# 브라우저 저장소 간 차이 (local storage, session storage, cookie)



## 공통점&#x20;

```
- 모두 '객체' 형태로 존재한다.
```





## local storage

```
- '브라우저 on/off' 해도 -> '유지' 된다. 

```





## session storage&#x20;

```
- '브라우저 on/off' 하면 -> '사라진다.' 
```





## cooki

## cookie

```
- '브라우저 on/off' 하면 -> '사라진다.' ❓❓❓ 

- '브라우저와 backend' 간 '소통' 하여, data 를 주고 받기 위한 것 임. 

- 특징 
    1. 프론트에서req.header.cookie 에 담아서 보내면, 그 전에 보냈던 것들도 모두 담겨 있음. 
    2. 백엔드에서 cookie 에 담아, 응답하면, 2차 가공(axios 로 비동기로 꺼내서 -> state 담는 과정) 없이! 
        ->  바로, cookie 에 저장되어서 -> 데이터 꺼내 쓸 수 있음. 
        
- 필드 의미 
    - secure : https 일 때 만 백엔드와 데이터를 주고 받겠다. 
    - httpOnly true
        - document.cookie 찍으면, 쿠키가 보여야 함. 
        - 만약, true 설정하면, js 로 접근 불가. 즉, document.coookie 해도 안 보임. 
        
- 사용법 
    - 그러면, access token 을 쿠키에 담아서 줄 수도 있음 ( 하지 불확실  📛📛) 

```





## 추가 공부&#x20;

```
1. access token 을 쿠키에 담아서, 서버에서 응답하는 건, 불확실 
```

