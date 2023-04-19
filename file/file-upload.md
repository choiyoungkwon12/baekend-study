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



