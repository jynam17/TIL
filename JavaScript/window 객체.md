(대충 메모 주의..)

모든 객체의 조상은 Object인줄 알았는데 알고보니 window가 모든 객체의 조상이다.

Object도 window 객체의 자식이다.

그런데 프로토타입 체인은 Object에서 끊긴다. 흠

<img width="795" alt="image" src="https://user-images.githubusercontent.com/73823388/165303848-94c1370f-40e7-4060-bc90-e2da9c75d495.png">

출처 - https://www.zerocho.com/category/JavaScript/post/573b321aa54b5e8427432946

window가 전역 객체이기 때문에

kakao map api를 script 태그로 로드하면 kakao 객체가 window 객체에 등록되는데 이를 window.kakao 이렇게 하지 않고 그냥 kakao 이렇게 사용 가능한 것이다.
