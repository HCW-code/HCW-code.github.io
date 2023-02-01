---
layout: single
title: "[node.js] 입력받기"
categories: project
tag: [codingtest, node.js]
toc: true

---

## 입력 받기

### fs모듈

한줄 입력

```js
//입력
//1 2 3

const fs = require('fs');
const input = fs.readFileSync('/dev/stdin').toString().split(' '); // 공백으로 자르기
const num = Number(input[0]); //1
```

여러 줄 입력 + 덧셈

```js
//첫번째 줄 총 개수
//  입력 예시           출력 예시
//  5									2
//  1 1								46
//  12 34							505
//  5 500							100
//  40 60							2000
//  1000 1000


const fs = require('fs');
const input = fs.readFileSync('/dev/stdin').toString().split(\n);
const count = input[0];
const numbers = '';

for(let i = 1; i <= count; i++){
	let num = input[i].toString().split(' ');
	numbers += parseInt(num[0])+ parseInt(num[1]) +'\n';
}
```



