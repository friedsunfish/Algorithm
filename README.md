Algorithm

[2진법으로 변환시 1이 가장 많은순으로 정렬(map,match,sort사용)]
```javascript

function solution(A) {
  A = A.sort((a, b) => a - b);
  let B = A.map((x) => x.toString(2));
  let map = {};
  let result = [];
  for (let i = 0; i < A.length; i++) {
    let num = B[i].match(/1/g)?.length;
    map[A[i]] = num;
    result.push([A[i], num]);
  }
  result.sort((a, b) => a[1] - b[1]);
  let answer = result.map((x) => x[0]);
  return answer;
}
console.log(solution([10, 9, 8, 7, 6, 5, 4, 3, 2, 1]));

```
