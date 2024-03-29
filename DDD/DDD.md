# DDD(Domain Driven Design)
- 2004년 Eric Evans가 사람들이 Blue Book이라고 부르는 DDD 책을 냄.
  - 해당 책에서의 내용은 소프트웨어는 복잡하기 때문에 잘 관리하지 못한다면 유지보수하기 힘든 레거시 시스템이 된다.
  - 소프트웨어의 복잡성은 현실에서 프로그래밍으로 해결 해야 할 도메인이(현실에서의 문제) 복잡하기 때문이다.
  - 먼저 복잡한 기술 영역과 도메인 영역을 분리하고, 도메인을 적적히 다루기 위한 모델을 가지고 복잡성을 관리하도록 한다.
  - 이렇게, 복잡한 현실의 문제를 잘 관리할 수 있게 하는 사고방식, 도구의 모음이 도메인 주도 설계이고, 에릭 에반스의 책도 여러 패턴을 소개하는 형태로 쓰여져 있다.

**DDD의 전제**
```
1. 대부분의 소프트웨어는 도메인과 도메인 로직에 집중해야 한다.
2. 복잡한 도메인 설계는 모델을 기반으로 해야한다.
```
DDD를 Microservices를 위한 수단 정도로 여기고 학습하는 경우가 있는데, 이런 접근 보다는 "비즈니스를 어떻게 더 잘 이해하고, 이를 설계와 코드에 녹여내고, 비즈니스 도메인에 대한 이해가 심화될 때마다 설계와 코드에 반영할 수 있을까?라고 생각해야함.

## 기술 부채(Technical Debt)

많은 사람들이 기술부채를 코드를 엉망으로 작성하는것으로 생각하는데 그게 아니라, 소프트웨어를 출시하면 많은것들을 배우게 되는데 대부분은 배우게 된 것들을 다시 설계와 코드에 반영하지 않는다. 
=> 이를 갚은 생각 없이 돈을 빌리는 것과 같은 일이다.

무언가 배웠으면 갚아야한다. 이해가 설계와 코드에 반영되지 않으면, 이해하기 어려운 복잡한 설계와 코드앞에 좌절하고, 작업한느데 더 오래걸리게 되는데 이게 기술부채가 되는것이다.

그래서 모델을 적절히 만들고, 이해를 설계와 코드에 반영 해야 기술부채를 다루기 쉬워진다.

### 모델(Model)

- 모델은 현실을 해석하고 추상화함으러써 단순화한것이다.
- 비즈니스 도메인에서 중요한 본질만 남기고 나머지를 제거한것이라고 말할 수도 있다.
  - 극단적인 예) 지하철 노선도
- 하지만 비즈니스 도메인을 잘 모르는 경우가 많고, 본질이 무엇인지, 어떻게 추상화 해야하는지 잘 모르는 경우가 많다.
  - 그래서 많은 경우 자신이 아는 적당하게 시작하고 주먹구구식으로 설계와 코드가 확장하면서 고통을 겪에 된다. => 기술부채
- 그래서 도메인 전문가와 대화하면서 모델을 발명하고 만들고 나서 대화하거나 설계하거나, 코드를 작성할때 많이 사용하면 도메인에 대한 이해가 점점 깊어지게 된다.
  - 이 경우 더 나은 설계, 모델,에 대한 통찰을 얻게 되고 이 경우에도 이해도가 높아짐에 따른 기술부채가 생겼다고도 말한다(좋은 의미에서의 기술부채) 

=> 기술부채가 처음부터 많이 생기는것을 방지하고, 좋은 의미의 기술부채가 생기게함으로써 다루기 좋은 상태의 소프트웨어로 발전 시키는데 DDD라는 것을 사용할 수 있다.

## Strategic Design (전략적 설계)

- 도메인 주도 설계는 크게 전략적 설계와 전술적 설계로 나눌 수 있고, 비즈니스 성공을 위해서는 전략적 설계가 중요하고, 전술적 설계의 선행 조건이 되기도 한다.

전략적 설계는 다음과 같은 패턴을 다룸.
```
1. Ubiquitous Language (보편 언어, 유비쿼터스 언어) 
2. Bounded Context (제한된 컨텍스트)
3. Subdomain (서브 도메인)
```

### Ubiquitous Language (보편 언어, 유비쿼터스 언어)
- DDD에서의 시작이자 끝이라고 할 정도로 굉장히 중요한 것이라고 함.
- 어떤 소프트웨어를 만드는데 참여하는 모두가 하나의 언아(어휘 모음)을 사용한다.
  - 도메인 전문가, 비즈니스 분석가, 소프트웨어 설계자, 프로그래머 등은 모두 같은 언어를 사용하도록 함.
- 주의할 점은 도메인 전문가가 사용하는 언어를 따라가는게 아니라, 비즈니스 도메인을 다룰 수 있는 용어를 함께 만들어서 코드를 작성할떄에도 사용해야한다는 것임.
  - 설계하기 어렵거나, 코딩하기 어려운 어휘 체계 등은 재검토하여 새로운 어휘를 만들거나 조율이 필요하다 있다는 증거이기도 하다.
- 하나의 언어를 사용하고, 계속 논의함으로 도메인에서의 이해도를 점점 늘리고 더 발전하고 똑똑해져서 긍정적인 기술 부채를 쌓고, 갚으며 선순환이 되는 것이 이상적일 것 같다.

### Bounded Context (제한된 컨텍스트)
- 커다란 시스템을 만든다면, 하나의 어휘가 다양한 의미로 쓰일 수 있다. 
  - 예) Account는 어떤 경우에는 사용자의 계정, 어떤 경우에는 은행의 통장을 의미함.
  - 하지만, UserAccount, BankAccount 등으로 나누어 쓰기 시작하면 접두어, 접미어가 넘쳐나는 상황이 발생 할 수 있다. => 대화의 비용이 증가함.

- 맥락을 좁힘으로써 하나의 어휘가 하나의 대상을 지시하는 이상적인 상황을 만들게 된다.
  - 예로, 은행 관련된 업무를 하는중에 말하는 Account는 계좌를 의미한다. 
  - 보통 여러 맥락을 뒤섞어서 이야기하거나 작업하는 경우는 드물다.
- 따라서, 우리는 하나의 시스템을 잘 조직화된 Bounded Context로 나누고, 보편언어를 잘 만들고 유지할 수 있을것이다.
  - 두가지가 만나는 지점이 분명 있을 수 있지만, 최소한으로 만들고 각 컨테스트마다 경계를 잘 나누고, 하나의 컨텍스트 안에서는 통일된 유비쿼터스 언어를 사용할 수 있게 해야한다.

보편 언어를 잘 사용하기 위해서 바운디드 컨텍스트를 사용하는것임.
- 사실상 바운디드 컨텍스트는 보편 언어를 위해서 존재함.
- 보통 같은 유비쿼터스 언어를 가진 사람들이 하나의 바운디드 컨텍스트 내에서 일 하는 경우가 많다.(하나의 팀을 만드는 데 쓰이기도 하며, 작게 만들어지는 경우 마이크로 서비스로 되기도 한다.)

### Subdomain (서브 도메인)
- 시스템을 나누는데 Bounded Context를 사용하고, 도메인을 나눌 땐 서브도메인이라는 단어를 사용한다.
- 하는일 : 비즈니스 도메인 => 그 안에서 더 세분화된 도메인을 서브 도메인이라고 함.
- Bounded Context와 서브도메인은 큰 차이가 없을 수 있지만, Bounded Context는 소프트웨어를 조직화 하는 방법이며, 그 때 모델링을 하고 유비쿼터스 언어를 쓰기 위함.
- Bounded Context는 개발하면서 점점 발전 시킬 수 있지만, 서브도메인은 개발하면서 맞춰나가야함.
  - Bounded Context는 Solution Spcce, 서브 도메인은 (Problem Space)라고 함.

## Entity, Value Object

### 전술적 설계 (Tactical Design)

- 전술적 설계가 사실 코드와 맞닿아 있는 부분이 있고, 이것만 다룰 경우 DDD Lite, Model Driven Design 이라고 부르기도 함.(DDD Lite가 사실 긍정적인 의미를 가지지는 않음)
  - 전략적 설계 패턴은 소프트웨어 개발에서 훨씬 중요하고, 거대한 시스템에서는 더 중요하지만, 지금 다룰수 있는 주제는 아니기 떄문에(왜? 도메인 전문가와 이야기를 하며 우리한테 맞는 그 소프트웨어에 맞는 것들을 정하며, 다른 경쟁사와 무엇이 다른가를 다루는 것들이라서 사실 정답이 있는 것은 아님)
  - 그래서 작은 규모의 설꼐 및 코드 작성 문제를 다룰것.

- 전략적 설계, 보편 언어를 통해 도메인 모델을 발견했을 것이라고 가정하고, 이를 설계와 코드에 반영할 수 있다. => 이게 바로 모델 주도 설계(Model Driven Design)이다.
- 도메인 모델은 몇가지로 구분할 수 있는데, 여기서는 대표적인 패턴 몇가지만 다룬다.
  - Entity
  - Value Object
  - Aggregate
  - Repository

### 엔티티 (Entity)
- OOP에서 대부분의 객체는 속성이 아닌, 연속성, 식별성에 따라 정의한다.
  - 엔트맨처럼 키가 바뀌거나 무언가 바뀌어도 앤트맨이 아닌것은 아니고, 속성이 같은 다른세계의 앤트맨이 등장하더라도 구별이 가능하다.
  - 조금 강하게 이야기하면, 식별자(Identifier)가 존재하고, 이를 통해 동일성(Identity)를 확인하면 Entity라고 할 수 있다.
  - 이는 일반적으로 이야기하는 개체(Entity)와 구별되고, 이런 혼란을 막기위해 OOP 또는 DDD라는 Bounded Context 안에서 Entity를 다룸.

### 값 객체 (Value Object, VO)
- 그러나 모든 객체가 연속성, 식별성이 중요한것은 아님.
  - 만원은 그냥 만원일 뿐임. => 쇼핑몰에서의 만원은 모두 같은 의미의 만원을 뜻함
  - 즉, 쇼핌올이라는 비즈니스 도메인을 다루기 위해 적합한 추상화, 모델링이라고 할 수 도 있고, 이를 Value Object 라고함.
- 하지만, 만원이라고 해서 모두 연속성, 식별성이 필요없는것은 아니며, 떄에 따라(ex. 검은돈을 추적하기 위한 일련번호 식별 등..) 만원을 식별해야 하며, 그 경우 일련번호라는 Identifier 를 갖는 Entity가 된다.
  - 죽, 어떤것이 Value Object인지, Entity인지 정해놓고 사용하는 것이 아니라, 비즈니스 도메인에 따라서 달라질 수 있다는게 중요하다.
- Value Object 는 속성을 통해 동등성(Equality)를 판단함.
  - Java 에서는 Value Object 는 해당 객체에 맞게 equals 메서드를 구현해줘야함.
  - 또한, 예측 가능성을 높이고, 혼란을 막기 위해 가능하면 불변객체로 만들어 줘야한다. (ex. final or record)
  

## 집합체 (Aggregate)
- 실제로 사용하게되고, 집중해야 될 것이 Aggregate다.
  - Entity와 Value Object는 도메인 모델, 도메인 객체가 맞지만, 바로 Entity와 Value Object를 사용하지 않을 것이다.
    - ex. 타이어와 엔진을 사용하지 않고, 자동차라는 집합체를 사용하는 것과 같다.

- Aggregate 는 불변식(Invariant)를 유지하고 여러 도메인을 사용하기 좋게 만들어준다.
  - 사방에서 개별 객체에 접근함으로써 불변식(무결성)을 깨뜨리고 일관성을 파괴하는 일이 없도록 지켜주면서 우리가 다뤄야 할 도메인 객체의 갯수를 적절하게 조절해 준다.
    - ex. 도메인 객체가 1000개라면 Aggregate가 도메인을 10개씩 가지고 있다면 Aggregate 100개만 다루면 되고, 가지고 있는 도메인이 더 많다면, 더 적은 Aggregate를 다루면 된다. 
  - 자동차 부품을 모두 직접 접근하는것과 자동차라는 단위로 접근하는 것은 차원이 다른 이야기임.

- 불변식은 우리가 지켜야 할 제약조건, 규칙 이라고 할 수 있음.
  - 에릭 에반스는 주문 예제를 예로 들어 설명하는데, Order는 여러 Line Item을 포함하고, 총 주문액이 10만원이 넘지 않는다는 불변식이 있다고 하자.

```
Order
- LineItem
  - Identifier : item-1
  - Product : mac
  - quantity : 1
  - price : 30000
- LineItem
  - Identifier : item-2
  - Product : book
  - quantity : 1
  - price : 20000
```

만약 개별로 접근이 가능하다고 한다면 item-1에서 봤을때는 현재 5만원이 여유가 있으니, mac 1개를 더 구입해도 된다고 생각할 수 있다.
item-2 관점에서 볼때도 5만원이 여유가 있으니 book 2개를 더 구입해도 된다고 생각할 수 있다.
=> 하지만, 결과적으로 같이 놓고 본다면 item-1 => 6만원, item-2 => 6만원으로 총 10만원으로 불변식이 깨질 수가 있다.

- 그래서 Order라는 Entity를 Order라는 Aggregate의 Root로 삼고, 하나의 객체에 동시에 접근할 수 없는 제약을 통해(일반적으로 트랜젝셩을 통해 달성가능) 불변식을 지킬 수 있음.
  - Aggregate가 하나의 Entity가 되는것처럼 보여짐
  - 이렇게 했을떄, 불변식을 지키는 장점도 있고, `Aggregate가 제공하는 적절한 인터페이스를 통해 더 나은 표현을 할 수도 있다.`

Line Item에 개별적으로 접근하는 경우:

```
LineItem lineItem = lineItemRepository.findById("item-234").get();
lineItem.changeQuantity(2);

LineItem lineItem = lineItemRepository.findById("item-345").get();
lineItem.changeQuantity(3);
```

Aggregate를 사용하는 경우:
```
Order order = orderRepository.findById("order-123").get();
order.changeItemQuantity("item-234", 2);
order.changeItemQuantity("item-345", 3);
```

Aggregate의 동작에 집중한 경우:
```
Order order = orderRepository.findById("order-123").get();
order.addItem("Guitar", 1);
order.addItem("Microphone", 2);
```

- 마지막 코드에서처럼 Aggregate를 통해 OOP에서 말하는 협력하는 객체를 더 잘 구성할 수 있게 된다.
  - 원하는 행동에 대한 의도를 더욱 잘 나타낼 수 있다.
- 책임, 위임, 괌심사의 분리등의 주제를 이를 통해 고민하고 적용할 수 있다.

IDDD 저자인 Vaughn Vernon은 4가지 경험을 제공한다고 함.
- 불변식을 통해 일관성 경계를 찾아서 모델링한다. Aggregate는 트랜잭션적 일관성 경계와 동일하다.
  - 도메인에 대한 이해를 바탕으로 불변식을 통해 모델링을 하고, 도메인이 크게 바뀐다면 불변식도 변경될 수 있음.
- 작은 Aggregate 로 설계한다.
- ID 로 다른 Aggregate 를 참조한다. Jpa 등을 사용하면 관련된 객체를 모두 참조할 수 있지만, 그렇게 하지 않고 경계 안에서만 직접 참조를 하고, 경계 밖에서는 ID를 통해 다른 Aggregate 를 참조하여 접근한다.
- 경계 밖에서 결과적 일관성을 사용한다. 이를 위해 도메인 이벤트 등을 사용할 수 있다.

## Repository

- Repository는 Aggregate를 관리하는 컬렉션처럼 동작한다.
- 이것은 아래와 같은 의미를 갖는데
```
1. 오직 Aggregate만 Repository를 갖는다.
    - ex. order Aggregate를 만들어 경계안에 LineItem을 넣으면 이전에는 직접 접근이 가능하던 LineItem 이라는 엔티티는 접근할 수 없고, Order 라는 Aggregate를 통해서 접근 해야하며, LineItem Repository는 없게된다. 
2. Repository는 영속화 방법 및 기술을 감춘다.
```

- Spring Data Jpa는 이 둘을 만족시키기 위한 기능을 갖추고 있고, Aggregate에 대한 Repository 를 만들어도 안정적으로 작동할 수 있도록 Cascade 옵션을 지원하고, orphanRemoval 과 같은 옵션도 존재한다.
  - 그래서 Persistence Context를 통해 Collection 처럼 사용하는 것이 가능하다.

- Repository는 사실상 전역으로 접근할 수 있어야 하는데, Spring을 사용하면 간단하게 DI를 활용해서 접근 가능하게 된다.
- 따라서, 우리는 적절한 Aggregate를 발견하고, 적절히 책임을 나눌 수 있도록 Entity와 Value Object로 구선(또는 분해)하고, 이를 위한 Repository를 만듦으로써, 여러 기술 문제와 무관한 비즈니스 도메인에 집중할 수 있게 된다.
  - 이렇게 비즈니스 도메인에 집중한 코드를 모아둔 곳을 `Domain Layer`라고 부르며, 
  - Repository와 Aggregate를 사용하는 코드가 모인곳을 `Application Layer`(여기서는 애플리케이션의 기능, Use Case가 직접적으로 드러나게 된다.),
    - Application Layer 안에는 Application Service가 존재함. (Domain Layer 에도 Domain Service가 존재)
    - Application Layer에서는 Aggregate가 제공하는 인터페이스를 사용하도록 하고, 실제 구현된 내용들은 Aggregate에 작성 되어 있도록 함. 
  - Web 등 구체적인 기술로 사용자와 소통하는 코드가 모인 곳을 `UI Layer`라고 부른다.
- Layered Architecture 와 DDD가 함께 다뤄지는 이유이다. Layered Architecture 없이 도메인 모델을 Domain Layer에 분리하는 것은 불가능하다.

---

- 결국, 유지보수하기 쉬운 소프트웨어를 만드는것이 목적이고, 응집도를 높이고, 결합도를 낮추는 것이 최종적인 목표가 되는것 같다.
- 다른 레이어들도 중요하긴 하지만, 대부분은 실제 비즈니스 문제를 해결할 수 있는 도메인 레이어를 더 중요

