---
layout: single
title: "[node.js] slice, splice, 소수점 자리수 지정, sort, 객체 키"
categories: codingtest
tag: [codingtest, node.js]
toc: true


---

### slice()

slice() 메소드는 begin부터 end 전까지의 복사본을 새로운 배열 객체로 반환한다. 즉, 원본 배열은 수정되지 않는다.

slice(start[, end])

- start : 추출 시작점에 대한 인덱스
- end : 추출을 종료할 기준 인덱스

### splice()

splice() 메소드는 배열의 기존 요소를 삭제 또는 교체하거나 새 요소를 추가하여 배열의 내용을 변경한다. 이 메소드는 원본 배열 자체를 수정한다.

splice(start[, deleteCount[, item1[, item2[, ...]]]])

- start : 배열의 변경을 시작할 인덱스
- deleteCount : 배열에서 제거할 요소의 수
- item : 배열에 추가할 요소

### toFixed()

```js
let num = 123.12345

num.toFixed(3); //123.123
```



### Sort()

```js
const arr = [2, 1, 3, 10];

arr.sort(function(a, b)  { //오름차순
  return a - b;
});
```

arr.sort([compareFunction])

- compareFunction - 정렬 순서를 정의하는 함수

이 값이 생략되면, 배열의 element들은 문자열로 취급되어, 유니코드 값 순서대로 정렬됩니다.

이 함수는 두 개의 배열 element를 파라미터로 입력 받습니다.

이 함수가 a, b 두개의 element를 파라미터로 입력받을 경우,

이 함수가 리턴하는 값이 0보다 작을 경우, a가 b보다 앞에 오도록 정렬하고,

이 함수가 리턴하는 값이 0보다 클 경우, b가 a보다 앞에 오도록 정렬합니다.

만약 0을 리턴하면, a와 b의 순서를 변경하지 않습니다.

### Objects.keys()

- 객체의 키 목록을 배열로 리턴한다.
- 객체 내장 메서드가 아니고, 객체 생성자인 Object 가 직접 가지고 있는 메서드이다. 

```js
const obj = {
  name: 'melon',
  weight: 4350,
  price: 16500,
  isFresh: true
}

Object.keys(obj) // ['name', 'weight', 'price', 'isFresh']
```

