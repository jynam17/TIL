# 옵션
- enabled: false 값이 전달되면 쿼리가 비활성화된다. 데이터 요청에 사용할 파라미터가 유효한 값일 때만 true를 할당하는 식으로 활용할 수 있다. 즉, 자동 실행 여부를 결정하는 옵션이다.


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


# 참고 자료
https://blog.rhostem.com/posts/2021-02-01T00:00:00.000Z
https://velog.io/@familyman80/React-Query-%ED%95%9C%EA%B8%80-%EB%A9%94%EB%89%B4%EC%96%BC
