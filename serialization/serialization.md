# Serialization(직렬화)

- 객체를 DB에 저장하거나 네트워크로 전송하는 건 불가능함.
  - 그래서, 객체를 복구할 수 있도록 데이터화 할 수 있어야함.
  - 바이터리라면 바이트 스트림, 텍스트면 기계가 파싱 할 수 있고, 사람도 읽을 수 있는 JSON, XML형태가 있음.

직렬화와 마샬링은 거의 같지만, Java에서는 마샬링을 특수하게 다룬다고 함.
- 직렬화(Serialization): 역직렬화(Deserialization)를 통해 객체 또는 데이터의 복사본을 만들 수 있음.
- 마샬링(Marshalling): 직렬화와 같거나, 원격 객체로 복원할 수 있음. 원격 객체의 경우 메서드 호출은 RPC(또는 RMI)가 됨.
  - 마샬링이 좀 더 넓은 의미이고, 원격 객체를 얻는 것은 약간 리모콘에 비유해볼수있다?

## JSON (JavaScript Object Notation)

- JavaScript Good Parts로 유명한 Douglas Crockford가 만든 `데이터 포맷`.

- JavaScript의 object는 기본적으로 key-value 쌍이다(심지어 Array도 제한된 key-value + length 관리에 불과함). Java는 Map이 이와 유사하지만, 스키마 관리 및 타입 안전성을 위해 DTO를 활용한다.
  - Map으로 사용하게 되면 Map에 어떤게 있는지 확인하기 어렵고, key는 String이지만, value는 Object와 같은 형태로 사용될 수 있기 떄문에 타입 안전성 측면에서 DTO를 활용하는 것이 더 좋다.


- java에서의 json 생성: DTO(자바 객체) → 변환기 → JSON 문자열
- java에서의 json 해석: JSON 문자열 → 변환기 → DTO(자바 객체)

자바에서는 Jackson 이라는 라이브러리를 사용하면 편리하게 json <-> dto 변환을 할 수 있다.

### JSON 스키마로서의 DTO
- DTO는 여러 곳에서 사용될 수 있고, 그 의미는 계속 확대됨. 
- 예를 들어 Tier, 즉 Remote 통신이 아닌 상황인 Layer 사이나 내부 객체를 감춘 공개 인터페이스를 만들 때도 DTO를 활용. 
- “데이터 전송”이기만 하면 사실 딱히 틀리지 않다.

- 우리가 여기서 쓰는 건 JSON 스키마로서의 DTO. 
- 이게 DTO의 전부라고 생각하지 말고, DTO를 쓰는 다양한 상황을 상상해 보자. 
- 이는 “DTO 변환을 어디에서 해야 하나요?” 같은 질문과 연결된다.
