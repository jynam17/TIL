# 옵션
- enabled: false 값이 전달되면 쿼리가 비활성화된다. 데이터 요청에 사용할 파라미터가 유효한 값일 때만 true를 할당하는 식으로 활용할 수 있다. 즉, 자동 실행 여부를 결정하는 옵션이다.
- refetchOnWindowFocus: input을 포커스하거나 다른 창을 보다가 돌아오는 등 포커스가 바뀌면 refetch가 될지 말지 여부에 대한 옵션이며 기본 값은 true이다. 왜냐하면 리액트 쿼리가 데이터가 stale한지 판단하는 기준 중에 하나가 포커스이기 때문이다. 포커스가 달라지면 stale 상태라고 판단한다.


# 쿼리 키
### 배열 키
다음 쿼리는 객체 내의 키 순서와 관계 없이 모두 동일한 것으로 간주된다.
```ts
useQuery(['todos', { status, page }], ...)
useQuery(['todos', { page, status }], ...)
useQuery(['todos', { page, status, other: undefined }], ...)
 ```
그러나 다음 쿼리 키는 같지 않다. 배열 항목 순서가 중요하다.
```
useQuery ( [ '할 일' , 상태 , 페이지 ] , ... ) 
useQuery ( [ '할 일' , 페이지 , 상태 ] , ... ) 
useQuery ( [ 'todos' , undefined , page , status ] , ... )
```
쿼리 기능이 변수에 의존하는 경우 쿼리 키에 포함한다.
```ts
function Todos({ todoId }) {
   const result = useQuery(['todos', todoId], () => fetchTodoById(todoId))
 }
 ```
 
# useMutation
## Option
useMutation의 옵션은 두 가지 방법으로 설정할 수 있다. <br />
첫 번째는 선언 시 두 번째 인자에 설정하는 것, 두 번째는 mutate 함수 사용 시 두 번째 인자에 설정하는 것이다.

그런데 만약 둘 다 설정되어 있다면 어떻게 될까?

이는 onSuccess로 실험해보니 선언부에 있는 것만 실행이 됐다.

# useInfiniteQuery
[잘 정리된 자료](https://jforj.tistory.com/246)

# 쿼리 선언부 모아서 따로 파일로 관리하기
![image](https://user-images.githubusercontent.com/73823388/173514107-457330aa-2271-4cc4-8626-3f55a10e6211.png)
너소서 초반 리액트 쿼리 도입 시기에 이걸 제안했었는데 굳이 해야하나? 싶은 의견이 다수여서 (나도 얘기하다 보니 동의했고) 안했었다.

그런데 지금은 완전 후회 중이다.
<br />
한 쿼리를 한 파일에서만 사용하는게 아니라 여기저기서 invalidateQueries 또는 setQueryData를 해줘야 하는데 선언부를 찾아다니기가 너무 힘들고 헷갈린다.
<br />
또한 같은 쿼리를 여러 파일에서 써야 하는 경우도 있다.

초반에는 이런 점들까지 생각하고 제안했던건 아니어서.....
<br />
지금이라도 바꾸고 싶은데 너무 대공사다ㅠ 다음 리액트 쿼리 쓰는 프로젝트에서는 꼭 저렇게 해야지..


# 참고 자료
https://blog.rhostem.com/posts/2021-02-01T00:00:00.000Z
https://velog.io/@familyman80/React-Query-%ED%95%9C%EA%B8%80-%EB%A9%94%EB%89%B4%EC%96%BC
