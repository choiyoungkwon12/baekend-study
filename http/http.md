# HTTP

- http란 hypertext transfer protocol로 웹상에서 데이서 전송을 위한 하이퍼텍스트 형식의 응용계층의 프로토콜(규약)이다.

응용 계층은 OSI 7계층 중 하나
- 2계층 - 데이터 링크 계층으로 기계에 할당된 mac address 와 관련된 계층
- 3계층 - 네트워크 계층 : IP address와 관련된 계층
- 4계층 - 전송 계층 : TCP, UDP 를 이용하여 데이터를 전송하는 계층
- 7계층 - 응용 계층 : HTTP : 응용 서비스와 관련된 계층

### 서버/클라이언트 모델

http의 동작은 서버/클라이언트 모델을 따름.
- 클라이언트 : 요청을 보내는 곳
- 서버는 작업을 처리해서 응답 하는곳을 말함.

클라이언트와 서버간의 요청-응답 사이에서 메시지를 통해 작업에 대한 요청/결과를 나타냄.
- 리소스(URL)를 통해 자원을 나타내고 원하는 결과를 요청 


### 무상태 

HTTP 통신은 기본적으로 무상태(stateless)이다.

- 그래서 클라이언트가 요청을 보낼때 본인이 누군지 알려주어야 상태를 가질 수 있게된다.
  - 이 때 사용하는 것이 쿠키, 세션, localStorage등을 사용함.

### HTTP 메시지
- 기본적으로 사람이 읽을 수 있는태형태
```
------ 요청(reqeust) 구조 ------
POST / HTTP/1.1                     <- Start-line
HOST: localhost:8080                <- headers
...

                                    <- empty line
-123456                             <- body

------  응답(response) 구조 ------  
HTTP/1.1 403 Forbidden              <- Start-line
Server: nginx                       <- headers
...

                                    <- empty line
{"num":-123456}                     <- body

```
http 메시지 요청과 응답의 값은 다르지만 전체적인 기본 구조는 같음.
- start-line, headers, empty line, body로 이루어져 있음.
- body
    - body는 크기를 알기 어렵기 때문에 content-length를 아용한다.
    - 사람이 읽지 못하는 형태일 수도 있음(ex. 이미지를 위한 바이너리)
    - 하나가 아니라 여러개일수 있다.

### HTTP Method (요청)
- GET
    - 조회 시 사용하며 멱등성을 가짐
- HEAD
    - Get 요청과 같지만, 응답 본문을 포함하지 않음.
- POST
    - 생성 요청 시 사용됨. 기본적으로 Submit 하면 Post 사용 가능하나, Collection Pattern에서 Create로 사용하며 실제로 대부분 따르고 있음.
    - 항상 같은 생성을 하면 계속 생성이 되거나 오류가 나거나 다르기 때문에 멱등하지 않을 수 밖에 없음.
- PUT
    - 데이터를 전체를 바꾸는(update) 역할을 하는 Http method (Overwrite하는 성격)
    - 전체 리소스를 그대로 대체하기 때문에 멱등함
- PATCH
    - update하는것으로 put과 비슷하지만, 부분적으로 변경한다는 개념에서 차이가 있음.
    - 단순히 일부 리소스를 교체하는 것은 멱등할 수 있지만, api 한번 보낼때마다 회원의 나이를 증가 시기는 것과 같이 매번 다른 값을 올수도 있기 떄문에 멱등하지 않음.
    - 코드를 짤때는 put과 patch가 비슷하게 되겠지만, 스펙상으로는 가능하다고 함.
- DELETE
    - 말 그대로 리소스를 삭제 할 때 사용
- OPTIONS
    - 여러 지원에 대한 확인을 할 수 있음(Put 가능한지, Delete 가능한지와 같은것들)




### HTTP Status Code(응답)
- 1xx : 정보 응답
- 2xx : 성공 응답
- 3xx : 리다이렉션 메시지
- 4xx : 클라이언트 에러 응답
- 5xx : 서버 에러 응답 


참고 : 
- https://developer.mozilla.org/ko/docs/Web/HTTP
