---
layout: single
title: "[node.js] 최대공약수, 최소공배수, 소수"
categories: codingtest
tag: [codingtest, node.js]
toc: true

---

### 최대공약수

- 전부다 해보는 방법

```js
let getGCD = (num1, num2) => {
    let gcd = 1;

    for(let i=2; i<=Math.min(num1, num2); i++){
        if(num1 % i === 0 && num2 % i === 0){
            gcd = i;
        }
    }

    return gcd;
}
```

- 유클리드 호제법 사용

  a와 b의 최대공약수는 (a를 b와 나눈 나머지)와 b의 최대공약수와 같다.

```js
const fs = require("fs");
const input = fs.readFileSync(0).toString().split(' ');

const num1 = parseInt(input[0]);
const num2 = parseInt(input[1]);

const gcd = (a ,b) => {
    return (a % b == 0) ? b : gcd(b, a % b)
}

let answer = gcd(max, min);

console.log(answer + ' ' + (num1 * num2)/answer)
```

### 최소공배수

최대공약수 * 최소공배수 = 두수의 곱

### 소수

2부터 자신의 제곱근까지 반복문을 사용하여 나눴을때 나머지가 없다면 1과 자신 외에  다른 약수가 있다는 것이다.

```js
const fs = require("fs");
const input = fs.readFileSync(0).toString().split('\n');
const count = parseInt(input[0]);
let num = input[1].split(' ');
let result = 0;
let sosu = true;

for(let i = 0; i < count; i++){
    if(num[i] == 1){ // 1일때는 소수가 아님 
        sosu = false;
    }else{
        for(let j = 2; j <= Math.sqrt(num[i]); j++){ // j가 제곱근까지만 검사하면 됨
            if(num[i] % j == 0){
                sosu = false;
                break;
            }
       }
    }
   if(sosu == true){
    result++;
   }
   sosu = true;
}

console.log(result)
```

