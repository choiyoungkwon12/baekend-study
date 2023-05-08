# CQS
CQRS 전에 CQS 는 Command Query Separation 이라는 뜻으로 커맨드와 쿼리를 분리하는 것이다.

커맨드와 쿼리는 왜 분리하느냐?
- 어떤 행위를 할 때, 크게 나누면 상태를 바꾸는 명령(커맨드)와 상태를 가져오는 질의(쿼리)로 나눌 수 있디.(CUD는 커맨드, R은 쿼리에 해당)
- 만약, 조회만 하는데 해당 객체의 상태가 의도치 않게 변경된다고 하면 문제가 발생할 수 있다.
  - 그래서 사이드 이펙트를 최소화 하도록 분리하는 것이다.(작은 서비스에서는 한눈에 알아보기 쉬워서 문제가 발생하지 않을 수 있지만, 대규모 서비스는 그렇지 않다.)
- 또한, 이런 쿼리와 커맨드를 분리하는것은 순수함수와 함수영 도구를 사용하기 위함 준비과정이라고 생각하면 됨.

# CQRS (Command Query Responsibility Segregation)
- Command 에 해당하는 일은 적절한 도메인 모델, 객체 등을 활용해서 비즈니스의 복잡한 문제를 해결해야 한다.
  - 대부분 이 과정에서 애플리케이션의 상태가 변경된다.
- 사용자에게 보여주기 위해 상태를 조회하는 Query에 해당하는 일은 이미 비즈니스 로직에 대한 처리가 대부분 끝난 상태이고, 자주 사용될 수 있다.(많은 조회)
- 그래서 Command 에 해당하는 모델을 Write Model 로 두고, Qeury 에 해당하는 모델을 Read Model 로 두어 분리한다.  
  - 요청이 들어오면 Write 모델을 이용해서 상태를 업데이트 하고, 조회가 들어오면 조회 전용 모델을 이용해 값을 반환
  - Write 와 Read 를 분리해서 오는 동기화 관련 부분은 Event Sourcing 을 통해 맞춰 줄 수도 있다.

### Materialized View
- 조회를 할때마다 필요한 데이터를 조회하고 가공해서 만들면 성능이 떨어질 수 있기 때문에 읽기 성능을 높이기 위해 사용할 수 있다.
  - 일반 view와 다르게 실제로 DB 에서 값(테이블) 저장되고, 업데이트(동기화) 된다고 함.
  - RDBMS를 잘 알아야 사용할 수 있음.

### OLTP & OLAP
- OLTP(Online Transaction Processing) : 일반적으로 사용하는 애플리케이션의 트랜잭션 처리를 말함.
- OLAP(Online Analytical Processing) : 의사결정을 위해 데이터 분석을 하는것을 OLAP라고 한다고 함.

### Event Sourcing
- 상태의 변화를 이벤트의 연속으로 다루는 방식.(순서가 있음
  - 과거의 이벤트 이력들이 있고, 그게 모여서 현재를 표현할 수 있음.

- 이벤트가 굉장히 많이 쌓인다면, 현재 상태를 조회하는데 분석하거나 하려면 빠르게 이벤트 소싱 만으로는 할 수 없음.
  - 그래서 대부분 CQRS와 같이 사용된다고 함.

- 스프링캠프에서 대규모 시스템 개선 경험기를 들었을때도, 스트랭글러 패턴을 이용해서 Fig Application을 만들어서 개선하는 작업을 할 때도 Read와 Write를 따로 옮겼는데 아마 이미 CQRS가 녹어져 있었던거 같다.

# Redis

- 레디스는 인메모리 기반이고, 여러 자료구조들을 제공한다.
- DB, 캐시, 메시지 브로커와 같은 역할로 사용할 수 있다.

- CQRS 을 적용하면서 사용하는 경우가 많음.
  - 커맨드 요청 시 상태 변경에 대한 내용을 레디스의 dto 로 저장 후 쿼리에서는 읽어가기만 하도록 하는 방식
  - 예를 들어, 장바구니와 같은 형태
