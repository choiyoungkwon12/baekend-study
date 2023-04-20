# File Upload

- 파일 업로드 시 사용할 수 있는 방식 중 전통적인 방식으로 multipart/form-data 형식을 이용해서 파일을 서버에 보내는 것이다.
  - 그러면 서버에서는 `@ModelAttribute`를 사용해서 파일을 받을 수 있다.
  - `@RequestBody`로도 Multipart form-data에서 파일을 전송할 수는 있지만, MultiPartFile 객체를 사용하지 못하고, 파일을 처리하기 불편함.
    - byte[] 또는 InputStream 를 이용해서 처리해야함. (바이너리 스트림이 포함된 데이터를 처리 못하는듯 함)
  - `@RequestPart`로도 'multipart/form-data' 로 파일 전송을 처리해서 MultipartFile를 사용 가능하다고 함.
    - MultipartFile이 포함되는 경우에 MutliPartResolver가 동작하여 (여기서도 전략 패턴이 사용된다) 역직렬화를 하게 됨. 
    - MultipartFile이 포함되지 않는 경우는 @RequestBody와 같이 HttpMessageConverter가 동작하게 된다.

그럼 `@RequestPart`와 `@ModelAttribute`의 차이점은 무엇일까?
- RequestPart는 HttpMessageConverter에 의해 값이 바인딩 된다.
  - 이 뜻은 objectMapper를 이용해서 json <-> dto 변환을 하는데, NoArgsConstructor를 이용해 객체를 생성하고 getter(게터만 있을 경우 리플렉션을 사용해서) or setter를 통해 private field에 접근함.
- ModelAttribute는 HttpMessageConverter를 사용하는게 아닌 Setter 혹은 적절한 생성자를 이용해서 값을 바인딩한다. ([참고](https://hyeon9mak.github.io/model-attribute-without-setter/))
  - ModelAttributeMethodProcessor 클래스의 constructAttribute 메서드에서 기본생성자가 있으면, setter를 통해 값 바인딩을 시도하고, 그렇지 않을 경우 필드에 맞는 파라미터를 가진 생성자를 찾아 바인딩을 시도한다.

### MockMultipartFile
- 파일 업로드에 대한 테스트를 위한 객체.
  - Mock implementation of the MultipartFile interface. (멀티파트파일의 모의 구현체?)
  - multipart form-data 형식의 컨트롤러를 테스트하기 위해서는 mockMvc의 요청에 multipart를 사용하면 된다.

### 관심사의 분리
- 예제에서 컨트롤러에서 파일 처리를 하는것을 ImageStorage 로 분리하여 컨트롤러는 요청을 받고 응답하는 역할을 하도록 분리함. 
- ImageStorage 에서 파일을 처리하도록 해서 SOILD의 SRP를 최대한 지키려고 함.
  - cloudinary를 듣고, 추가하자면 ImageStorage 를 인터페이스로 만들고, 추상 메서드로 save, download등을 가지게 하고, 로컬에 저장하는 LocalStorage, CloudinaryStorage, S3Storage 등으로 구현체를 만들 수 있을 것 같다.
  - 전략 패턴을 사용해서 OCP를 지키면서 외부의 요청에 따라서, 어디에 저장할지 다르게 구현체를 사용하도록 할 수 있을것 같다.


### Cloudinary
- 이미지, 영상등을 관리할 수 있게 해주는 클라우드 서비스로 기존에 사용해봤던 S3와의 차이점은 url을 변경하면서 특별한 기능들을 간편하게 사용할 수 있다.
  - 블라처리, 이미지 크기조정, 썸네일 만들기 등등
- SDK를 사용해서 cloudinary에 연결하고, 파일을 저장할 수 있음.(코드는 사실 S3와 크게 다르지 않아보임.)

---
그냥 찾아본거) 파일 업로드 하는 방식으로 Base64로 보내는 방법도 있는데, MultipartFile로 보냈을때 성능이 더 좋다고 함.
  - 이유는 MultipartFile 은 파일의 바이너리 형태 그대로 보내는데 Base64 는 바이너리를 -> 문자열로 인코딩 후 보내기 떄문에 사이즈가 더 커질 수 있고, 서버에서 변환하는 작업을 다시 거쳐야 함.
