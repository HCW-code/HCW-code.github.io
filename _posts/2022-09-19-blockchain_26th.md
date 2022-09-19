---
layout: single
title: "[블록체인] 스마트 컨트랙트 문법(1)"
categories: blockchain
tag: [솔리디티, 변수, 자료형, 연산자, 함수]
toc: true

---

### 솔리디티

솔리디티는 객체 지향 프로그래밍 언어로써

이더리움 블록체인 플랫폼에서 다양한 스마트 컨트랙트(계약 로직)를 작성할 때 사용된다.

(예 : 투표, 크라운드 펀딩, 블라인드 경매, 다중 서명 지갑 등)

**솔리디티의 특징**

- 정적 타입의 중괄호 언어 : 자바스크립트와 달리 컴파일 시에 변수에 타입이 결정되는 언어이다. 그렇기에 소스 코드에 타입을 명확하게 정의해줘야 한다.
- Ethereum Virual Machine(EVM) : 솔리디티는 EVM이라는 이더리움 가상 스택 머신 위에서 동작한다.
- 세미콜론 : 솔리디티는 문장의 끝에 반드시 세미클론을 붙여야 한다.

#### SPDX License Identifier

스마트 컨트랙트에 대한 신뢰도를 높이고 저작권과 같은 문제를 해소하기 위해 솔리디티 코드의 최상단에 SPDX 라이센스를 명시해야 한다.

SPDX 라이센스는 주석으로 표기한다.

```solidity
//SPDX-License-Identifier: MIT
```

```solidity
//SPDX-License-Identifier: GPL-3.0
```

SPDX 라이센스 리스트 : https://spdx.org/licenses/

#### Pragma

pragma 키워드는 특정 컴파일러의 버전을 표기할 때 사용한다.

pragma는 모든 소스 코드 파일에 있어야 하며, 다른 파일을 임포트 하더라도, pragma는 자동으로 임포트 되지 않는다.

```solidity
//SPDX-License-Identifier: GPL-3.0
pragma solidity 0.8.14;
```

특정 버전 이상의 pragma를 사용할 때는 ^을 붙인다.

```solidity
//SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.14;
```

```solidity
//SPDX-License-Identifier: GPL-3.0
pragma solidity >= 0.4.0 <0.9.0 //0.4.0 이상 0.9.0 미만의 버전을 사용한다.
```

다양한 버전 규칙을 사용할 수 있으며, 버전 규칙은 npm 문법과 동일한다.

npm 버전 규칙 : https://docs.npmjs.com/cli/v6/using-npm/semver

#### Contract

솔리디티 계약은 이더리움 블록체인의 특정 주소를 가진 **기능(코드)**와 상태(데이터)의 모음이다.

여기서 **특정 기능**은 **함수**로 표현하고, **상태**는 **변수**로 표현한다.

마치 일반적인 객체 지향 언어의 클래스를 정의하듯이, 하나의 contract(계약)를 정의한다.

```solidity
contract SimpleStorage {
	uint storedData; //상태변수
	
	//함수
	function set(uint x) public {
		storedData = x;
	}
	//함수
	function get() public view returns (uint){
		return storedData;
	}
}
```

#### Import

파일을 임포트 하는 방식은 자바스크립트에서 사용하는 방식과 동일하다.

```solidity
import "파일이름";

//임포트하는 파일을 symbolName이라는 이름으로 사용
import * as symbolName from "파일이름";
import "파일이름" as symbolName;

//파일의 일부분만 임포트 하는 경우
import {symbol1 as alias, symbol2} from "파일이름"
```

### 변수

#### 데이터 저장 위치

보통 프래그래밍 언어라면 변수는 스택, 힙 등 메모리에 저장되는 것이 기본이다.

하지만 솔리디티는 변수를 메모리 뿐 아닌 하드 디스크 등과 같은 **스토리지**에 저장하기도 한다.

또한 **calldata**라는 영역에 저장하기도 하는데 여기에는 함수 인자가 저장된다.

calldata 역시 메모리처럼 동작하지만 수정 불가능하고 비영구적인 영역이다.

**솔리디티의 데이터 저장 위치**

- 메모리
- 스토리지
- calldata

**강제 데이터 위치**

- 외부 함수의 매개 변수(반환 값 미포함) : calldata
- 상태 변수 : 스토리지

**기본 데이터 **

- 함수의 매개변수(반환 값 포함) : 메모리
- 모든 지역 변수 : 스토리지

#### 변수의 종류

상태변수, 지역변수, 전역변수

지역변수와 상태변수는 일반적인 프로그래밍 언어에서의 변수와 같다.

선언 및 초기화 방식

```solidity
{데이터 타입} {변수명}; //변수명으로 선언
{데이터 타입} {변수명} = {초기화할 값}; //선언 및 초기화
```

전역 변수는 우리가 아는 다른 언어의 전역 변수와는 다르다.

솔리디티만의 특수한 변수(또는 함수)로써 주로 블록체인에 관한 정보를 제공한다.

전역변수는 따로 선언이나 초기화 없이 불러와서 사용한다.

##### 상태변수

상태변수란 컨트랙트 저장소(이더리움 블록체인)에 영구적으로 저장되는 변수를 말한다.

즉, 항상 스토리지에 저장된다.

보통 컨트랙트 최상위 단에 선언한다.

```solidity
pragma solidity ^0.8.14;

contract SimpleStorage {
	uint storedData; //상태변수 선언
	uint storedData2 = 20; //상태 변수 선언 및 초기화
}
```

###### 상태 변수 접근 수준

컨트랙트 내의 상태 변수를 선언할 때는 지정할 수 있는 접근 수준을 함께 표기한다.

- Internal(default)
  - 컨트랙트 및 해당 컨트랙트를 상속받은 컨트랙트만 접근 가능
  - 외부에서 액세스 불가능
- public
  - 컴파일러가 자동으로 getter 함수를 생성
  - 컨트랙트 내에서 직접 퍼블릭 상태 변수를 사용 가능
  - 외부 컨트랙트나 클라이언트 코드에서도 getter 함수를 통해 퍼블릭 상태 변수에 접근 가능
- private
  - 동일한 컨트랙트 멤버만 프라이빗 상태 변수에 접근 가능
- constant/immutable
  - 선언될 때 값을 할당해야함
  - 상수화 = 변경 불가능

##### 지역변수

지역 변수란 함수가 실행될 때까지만 존재하는 변수를 말한다.

지역변수 여기 기본값으로는 스토리지에 저장된다.(레퍼런스 타입의 경우 재정의 가능)

보통 함수 아래에 선언되는 변수를 말한다.

```solidity
pragma solidity ^0.8.14;

contract SimpleStorage {
	uint storedData; //상태변수 선언
	uint storedData2 = 20; //상태 변수 선언 및 초기화
	
	function simpleFunction() public pure returns(uint){
		uint a; //지역변수 선언
		uint b = 1; //지역변수 선언 및 초기화
		a = 1;
		uint result = a + b;
		return result;
	}
}

```

##### 전역변수

전역변수란 글로벌한 블록체인 안에 있는 특수 변수를 말한다.

블록체인 및 트랜잭션에 대한 속성을 가지고 올 수 있다.

```solidity
function f(uint start, uint daysAfter) public {
	if(block.timestamp >= start + daysAfter * 1 days){
		//여기서 block.timestamp는 전역 변수
	}
}
```

- block : 블록에 대한 정보를 갖고 있다.
- msg : 컨트랙트를 시작한 트랜잭션 콜이나 메시지 콜에 대한 정보를 갖고 있다.
- tx : 트랜잭션 데이터를 갖고 있다.
- This : 현재 컨트랙트를 참조한다. 현재 컨트랙트 주소로 암시적으로 변환된다.

| 전역변수                     | 데이터 형식     | 설명                                    |
| ---------------------------- | --------------- | --------------------------------------- |
| block hash(uint blockNumber) | Byte32          | 주어진 블록의 해시를 반환               |
| block.basefee                | uint            | 현재 블록의 기본 수수료                 |
| block.chainid                | uint            | 현재 블록의 체인 ID                     |
| block.coinbase               | address payable | 현재 블록의 채굴자 주소                 |
| block.difficulty             | uint            | 현재 블록의 난이도                      |
| block.gaslimit               | uint            | 현재 블록의 가스 한도                   |
| block.number                 | uint            | 현재 블록의 번호                        |
| block.timestamp              | uint            | 현재 블록의 유닉스 타임스탬프           |
| gasleft()                    | uint256         | 남아있는 가스의 양을 반환               |
| msg.data                     | bytes calldata  | 전체 콜데이터 본문                      |
| msg.sender                   | address         | 현재 호출을 수행하고 있는 메시지 발신자 |
| msg.sig                      | bytes4          | 호출 데이터의 첫 4바이트(함수 식별자)   |
| msg.value                    | uint            | 메시지와 함께 보낸 이더(wei) 금액       |
| tx.gasprice                  | uint            | 트랜잭션 가스 비용                      |
| tx.origin                    | address         | 트랜잭션 발신자                         |

### 자료형

- 값 형 데이터 타입(Value Types)
- 참조형 데이터 타입(Reference Types)
<center>
<img src="../../images/2022-09-19-blockchain_26th/image-20220919150216975.png" alt="image-20220919150216975" style="zoom:50%;" />
</center>
#### 값 형 데이터 타입(Value Types)
<center>
<img src="../../images/2022-09-19-blockchain_26th/image-20220919150453554.png" alt="image-20220919150453554" style="zoom: 33%;" />
</center>
1. 불(bool)

   ```solidity
   bool isOpen = true;
   bool isSold = false;
   ```

2. 정수(int, uint)

   부호가 있는 경우에는 int, 부호가 없는 0 이상의 값에는 uint를 사용한다.

   int, uint 뒤에 8 ~ 256의 8의 배수의 숫자를 붙여 변수의 크기를 비트 단위로 지정할 수도 있다.(예 int 8, int 16, int 24, int 64 ...)

   각 숫자에 따라 정수는 특정 범위로 제한된다.

   int16는 -32768 ~ 32767 사이의 정수를 의미하며 uint16은 0 ~ 65535 사이의 정수를 의미한다.

   일반적으로 뒤에 숫자가 없으면 256을 의미한다.

3. 주소

   주소 타입은 크게 두가지 유형으로 나뉜다.

   - address : 20바이트의 이더리움 주소를 가진다.
   - address payable : address와 동일한 값을 가지지만 추가 멤버인 transfer, send를 가진다.

   주소 객체는 0x로 시작하고 최대 40자리의 16진수로 구성되는 문자열을 값으로 가진다.

   중요한 것은 0.8 버전부터 address 형식은 **송금이 불가능한 주소값**이라는 점이다.

   스마트 컨트랙트에서 특정 주소 값으로 송금하기 위해서는 address payable 형식을 사용해야 한다. address payable 형식에는 이더 송금을 위한 transfer() 와 send() 함수가 내장되어 있다.

   address payable 형식 데이터는 address 형식 데이터를 payable() 함수에 인자로 담아 만들 수 있다.

   ```solidity
   address addr1;
   address payable p_addr1 = payable(addr1);
   ```

   uint160 또는 bytes20 형식의 데이터를 address payable로 바꾸기 위해서는 아래와 같이 address() 를 사용한다.

   ```solidity
   uint160 num;
   address addr = address(num);
   address payable p_addr = payable(addr);
   ```

   컨트랙트를 address payable로 변환할 수도 있다.

   만약 컨트랙트가 이더를 받을 수 있는 컨트랙트인 경우, address(컨트랙트)를 수행했을 때 address payable 형식의 주소값을 반환한다.

   ```solidity
   contract C{
   	constructor() payable {
   	
   	}
   }
   
   address payable addr = address(C); //address(C)는 address payable 형식의 주소값 반환
   ```

   하지만 이더를 받지 않는 컨트랙트이면 address 형식의 주소값을 반환한다.

   이 경우 결과값을 payable() 에 넣어 address payable 형식으로 만들 수 있다.

   ```solidity
   contract D{
   	constructor() {
   	
   	}
   }
   address addr = address(D); //address 형식의 주소값 반환
   address payable addr_p = payable(addr); //address payable 형식의 주소값으로 만듦
   ```

4. 바이트 배열(고정 크기)

   데이터를 바이너리 형태로 저장하기 위해 사용한다.

   bytes1 ~ bytes32까지의 고정된 크기의 배열을 선언한다.

5. 열거형(enum)

   열거형(enum)은 특정 값들로 집합을 지정하고, 집합에 있는 데이터만을 값으로 가진다.

   각 집합의 데이터는 내부적으로는 순서에 따라 0부터 1씩 올라가는 정수를 값으로 가진다.

   ```solidity
   enum EvalLevel { Bad, Soso, Great } //열거형 집합을 지정
   EvalLevel kimblock = EvalLevel.Bad //열거형으로 변수 선언
   
   int16 kimblockValue = int16(kimblock) //kimblock dufrjgud rkqt 0을 정수형으로 변환한다.
   ```

추가적으로 (u)fixedMxN 형식으로 표현되는 고정소수점 타입이 존재하지만 현재 솔리디티에서 지원하지 않음

#### 참조형 데이터 타입(Reference Types)
<center>
<img src="../../images/2022-09-19-blockchain_26th/image-20220919152728697.png" alt="image-20220919152728697" style="zoom:50%;" />
</center>
참조형 변수(reference type)는 마치 배열과 같이 연속되어 저장되는 값의 첫번째 메모리의 주소를 값으로 가지는 변수 타입이다.

**데이터 저장 영역**

- 메모리 : 프로그램이 동작하는 동안에만 값을 기억하고, 종료되면 값을 잃는 데이터 영역
- 스토리지 : 블록체인에 기록되어 영구적으로 값이 유지되는 데이터 영역
- calldata : 메모리와 비슷하지만 수정 불가능하고 비영구적인 데이터 영역

참조형 변수를 선언할 때는 메모리에 저장할지 스토리지에 저장할지 명시해야 한다.

(상태변수는 무조건 스토리지에 저장된다.)

```solidity
function f() {
	//5개의 int32 형태의 데이터를 메모리에 저장하는 변수 fixedSlots 선언
	int32[5] memory fixedSlots;
	fixedSlots[0] = 13;
}
```

**참조형 변수의 유형**

- 배열(Array)
- 바이트 배열(가변 크기, Dynamically-sized byte array)
- 문자열(String)
- 구조체(Struct)
- 매핑(Mapping)

1. 배열

   정적 배열: uint[4] {배열 이름}과 같은 형식으로 사용할 배열의 크기를 지정하여 선언한다.

   동적 배열: uint[] {배열 이름}과 같은 형식으로 배열의 크기를 지정하지 않고 선언한다.

   - 5개의 동적 배열로 구성된 배열은 uint[][5]로 작성된다.

   new 키워드를 사용해 동적 배열을 메모리에 할당할 수도 있다.

   **바이트 배열(가변 크기)**

   바이트(bytes)는 특수한 형태의 배열이다.

   배열식 표현의 byte[] 와 유사하지만 calldata 와 메모리를 활용한다는 점이 다르다.

   bytes로 가변 크기의 배열을 선언한다.

   ```solidity
   bytes alphabets = 'abc';
   ```

   **문자열(string)**

   문자열 역시 특수한 형태의 배열로써, 바이트 배열에 기반한 문자열 타입이다.

   string은 bytes와 동일하지만 index, push, length, concat 등을 지원하지 않는다.

   ```solidity
   string name = 'kimblock'
   ```

2. 구조체

   구조체는 서로 다른 유형의 항목을 포함하는 집합으로, 사용자 정의 형식이다.  
   구조체는 배열과 매핑의 내부에서 사용될 수 있으며, 반대로 구조체에 배열과 매핑을 포함할 수 있다.

   하지만 구조체가 동일한 구조체 타입의 멤버를 포함할 순 없다.

   구조체 정의

   ```solidity
   contract exampleC{
   	struct User {
   		address account;
   		string lastName;
   		string firstName;
   			mapping (uint => Funder) funders;
   	}
   	
   	mapping (uint => User) users;
   }
   ```

   구조체 사용할 때는 각 항목에 대한 값을 객체 형식으로 추가한다.

   ```solidity
   contract exampleC{
   	struct User {
   		address account;
   		string lastName;
   		string firstName;
   	}
   	
   	function newUser (address newAddress, string newLastName, string newFirstName) {
   		User memory newOne = User({account: newAddress, lastName: newLastName, firstName: newFirstName});
   	}
   }
   ```

3. 매핑

   매핑(mapping)은 스토리지 데이터 영역에서 키-값 구조로 데이터를 저장할 때 사용하는 참조형이다.

   mapping({키 형식}=>{값 형식}) {변수명} 형태로 선언한다.

   여기서 **키 형식**은 매핑, 구조체, 배열 제외한 유형의 값이 다 될 수 있다.

   여기서 **값 형식**은 매핑, 구조체, 배열을 포함한 모든 유형의 값이 다 될 수 있다.

   ```solidity
   mapping(address => int) public userAddress;
   ```

   
  <center>
   <img src="../../images/2022-09-19-blockchain_26th/image-20220919155610883.png" alt="image-20220919155610883" style="zoom:33%;" />
  </center>
   매핑은 일반적인 프로그래밍 언어에서의 해시 테이블 또는 딕셔너리와 유사하다.  
   키 자체가 실제로 저장되지는 않고, 키의 keccak256 해시를 이용해 값에 접근한다.

   매핑은 오직 스토리지 영역에만 저장될 수 있으므로 상태 변수, 내부 함수에서의 스토리지 참조 타입, 라이브러리 함수의 매개 변수에만 허용된다.

### 함수

선언

```solidity
function 함수이름(파라미터형식1 파라미터1, 파라미터형식2 파라미터2, ...) { ... }
```

함수가 값을 반환하는 경우

```solidity
function 함수이름(파라미터, ... ) returns (반환 형식) { ... }
```

#### 함수 접근 수준

- public(default)
  - 외부에서도 접근 가능
  - 컨트랙트 내부, 외부, 클라이언트 코드에서 모두 호출 가능
- external
  - public 과 비슷함
  - 외부 컨트랙트나 클라이언트 코드에서 호출 가능
- internal
  - 컨트랙트 멤버와 상속된 컨트랙트에서 호출 가능
- private
  - 컨트랙트 멤버만 호출 가능

무언가를 internal 또는 private 로 만드는 것은 다른 계약이 정보를 읽거나 수정하는 것을 방지할 뿐이다.  
퍼블릭 블록체인 특성상 공개되어 있다.

```solidity
contract exampleC{
	function changeName(address account, string newName) internal{ ... }
	function checkGas(uint256 amount) private returns (bool) { ... }
}
```

#### Qualifier

함수가 컨트랙트의 내부 상태를 변경할 수 있는 능력을 선언하는 것

- view, pure

  view로 표시된 함수는 상태를 변경하지 않는 읽기 전용 함수이다.

  pure는 스토리지에서 변수를 읽거나 쓰지 않는 함수이다.

  ```solidity
  pragma solidity ^0.8.14;
  contract exampleC {
  	uint256 public constant maxLimit = 1000;
  	mapping(address => bool) public frozenAccount;
  	
  	function checkGas(uint256 amount) private pure returns (bool) {
  		if(amount < maxLimit) return true;
  		return false;
  	}
  	
  	function validateAccount(address account) internal view returns (bool) {
  		if(frozenAccount[account]) return true;
  		return false;
  	}
  }
  ```

- payable

  payable을 선언하면 함수에서 이더를 받을 수 있다.

  ```solidity
  pragma solidity ^0.8.14;
  contract exampleC{
  	function getEther() payable returns (bool) {
  		if(msg.value === quoteFee){
  			//..
  		}
  	}
  }
  ```

#### 생성자 함수(constructor)

생성자 함수를 선언하면, 컨트랙트가 생성될 때 생성자 함수가 실행되며 컨트랙트의 상태를 초기화할 수 있다.

- constructor 키워드 사용
- 컨트랙트 당 1개만 작성
- 생성자 함수 생략시 기본 생성자(default constructor)가 생성된다.
- 생성자 함수의 함수 접근 수준(visibility)은 internal이거나 public이어야 하지만, 0.7버전 이후부터는 visibility를 붙이지 않는다.

```solidity
pragma solidity ^0.8.14;
contract exampleC{
	
		address public account;
		
		constructor(address _account) {
			account = _account;
		}
	}
}
```

#### selfdestruct

컨트랙트 소멸

```solidity
selfdestruct(컨트랙트 생성자의 주소)
```

### 함수 제어자(modifier)

비슷한 역할을 하는 코드를 모아서 만든 특별한 형태의 함수이다.

함수 선언에 modifier를 추가하여 함수에 변경자(함수를 실행하기 전, 요구 조건을 만족하는지 확인하는 작업)를 적용할 수 있다.

변경자를 작성할 때는 _;을 사용한다. _;는 함수를 실행하는 시점을 나타내며, 변경자 코드는 _; 코드를 기준으로 실행 시점이 달라진다.

다음의 changeNum 변경자는 함수를 실행하기 전 num 상태 변수의 값을 올리고 함수의 실행이 완료되면 num 상태 변수의 값을 1을 내린다.

```solidity
int public num = 0;
modifier changeNum{
	num++;
	_;
	num--;
}
```

changeNum 변경자는 다음과 같이 사용될 수 있다.

```solidity
function func() public changeNum {
	if(num == 1){
		//do something
	}
}
```

함수 func() changeNum을 사용하기 때문에 func() 는 changeNum 변경자의 _;를 기준으로 다음과 같이 동작한다.
<center>
<img src="../../images/2022-09-19-blockchain_26th/image-20220919171201253.png" alt="image-20220919171201253" style="zoom:33%;" />
</center>
이렇게 함수 변경자를 사용하면 함수를 선언적으로 사용할 수 있는 특징이 있다.