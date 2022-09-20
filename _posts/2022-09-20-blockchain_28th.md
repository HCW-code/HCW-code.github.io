---
layout: single
title: "[블록체인] 스마트 컨트랙트 문법(3)"
categories: blockchain
tag: [오버로딩, 오버라이딩, 추상 계약,인터페이스]
toc: true
---

### 함수 오버로딩

계약은 동일한 이름의 여러 기능을 가질 수 있지만 매개 변수 유형은 다를 수 있다. 이 프로세스를 "오버로딩"이라고 하며 상속된 함수에도 적용된다.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract A {
    function f(uint value) public pure returns (uint out) {
        out = value;
    }

    function f(uint value, bool really) public pure returns (uint out) {
        if (really)
            out = value;
    }
}
```



### 함수 오버라이딩

기존의 함수를 덮어쓰는 것(재정의 하여 동작을 변경한다.)

virtual, override

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Base
{
    function foo() virtual external view {}
}

contract Middle is Base {}

contract Inherited is Middle
{
    function foo() override public pure {}
}
```

다중 상속의 경우

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract Base1
{
    function foo() virtual public {}
}

contract Base2
{
    function foo() virtual public {}
}

contract Inherited is Base1, Base2
{
    // Derives from multiple bases defining foo(), so we must explicitly
    // override it
    function foo() public override(Base1, Base2) {}
}
```

예시

```solidity
// SPDX-License-Identifier:GPL-30
pragma solidity >= 0.7.0 < 0.9.0;

contract Father{
    
    string public familyName = "Kim";
    string public givenName = "Jung";
    uint256 public money = 100; 
    
    constructor(string memory _givenName) public {
        givenName = _givenName;
    }
    
    
    function getFamilyName() view public  returns(string memory){
        return familyName;
    } 
    
    function getGivenName() view public  returns(string memory){
        return givenName;
    } 
    
    function getMoney() view  public virtual returns(uint256){
        return money;
    }
    
    
}

contract Son is Father("James"){
    
    
    uint256 public earning = 0;
    function work() public {
        earning += 100;
    }
    
     function getMoney() view  public override returns(uint256){
        return money+earning;
    }

}
```

### 인터페이스

스마트 컨트랙트에서 정의되어야할 필요한 것

1. 함수는 external로 표시
2. enum, structs 가능
3. 변수, 생성자 불가(constructor X)
4. 다른 컨트랙트나 인터페이스를 상속받을 수 없다.

예시

```solidity
interface ItemInfo {
	struct item{
		string name;
		uint 256 price;
	}
	function addItemInfo(string memory _name, uint256 _price) external;
	function getItemInfo(uint256 _index) external view returns(item memory);
}

contract lec39 is ItemInfo{
	item[] public itemList;
	function addItemInfo(string memory _name, uint256 _price) override public {
		itemList.push(item(_name, _price));
	}
	function getItemInfo(uint256 _index) override public view returns(item memory){
		return itemList[_index];
	}
}
```

### 추상 계약

추상 계약은 인터페이스와 비슷하지만 인터페이스가 더 많은 제한이 있다.

인터페이스 안에는 모조리 추상 메서드이지만 추상클래스는 추상메서드와 일반 메서드가 있을 수 있다.

추상 메서드는 단지 이름과 입력 매개 변수 및 출력 매개 변수만 선언 해 두고 내용은 없는 함수이다.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

abstract contract Feline {
    function utterance() public pure virtual returns (bytes32);
}

contract Cat is Feline {
    function utterance() public pure override returns (bytes32) { return "miaow"; }
}
```

