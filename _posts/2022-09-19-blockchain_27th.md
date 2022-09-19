---
layout: single
title: "[블록체인] 스마트 컨트랙트 문법(2)"
categories: blockchain
tag: [이벤트, 에러, 상속, 라이브러리, 조건문, 반복문]
toc: true
---

### 이벤트 및 에러 핸들링

#### 이벤트

이벤트는 어떤 결과가 발생했을 때 해당 컨트랙트에서 dApp 클라이언트, 또는 다른 컨트랙트에게 전달한다.

컨트랙트는 event 키워드를 사용해 이벤트를 설정하고, 때에 따라 emit 키워드를 사용해 이벤트를 실행한다. 이벤트가 실행된 경우, 트랜잭션에 기록된다.

```solidity
contract coinTransfer {
	event Transfer(address from, address to, uint256 value);
	
	function transfer(address to, address amount){
		//...
		
		//emit 이벤트명(인자1, 인자2, ...)
		emit Transfer(msg.sender, to, amount);
	}
}
```

#### 에러 핸들링

솔리디티에서는 에러를 처리할 때 assert, require, revert 함수를 사용한다.

- revert : 해당 함수 종료하고 에러 반환

  ```solidity
  pragma solidity ^0.8.14;
  
  contract VendingMachine {
  	address owner;
  	
  	function buy(uint amount) public payable {
  		if(amount > msg.value /2 ether)
  			revert("not enough"); //에러를 반환하면서 에러 메시지 지정
  			
  			//송금 진행
  	}
  }
  ```

  

- require, assert : 설정한 조건이 참인지 확인하고, 조건이 거짓이면 에러 반환

  require는 그 자체로 if...revert처럼 사용되는 게이트키퍼 역할을 한다.

  ```solidity
  pragma solidity ^0.8.14;
  
  contract VendingMachine {
  	address owner;
  	
  	function buy(uint amount) public payable {
  		require(
  				amount <= msg.value / 2 ether, //주어진 조건이 참이면 넘어가고, 거짓이면 에러 반환
  				"Not enough" //에러 메시지 지정
  			);
  			
  			//송금 진행
  	}
  }
  ```

  assert는 require와 사용법이 동일하나 사용하지 않은 가스를 호출자에게 반환하지 않고, 공급된 가스를 모두 소모하며 상태를 원래대로 되돌린다.

### 상속 및 라이브러리

#### 상속

솔리디티의 contract 객체는 상속을 지원한다. 상속을 통해 컨트랙트에 기능들을 추가하고, 확장할 수 있다.

상속을 사용하려면 부모 컨트랙트에 is 키워드를 지정해준다.

```solidity
contract ChildContract is ParentContract {
	//...
}
```

솔리디티는 다중 상속도 지원한다.

#### 라이브러리

라이브러리의 목적은 코드를 공유하기 위함이다.

참고 : https://www.openzeppelin.com/

외부 라이브러리를 호출할 시에는 기존 컨트랙트 호출과는 다른 방식으로 진행한다.

- contract 키워드 대신 library 키워드 사용
- 상태 변수, 상속 관계, fallback 함수, payable 함수 지원 안됨
- 파라미터 받는 것 가능
- 호출 방법:
  - 라이브러리 이름.메소드이름()
  - using 라이브러리 이름 for 데이터타입

```solidity
import "./UIntFunctions.sol";
contract Example {
	function isEven(uint x) publick pure returns(bool) {
		return UIntFunctions.isEven(x);
	}
}
```

```solidity
import "./UIntFunctions.sol";
contract Example {
	using UIntFunctions for uint;
	function isEven(uint x) publick pure returns(bool) {
		return x.isEven
	}
}
```

### 조건문, 반복문

#### 조건문

js와 동일

삼항 연산자

```solidity
function checkCondition(uint x) public pure returns(uint result){
	//result = 조건식 ? 참일 경우 : 거짓일 경우;
	result = x >= 1500 ? 1 : 0;
	return result
}
```

#### 반복문

- while

- do-while

```solidity
do
{
	최초 한번은 무조건 실행
} while (조건식);
```

```solidity
//SPDX-License-Identifier : MIT
pragma solidity ^0.8.14;

contract DoWhileLoop{
	uint[] data;
	uint8 j =0;
	
	function loop(
	) public returns(uint[] memory){
	do {
		j++;
		data.push(j);
	}while(j < 0);
	return data;
	}
}

//data == [1]
```

do-while문은 반복문의 끝에 조건식 검사가 있기 때문에, 조건식이 거짓인 경우에도 **적어도 한번은 무조건 실행**한다는 특징이 있다.

- for

- continue

  continue는 반복문 실행 도중 나머지 코드를 건너뛰고 싶을 때 사용한다.

  while, do-while, for문 안에 사용할 수 있다.

  ```solidity
  while(조건식){
  	조건식이 참이면 여기있는 코드 수행
  	<새로운 조건>{
  		continue;
  		//아래코드를 실행하지 않고 건너뛴다.
  	}
  	카운터 값 증가
  }
  ```

- break

  break는 중간에 반복문을 멈추고 바깥으로 나가고 싶을 때 사용

  while, do-while, for문 안에 사용할 수 있다.