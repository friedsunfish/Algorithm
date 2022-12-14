# Algorithm

정렬(Sorting)알고리즘

거품정렬(Bubble Sort) = O(n²) <br>

```javascript
let swap = function (arr, idx_1, idx_2) {
  // idx_1과 idx_2의 자리를 바꾸는 함수
  let tmp = arr[idx_1]; // tmp에 inx_1값 임시저장
  arr[idx_1] = arr[idx_2]; //idx_1을 idx_2로 변경
  arr[idx_2] = tmp; // idx_2를 tmp에저장해놓았던 inx_1값으로 변경
};

let bubbleSort_1 = function (arr) {
  //i와 i+1로 비교하기때문에 arr.length-1값으로 잡는다
  for (let i = 0; i < arr.length - 1; i++) {
    // 〃
    for (let j = 0; j < arr.length - 1; j++) {
      //앞의값이 뒤에값보다 클경우 swap함수실행
      if (arr[j] > arr[j + 1]) {
        swap(arr, j, j + 1);
      }
      console.log(arr);
    }
  }
};

let bubbleSort_2 = function (arr) {
  //i와 i+1로 비교하기때문에 arr.length-1값으로 잡는다
  for (let i = 0; i < arr.length - 1; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      //정렬이 끝난 부분도 계속 확인하는것을 방지하기위해 arr.length-i-1을 한다
      if (arr[j] > arr[j + 1]) {
        swap(arr, j, j + 1);
      }
    }
  }
};

let bubbleSort_3 = function (arr) {
  // 스왑을 했는지안했는지 체크하기위해 변수생성
  let swapped;
  //i와 i+1로 비교하기때문에 arr.length-1값으로 잡는다
  for (let i = 0; i < arr.length - 1; i++) {
    // 기본값을 false로 지정
    swapped = false;
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        swap(arr, j, j + 1);
        // 스왑을 했기때문에 상태값을 true로 변경
        swapped = true;
      }
    }
    // swapped가 false일경우(스왑을 하지않았을경우) 이미정렬되어있는것으로판단하고 반복문종료
    if (!swapped) break;
  }
};

// test code
let init_array = [6, 5, 1, 3, 2, 4];
let array = [...init_array];

bubbleSort_1(array);
console.log(array); //[ 1, 2, 3, 4, 5, 6 ]
array = [...init_array];
bubbleSort_2(array);
console.log(array); //[ 1, 2, 3, 4, 5, 6 ]
array = [...init_array];
bubbleSort_3(array);
console.log(array); //[ 1, 2, 3, 4, 5, 6 ]

```
```javascript
let swap = function (arr, idx_1, idx_2) {
  // idx_1과 idx_2의 자리를 바꾸는 함수
  let tmp = arr[idx_1]; // tmp에 inx_1값 임시저장
  arr[idx_1] = arr[idx_2]; //idx_1을 idx_2로 변경
  arr[idx_2] = tmp; // idx_2를 tmp에저장해놓았던 inx_1값으로 변경
};

//오름차순 정렬
let ascending = function (x, y) {
  return x > y;
};

//내림차순 정렬
let descending = function (x, y) {
  return x < y;
};

let bubbleSort = function (arr, compare) {
  for (let i = 0; i < arr.length - 1; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (compare(arr[j], arr[j + 1])) {
        swap(arr, j, j + 1);
      }
    }
  }
};

// test code
let init_array = [6, 5, 1, 3, 2, 4];
let array;

let sorting = [bubbleSort];
let order = [ascending, descending];
for (let i = 0; i < sorting.length; i++) {
  for (let j = 0; j < order.length; j++) {
    console.log(sorting[i].name, order[j].name);
    array = [...init_array];
    sorting[i](array, order[j]);
    console.log(array);
  }
}

```
선택정렬(Selection Sort) <br>
```javascript
let swap = function (arr, idx_1, idx_2) {
  // idx_1과 idx_2의 자리를 바꾸는 함수
  let tmp = arr[idx_1]; // tmp에 inx_1값 임시저장
  arr[idx_1] = arr[idx_2]; //idx_1을 idx_2로 변경
  arr[idx_2] = tmp; // idx_2를 tmp에저장해놓았던 inx_1값으로 변경
};

//오름차순
let ascending = function (x, y) {
  return x > y;
};

//내림차순
let descending = function (x, y) {
  return x < y;
};

let selectionSort = function (arr, compare) {
  for (let i = 0; i < arr.length; i++) {
    let k = i;
    for (let j = i + 1; j < arr.length; j++) {
      if (compare(arr[k], arr[j])) {
        k = j;
      }
    }
    swap(arr, i, k);
  }
};

// testcode
let init_array = [6, 5, 1, 3, 2, 4];
let array;

let sorting = [selectionSort];
let order = [ascending, descending];
for (let i = 0; i < sorting.length; i++) {
  for (let j = 0; j < order.length; j++) {
    console.log(sorting[i].name, order[j].name);
    array = [...init_array];
    sorting[i](array, order[j]);
    console.log(array);
  }
}
```
삽입정렬(Insertion Sort) <br>
```javascript
let swap = function (arr, idx_1, idx_2) {
  // idx_1과 idx_2의 자리를 바꾸는 함수
  let tmp = arr[idx_1]; // tmp에 inx_1값 임시저장
  arr[idx_1] = arr[idx_2]; //idx_1을 idx_2로 변경
  arr[idx_2] = tmp; // idx_2를 tmp에저장해놓았던 inx_1값으로 변경
};

//오름차순
let ascending = function (x, y) {
  return x > y;
};

//내림차순
let descending = function (x, y) {
  return x < y;
};

let insertionSort = function (arr, compare) {
  for (let i = 0; i < arr.length; i++) {
    let tmp = arr[i];
    let j;
    for (j = i - 1; j >= 0; j--) {
      arr[j + 1] = arr[j];
      if (compare(tmp, arr[j])) {
        break;
      }
    }
    arr[j + 1] = tmp;
  }
};

// testcode
let init_array = [6, 5, 1, 3, 2, 4];
let array;

let sorting = [insertionSort];
let order = [ascending, descending];
for (let i = 0; i < sorting.length; i++) {
  for (let j = 0; j < order.length; j++) {
    console.log(sorting[i].name, order[j].name);
    array = [...init_array];
    sorting[i](array, order[j]);
    console.log(array);
  }
}
```

병합정렬(Merge Sort) <br>
```javascript
let mergeSort = function (arr, compare) {
  if (arr.length === 1) return arr;

  let m = (arr.length / 2).toFixed(0);
  let left = mergeSort(arr.slice(0, m), compare);
  let right = mergeSort(arr.slice(m), compare);

  let i = 0,
    j = 0,
    k = 0;
  while (i < left.length && j < right.length) {
    arr[k++] = compare(left[i], right[j]) ? right[j++] : left[i++];
  }
  while (i < left.length) arr[k++] = left[i++];
  while (j < right.legnth) arr[k++] = right[j++];

  return arr;
};
```
퀵 정렬(Quick Sort) <br>
공통함수(swap() , ascending() , descending()) <br>



```javascript

```
```javascript

```
```javascript

```
```javascript

``````javascript

``````javascript

```
```javascript

```

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

[배열에서 중복된 값 제거후 새로운 배열반환]
```javascript
function answer(str) {
  let set = new Set(str);
  let set_arr = [...set];
  return set_arr;
}

let input = [
  ["A", "B", "B"],
  ["치킨", "피자", "햄버거", "치킨"],
  ["월", "화", "수", "월", "일"],
];

for (let i = 0; i < input.length; i++) {
  console.log(answer(input[i]));
}
```

[숫자가 들어갈 위치 ]
```javascript



```

```javascript

```

```javascript

```

```javascript

```

