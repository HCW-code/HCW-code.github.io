---
layout: single
title: "[baekjoon] js 15649번"
categories: codingtest
tag: [codingtest, node.js, baekjoon]
toc: true

---





```js
let fs = require('fs');
//let input = fs.readFileSync().toString().split(' ').map(el => parseInt(el));
// const N = input[0];
// const M = input[1];

let result = "";
const [N, M] = [4, 3];
const visited = Array(N + 1).fill(0);
const output = [];


const dfs = (cnt) => {
  if (cnt === M) { //주어진 M개 만큼 채워졌다면
        result += `${output.join(" ")}\n`; //출력값에 추가
        return;
    }

  for (let i = 1; i <= N; i++) {
    if (visited[i] === 1) continue; //이미 방문했었다면 통과
 
    visited[i] = 1;
    output.push(i);
    dfs(cnt + 1); //재귀함수 돌리기
 
    output.pop(); // 새로운것을 넣기 위해서 output에 있던것을 뽑음
    visited[i] = 0; // 방문안한걸로 설정
  }
}

dfs(0);

console.log(result.trim())
```