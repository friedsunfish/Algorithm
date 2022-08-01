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

[각자리수별 숫자 몇번씩 나왔는지 카운팅]
```javascript
function answer(s, e) {
  let result = [];
  for (let i = 0; i < 10; i++) {
    result[i] = 0;
  }
  let num;
  for (let i = s; i <= e; i++) {
    num = i;
    while (num != 0) {
      result[num % 10]++;
      num /= 10;
      num = parseInt(num);
    }
  }
  return result;
}
console.log(answer(100, 101));
```

[고정값인 배열과 입력배열의 요소의차로 배열구성]
```javascript
let arr = [1, 1, 2, 2, 2, 8];
let needChess = [];
function solution(chess) {
  for (let i = 0; i < arr.length; i++) {
    needChess.push(arr[i] - chess[i]);
  }
  return needChess;
}
console.log(solution([0, 1, 1, 5, 3, 6]));
```

[두수를 합쳐서 목표값이 되는 경우의수 찾기]
```javascript
// 첫번째 for문에서 배열길이가 2일경우 break시켜서 중복으로 찾지않게 했는데
// 중복까지 찾을때는 이부분만 제거해서 사용하면 좋을듯하다
function soultion(arr, num) {
  let result = [];
  for (let i = 0; i < arr.length; i++) {
    if (result.length == 2) {
      break;
    }
    for (let j = 0; j < arr.length; j++) {
      if (j == i) {
        continue;
      }
      if (arr[i] + arr[j] == num) {
        result.push(i);
        result.push(j);
        break;
      }
    }
  }
  return result;
}
// console.log(soultion([3, 3], 6));

// 다른풀이
// 애초에 중복을 순회하지않아서 더좋은듯하다..
function soultion2(arr, num) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i] + arr[j] == num) {
        return [i, j];
      }
    }
  }
}
// console.log(soultion2([3, 3], 6));

//다른풀이2 빈객체를 이용한 풀이
function soultion3(arr, num) {
  let map = {};
  for (let i = 0; i < arr.length; i++) {
    if (map[num - arr[i]] != undefined) {
      return [map[num - arr[i]], i];
    }
    map[arr[i]] = i;
  }
}
console.log(soultion3([3, 2, 4], 6));

// i=0 -> map[3] = 0;
// i=1 -> map[2] = 1;
// i=2 -> map[2] != undefined; return map[2],2
```

[정답시 점수1획득, 연속득점시 추가점수 1씩증가]
```javascript
function solution(arr) {
  let plus = 1;
  let result = 0;
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === 1) {
      result += plus;
      plus++;
    } else if (arr[i] === 0) {
      plus = 1;
    }
  }
  return result;
}
console.log(solution([1, 1, 1, 1, 1, 0, 0, 1, 1, 0]));

// 다른풀이

function answer(mark) {
  let result = 0;
  let score = 0;
  for (let i = 0; mark.length; i++) {
    if (mark[i] == 1) {
      result += ++score;
    } else {
      score = 0;
    }
  }
}
```
[배열 정렬후 최소,최대찾기]
```javascript
function solution(arr) {
  let arr2 = [...arr];
  let result = [];
  arr2 = arr2.sort(function (x, y) {
    return x - y;
  });
  result.push(arr2[arr2.length - 1], arr2[arr2.length - 2]);
  return result;
}
console.log(solution([-15, -4, -8, 12, 12, -8, -8, 9, 10, 15, -2, 10, -14, 2, 13, 19, -9, 3, -18, 14]));
```

[배열 최소값위치 모두찾기]
```javascript
function solution(arr) {
  let result = [];
  // 최소값 구하기
  let min = Number.MAX_SAFE_INTEGER;
  arr.forEach(function (i) {
    if (i < min) {
      min = i;
    }
  });
  // 최소값의 첫번째 index 찾고 찾은 index값이후로 찾기
  let fromIndex = arr.indexOf(min);
  while (fromIndex != -1) {
    result.push(fromIndex);
    // Array.indexOf(찾을값,찾을위치);
    fromIndex = arr.indexOf(min, fromIndex + 1);
  }
  return result;
}
console.log(solution([1, 1, 1, 1, 1]));
```

[벽돌옮기기 더많이 쌓여있는 블록의개수]
```javascript
function solution(arr) {
  let sum = arr.reduce(sumReducer);
  let standard = sum / arr.length;
  let over = arr.filter((element) => element > standard);
  let result = over.map((x) => x - standard);
  return result.reduce(sumReducer);
}
console.log(solution([27, 14, 19, 11, 26, 25, 23, 15]));

function sumReducer(accumulator, currentNumber) {
  return accumulator + currentNumber;
}

// reduce 사용법
// 1. let sum = arr.reduce((accumulator,currentNumber) => accumulator+currentNumber);
// 2. function sumReducer(accumulator,currentNumber) {
//      return accumulator + currentNumber;
//    }
// sum2 = arr.reduce(sumReducer);
```

[별나무만들기]
```javascript
let input = 7;
let star = 1;
let space = 1 + (input - 1) * 2;
for (let floor = 1; floor <= input; floor++) {
  let num = (space - star) / 2;
  let empty_space = " ".repeat(num);
  console.log(empty_space, "*".repeat(star), empty_space);
  star += 2;
}
```

[map이용 배열 생성/ 지정된 숫자부터 배열생성]
```javascript
function solution(s, e) {
  let result = [];
  let arr = [...Array(e - s + 1)].map((v, i) => i + s);
}
console.log(solution(100, 101));

// n에서 n2까지 배열만들기
// function solution(s, e) {
//   let result = [];
//   let arr = [...Array(e - s + 1)].map((v, i) => i + s);
// }
// console.log(solution(100, 101));

// let result = [0, 1];
// let arr = [...Array(e - s + 1)].map((v, i) => i + s);
// (v,i)부분 왜들어가는지 실험해봤는데 이미 만들어져있는 배열을 끌어다쓸때는 밑에처럼 v를 쓰지않아도 되는데
// (map이 기본적으로 return하는값이 v여서 v인거같다) 만드는 과정에서 바로 생성할때는 앞에계산된 value를 v로 가져와서 계산해야되서
// (v,i로 쓰는거같다)
// let arr2 = result.map((i) => i + s);
```

```javascript

```

```javascript

```

```javascript

```

```javascript

```

```javascript

```

