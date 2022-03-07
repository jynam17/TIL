
# (작성 중) React Query와 상태관리 :: 2월 우아한테크세미나

해당 세미나는 우아한형제들 기술 블로그에 배민근님이 올리신 [Store에서 비동기 통신 분리하기 (feat. React Query)](https://techblog.woowahan.com/6339/)라는 글이 유명해져 진행하게 되었다고 한다.
<br /> 따라서 세미나 영상을 본 후 해당 글도 읽어보려고 한다.

## FE 상태관리에 대해
> 본격적인 이야기 전에 기본 지식 잠깐!

### 상태란?
주어진 시간에 대해 시스템을 나타내는 것으로 언제든지 변경될 수 있음. 즉, 문자열, 배열, 객체 등의 형태로 응용 프로그램에 저장된 데이터

=> 개발자 입장에선 관리해야 하는 데이터들

### 모던 웹 프론트엔드 개발
UI/UX의 중요성과 함께 프로덕트 규모가 많이 커지고 FE에서 수행하는 역할이 늘어남 

=> 관리하는 상태가 많아짐

### 상태관리는? (feat. FE)

- 상태를 관리하는 방법에 대한 것 -> 프로덕트가 커짐에 따라 어려움도 커짐
- 상태들은 시간에 따라 변화함
- React에선 단방향 바인딩이므로 Props Drilling 이슈도 존재
- Redux와 MobX 같은 라이브러리를 활용해 해결하기도 함

## 주문 FE 프로덕트를 보며 가진 고민
> 제가 왜 이 'React Query와 상태관리'라는 주제를 가지고 왔을까요?

### 주문 FE 프로덕트
<img width="932" alt="image" src="https://user-images.githubusercontent.com/73823388/156877859-ee3c62e4-254b-4d6c-a33d-d7e3e6a52c43.png">

### 때는 바야흐로 2021년의 여름..

<img width="928" alt="image" src="https://user-images.githubusercontent.com/73823388/156878419-83749a7f-24ea-46f0-b775-a287f1b04139.png">


- 모든 장표들을 다 다른 레포지토리에서 관리하고 있었다. 마이크로서비스 아키텍쳐이긴 하지만 한 팀 내에서 너무 세분화되어 있었다.
- 팀 인원은 3명이었다.

=> 레퍼지토리를 합치고, 레거시 코드를 없애고, 신기술 검토도 하면서 주문 FE 프로덕트를 최신 아키텍처로 통합해보자! 

> '레거시'라고 표현한 이유: React, 우아한js, JQeury 등 프로젝트들이 다양한 아키텍처로 만들어져 있었다.

### 그 중 상태관리에 관한 고민
<img width="1307" alt="image" src="https://user-images.githubusercontent.com/73823388/156878544-edc684c7-4f73-4347-aa0a-31131bcde9cd.png">

- Store는 전역 상태가 저장되고 관리되는 공간인데 상태관리보단 API 통신 코드라는 느낌이 든다.
- Store에 API 통신 로직이 너무 많다. 

### 여기서 다 관리하는게 맞나..?
> 상태관리 영역이 서버값을 저장하는데까지 확장

- API 통신 관련 코드가 모두 Store에
- 반복되는 isFetching, isError 등 API 관련 상태
- 반복되는 비슷한 구조의 API 통신 코드

Redux, MobX, saga 등을 도입할 당시에는 적정 기술이 없었다.

그러나, 과연 현재도 적정 기술인가?

### 서버에서 받아야 하는 상태들의 특성

<img width="752" alt="image" src="https://user-images.githubusercontent.com/73823388/156878990-3edb908a-4586-4e2a-b814-6e620a6b24c4.png">

- 1번 상태들의 오너십이 다른 곳에 있다.
- 3번 ex) 사장님이 사용자가 한 주문 건에 대해 접수를 누른다.

=> Client에서 관리하는 일반적인 상태들과는 특성이 다르다. 즉, 어쩌면 다른 관리 방법이 있다면 좋을지도?

> 🤓 주영: 무작정 남들이 비슷한 용도로 이 기술을 쓴다고 해서 따라 쓰는 것이 아니라 이런 식으로 고민하며 분석을 한 것이 대단한 것 같다.

### 상태를 두 가지로 나누어 봅시다
- Client State
- Server State

<img width="910" alt="image" src="https://user-images.githubusercontent.com/73823388/156883936-d5db0330-bfb5-457e-8a22-cd6440e187ac.png">

## React Query 살펴보기

### React Query 자기소개
<img width="915" alt="image" src="https://user-images.githubusercontent.com/73823388/156895874-37202f48-09d8-437a-8746-f4b5f562c210.png">

- 데이터를 global state를 터치하지 않고 fetch/cache/update 해준다.
