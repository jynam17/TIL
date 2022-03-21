## DP의 조건
- 부분 반복 문제(Overlapping Subproblem)
  - 큰 문제와 작은 문제를 같은 방법으로 풀 수 있어야한다. 그리고 문제를 작은 문제로 나누어서 풀 수 있어야한다.
  - DP는 부분 문제의 결과를 저장하여 재 계산하지 않을 수 있어야 하는데, 해당 부분 문제가 반복적으로 나타나지 않는다면 재사용이 불가능하니 부분 문제가 중복되지 않는 경우에는 사용할 수 없다.
- 최적 부분 구조(Optimal Substructure)
  - 부분 문제의 최적 결과 값을 사용해 전체 문제의 최적 결과를 낼 수 있는 경우


## 참고 자료
https://kimlog.me/algorithm/2016-05-15-dynamic-programing.md/
https://hongjw1938.tistory.com/47
