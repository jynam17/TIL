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

# useInfiniteQuery
[잘 정리된 자료](https://jforj.tistory.com/246)



# 참고 자료
https://blog.rhostem.com/posts/2021-02-01T00:00:00.000Z
https://velog.io/@familyman80/React-Query-%ED%95%9C%EA%B8%80-%EB%A9%94%EB%89%B4%EC%96%BC
