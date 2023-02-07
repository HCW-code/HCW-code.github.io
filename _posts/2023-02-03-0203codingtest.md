---
layout: single
title: "[node.js] shift/unshift/pop/push"
categories: codingtest
tag: [codingtest, node.js]
toc: true


---

### shift/pop

shift: 배열의 가장 첫 번째 원소를 제거하고 제거된 요소를 반환

pop: 배열의 가장 마지막 원소를 제거하고 제거된 요소를 반환

```js
let arr = [1, 2, 3];
let firstElement = arr.shift();

console.log(firstElement); // expected output: 1
console.log(arr);          // expected output: [2, 3]

let lastElement = arr.pop();

console.log(lastElement); // expected output: 3
console.log(arr);          // expected output: [2]

```

### unshift/push

unshift: 배열의 앞쪽에 데이터를 삽입하고 삽입 된 배열의 길이를 반환

push: 배열의 뒷쪽에 데이터를 삽입하고 삽입 된 배열의 길이를 반환

```js
let arr2 = [1, 2, 3];
let arr2Length = arr2.unshift(4, 5);

console.log(arr2Length); // expected output: 5
console.log(arr2);       // expected output: [4, 5, 1, 2, 3]

arr2Length = arr2.push(6);

console.log(arr2Length); // expected output: 6
console.log(arr2);       // expected output: [4, 5, 1, 2, 3, 6]
```

