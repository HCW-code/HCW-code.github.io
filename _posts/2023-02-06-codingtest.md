---
layout: single
title: "[baekjoon] js 15649번"
categories: codingtest
tag: [codingtest, node.js, baekjoon]
toc: true

---

이 문제는 DFS를 사용하여 해결할 수 있다. 첫번째가 1, 2, 3, 4를 돈다고 생각하고 그 다음에는 방문했던것을 제외하고 다시 for문을 돈다.

그래서 한 for문이 돌고 나면 넣었던 수를 pop해줌으로써 for문을 돌면서 그 자리에 다른 숫자를 넣어줄수 있게 한다.

pop 다음에는 현재 숫자(ex. 1)를 방문안한걸로 설정해서 pop자리에 다른게 들어오더라도(ex. 2) 다음자리에 방문안했던 숫자(ex. 1)가 올수 있게 한다.

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