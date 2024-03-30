# \[해결방안 2] refresh token

## Refresh token 특징&#x20;

* '자동 로그인' 구현에 도움이 됨&#x20;



## Refresh token 순서도&#x20;

```
1. 브라우저에서, login API 로  ID/PW 전달 
2. BE 에서, DB 에 요청 
3. 해당 ID 에 대한 로그인 상태 등을 받아옴
4. BD 에서, 해당 데이터로 token 을 만듦
    - 이 객체를 '암호화' 에 넣어서 -> hash 를 만듦 -> access token (유효시간 1h) (JWT 토큰)
    - 그리고, 이때, refresh token(유효시간 2h) 추가로 생성 
5. 만들어진 access token 을 브라우저로 보냄 
6. 브라우저는 access token 을 '변수(recoil)', refresh token 을 '쿠키' 에 저장 
    - '전역 변수' 에 저장하면, 모든 페이지에서, 일일이 요청할 필요 없음. 
    - '쿠키' 에 저장하면 1) 보안상 유리함 
        - [설정 옵션] http only 설정하면 -> JS 로 쿠키 데이터 못 꺼냄. ex) document.cookie 해도 안 보임 
        - [설정 옵션] secure 옵션 on -> https 에서만 오갈 수 있음. 
        - [쿠키 특징] api 요청시 같이 들어감. 막 꺼내거나 하지 않아도! 
        

7. 브라우저가 인가 api 에 요청할 때, header 에 쿠키를 넣어서 요청 
    - bearer accesstoken 
    
8. BE 에서, 브라우저 에서 보낸 access token 안에 있는 '유효시간' 이 '만료' 되었다고 나옴 

9. BE 에서 브라우저로 'token 만료' 를 리턴함 

10-1 [기존] 에러 메시지를 받으면 -> page 이동 -> 다시 로그인 하게 한다. 
10-2 [refresh token 사용] 
    1) token 만료 여부를 체크 한다. 
    2) 'token 재발급 api'에 'header' 에 refresh token 을 담아서, 다시 요청을 보낸다.
    3) BE 는 해당 refresh token 의 만료기간을 확인함
    4) 기간이 남으면 '암호화' 해서 -> access token(유효시간을)을 다시 만든다.
    5) 다시 access token 을 브라우저에 전달한다. 
    6) 브라우저는, 전역상태에 저장된 access token 만 갈아끼운다. 
    7) 그리고, 실패한 인가를 api 요청을 다시 보낸다. 
    8) BE 에서 인가 성공 
    9) DB 에 데이터 요청 
    10) DB 에서 데이터 회신 
    11) BE 에서 브라우저로 해당 데이터 응답 
      
```





## Refresh token 적용 관련 개념&#x20;

### silent authentication

```
- 위의 과정은 1초도 안 걸림.   
- 하지만, 뒷단에서는, 조금 더 복잡한 작업이 이루어지고 있음. 
- 그래서, 이렇게 사용자 모르게, refresh 토큰으로 다시 인가를 받는 과정을 silent authentication 이라 함
```



### O Auth&#x20;



<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>





&#x20;`출처 : [코드캠프] 프론트엔드 코스_섹션 33_로그인 만료 시간 연장`





