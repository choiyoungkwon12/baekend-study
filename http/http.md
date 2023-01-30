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
    - Get 요청 전에
- POST
    - 생성 요청 시 사용됨. 기본적으로 Submit 하면 Post 사용 가능하나, Collection Pattern에서 Create로 사용하며 실제로 대부분 따르고 있음.
- PUT
- POST
- DELETE
- OPTIONS




### HTTP Status Code(응답)
