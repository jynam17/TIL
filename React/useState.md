# 지연 초기 state
하는 이유: 컴포넌트 함수를 실행시킬 때마다 useState(머시기)에서 머시기로 새로 초기화 시켜주진 않겠지만 머시기를 읽기는 하기 때문에 머시기가 무거운 작업이라면 쓸데 없이 실행을 하게 되는 것이다.
그런데 이것 때문에 문제를 겪을 수도 있다.
예를 들어 머시기가 Array.sort라고 해보자.
처음에만 sort를 하면 되는데 계속 sort를 해서 의도치 않은 결과를 발생시킬 수 있다.
<img width="947" alt="image" src="https://user-images.githubusercontent.com/73823388/167692342-ae731068-f556-4993-862f-1225dcb0ae7b.png">
