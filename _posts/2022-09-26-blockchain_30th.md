---
layout: single
title: "[블록체인] ERC-20 개발"
categories: blockchain
tag: [erc20, kip7, ganache, truffle, openzeppelin]
toc: true

---

### ERC-20

ERC-20은 Ethereum Request for Comment 20의 약자를 뜻하며 20은 리퀘스트 숫자이다.

**EIP**(Ethereum Improvement Proposals)는 이더리움 개선 제안이고 **ERC**(Ethereum Request for Comments)는 이더리움 기능 표준이다.

ERC-20이라는 표준을 사용하는 이유는 토큰끼리의 호환을 위해서이다. 안드로이드 운영체제를 사용하는 네이버 지도를 카카오톡으로 바로 공유할 수 있는 것처럼 ERC-20 기반으로 생성된 토큰은 상호 호환이 가능하고, ERC-20 기반 토큰들은 동일한 이더리움 지갑으로 전송이 가능하다.

ERC-20 토큰은 스마트 컨트랙트를 통해 생성된다. ERC-20 토큰을 생성하면 이 토큰을 다른 주소로 보낼 수 있으며 여러 가지 역할을 해준다.

이더리움은 자체 블록체인을 기반으로 다양한 탈중앙화 된 애플리케이션들이 작동할 수 있도록 고안된 하나의 플랫폼 네트워크이다. 디앱(dApp)은 이러한 이더리움 플랫폼상에서 스마트 컨트랙트를 이용하여 쉽고 빠르게 토큰을 발행할 수 있다. 이더리움 블록체인에서는 이더(ETH)가 사용되고, 이더리움 블록체인 상의 디앱은 또 다른 다양한 분야에 적용될 수 있는 각각의 솔루션을 지니고 있으며, 그에 맞는 토큰을 발행한다.

이때 발행된 토큰은 독자적인 토큰인 듯하지만 실제로는 **이더리움 생태계에서 호환 및 사용 가능**하다.

디앱 내에서의 토큰 교환은 물론 또 다른 이더리움 플랫폼을 기반으로 한 디앱의 토큰과 교환 가능한데 이를 위해서 ERC-20 토큰 표준이 만들어졌다. 다양한 디앱에 흩어져있는 ERC-20 표준 호환 토큰들은 나중에 통합되어 한번에 이더로 모두 바꾸어 현금화할 수 있다.
<center>
<img src="../../images/2022-09-26-blockchain_30th/image-20220926210108500.png" alt="image-20220926210108500" style="zoom: 33%;" />
</center>


이더리움 생태계에서 호환 및 사용이 가능하다는 것은 이더리움 네트워크에 있는 수많은 플랫폼, 즉 클레이튼, 메타마스크, 마이이더 월렛 등에서 사용할 수 있다는 뜻이다.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity 0.8.14;

interface ERC20Interface {
    function totalSupply() external view returns (uint256);
    function balanceOf(address account) external view returns (uint256);
    function transfer(address recipient, uint256 amount) external returns (bool);
    function approve(address spender, uint256 amount) external returns (bool);
    function allowance(address owner, address spender) external view returns (uint256);
    function transferFrom(address spender, address recipient, uint256 amount) external returns (bool);

    event Transfer(address indexed from, address indexed to, uint256 amount);
    event Transfer(address indexed spender, address indexed from, address indexed to, uint256 amount);
    event Approval(address indexed owner, address indexed spender, uint256 oldAmount, uint256 amount);
}

contract SimpleToken is ERC20Interface {
    mapping (address => uint256) private _balances;
    mapping (address => mapping (address => uint256)) public _allowances;

    uint256 public _totalSupply;
    string public _name;
    string public _symbol;
    uint8 public _decimals;
    uint private E18 = 1000000000000000000;

    constructor(string memory getName, string memory getSymbol) {
        _name = getName;
        _symbol = getSymbol;
        _decimals = 18;
        _totalSupply = 100000000 * E18;
        _balances[msg.sender] = _totalSupply; // 추가
    }

    function name() public view returns (string memory) {
        return _name;
    }

    function symbol() public view returns (string memory) {
        return _symbol;
    }

    function decimals() public view returns (uint8) {
        return _decimals;
    }

    function totalSupply() external view virtual override returns (uint256) {
        return _totalSupply;
    }

    function balanceOf(address account) external view virtual override returns (uint256) {
        return _balances[account];
    }

    function transfer(address recipient, uint amount) public virtual override returns (bool) {
        _transfer(msg.sender, recipient, amount);
        emit Transfer(msg.sender, recipient, amount);
        return true;
    }

    function allowance(address owner, address spender) external view override returns (uint256) {
        return _allowances[owner][spender];
    }

    function approve(address spender, uint amount) external virtual override returns (bool) {
        uint256 currentAllowance = _allowances[msg.sender][spender];  
        require(_balances[msg.sender] >= amount,"ERC20: The amount to be transferred exceeds the amount of tokens held by the owner.");
        _approve(msg.sender, spender, currentAllowance, amount);
        return true;
    }

    function transferFrom(address sender, address recipient, uint256 amount) external virtual override returns (bool) {
        _transfer(sender, recipient, amount);
        emit Transfer(msg.sender, sender, recipient, amount);
        uint256 currentAllowance = _allowances[sender][msg.sender];
        require(currentAllowance >= amount, "ERC20: transfer amount exceeds allowance");
        _approve(sender, msg.sender, currentAllowance, currentAllowance - amount);
        return true;
    }

    function _transfer(address sender, address recipient, uint256 amount) internal virtual {
        require(sender != address(0), "ERC20: transfer from the zero address");
        require(recipient != address(0), "ERC20: transfer to the zero address");
        uint256 senderBalance = _balances[sender];
        require(senderBalance >= amount, "ERC20: transfer amount exceeds balance");
        _balances[sender] = senderBalance - amount;
        _balances[recipient] += amount;
    }

    function _approve(address owner, address spender, uint256 currentAmount, uint256 amount) internal virtual {
        require(owner != address(0), "ERC20: approve from the zero address");
        require(spender != address(0), "ERC20: approve to the zero address");
        require(currentAmount == _allowances[owner][spender], "ERC20: invalid currentAmount");
        _allowances[owner][spender] = amount;  
        emit Approval(owner, spender, currentAmount, amount);
    }
}
```



### KIP-7

KIP-7은 ERC-20을 기반으로 만들어진 내용으로 대체 가능한 토큰(Fungible Token)에 대한 표준이다.

대체 가능한 토큰은 각 토큰 단위가 동일한 가치를 지니며 모든 가용 토큰끼리 서로 호환이 가능하다.

KIP-7으로 만든 토큰은 표준 인터페이스를 통해 클레이튼의 모든 토큰이 지갑에서 탈중앙 거래소에 이르기까지 다른 어플리케이션에서 재사용 할 수 있다.

그중 Fungible Token Standard에 대한 내용은 KIP-7에서 찾을 수 있따.

KIP-7 : https://kips.klaytn.com/KIPs/kip-7

#### KIP-7 vs ERC-20 차이점

다음은 KIP(Klaytn Improvement Proposals)에 기재되어 있는 KIP-7과 ERC-20 차이점이다.

- 더욱 많은 선택 가능한 기능들을 (mint, burn and pause extension) 지원한다.
- 모든 토큰의 transfer/mint/burn 작업은 이벤트 로그별 추적을 거쳐야 한다. 즉, 송금 작업은 무조건 transfer/mint/burn 관련된 작업들에서 발생하여야 한다.
- 각 method group에 KIP-13 인터페이스를 구현해야 한다.

#### 기본적인 KIP-7의 인터페이스 목록

```solidity
//KIP7 Interface
event Transfer(address indexed from, address indexed to, uint256 value);
event Approval(address indexed owner, address indexed spender, uint256 value);
function totalSupply() external view returns (uint256);
function balanceOf(address account) external view returns (uint256);
function transfer(address recipient, uint amount) external returns (bool);
function allowance(address owner, address spender) external view returns (uint256);
function approve(address spender, uint256 amount) external returns(bool);
function transferFrom(address sender, address recipient, uint256 amount) external returns (bool);
function safeTransfer(address recipient, uint256 amount, bytes data) external;
function safeTransfer(address recipient, uint256 amount) external;
function safeTransferFrom(address sender, address recipient, uint256 amount, bytes data) external;
function safeTransferFrom(address sender, address recipient, uint256 amount) external;
```

### Ganache

이더리움 노드는 Geth나 Parity를 사용하여 실제 이더리움 메인(또는 테스트) 네트워크에 접속하여 블록을 모두 동기화시켜야 한다.  
그래서 스마트 컨트랙트를 개발할 때는 가나슈와 같은 가상 혹은 프라이빗 네트워크상에서 스마트 컨트랙트를 구동해보고, 테스트넷을 거쳐 메인넷에 올린다.

#### 개발 및 배포 과정

TestRPC -> TestNet -> MainNet

- TestRPC : 가나슈를 사용해 로컬 환경에서 개발 진행
- TestNet : 개발 완료 후 MainNet과 동일한 환경에서 테스트
- MainNet : 실제 서비스에 사용할 수 있도록 배포

### Truffle

truffle 프레임워크는 스마트 컨트랙트(solidity) 개발 시 개발, 배포 및 테스트 환경을 제공한다.  
이 프레임 워크는 node.js 에서 동작을 하며 npm으로 설치할 수 있다.

**요구사항**

- NodeJS 5.0 이상
- 윈도우, 리눅스, MAC OS X
- JSON RPC API를 지원하는 이더리움 클라이언트

#### Truffle Project 초기화

```shell
truffle init
```
<center>
<img src="../../images/2022-09-26-blockchain_30th/image-20220926212807344.png" alt="image-20220926212807344" style="zoom: 33%;" />
</center>
- contracts : solidity로 개발된 스마트 컨트랙트 소스 파일 폴더

- migrations : 배포를 위한 스크립트 파일 폴더
- test : 개발된 컨트랙트를 테스트하기 위한 폴더
- truffle-config.js : truffle 설정 파일

#### Truffle Develop

```shell
truffle develop
```

위 명령을 실행하면 10개의 Accounts 와 Private Keys가 리스트업 되면서 truffle(develop)> 프롬프트가 나타나게 된다.  
또한 JSON-RPC용(http://127.0.0.1:9545/) 서비스가 제공된다.

#### Smart contract 컴파일

```shell
truffle(develop)> compile
```

위 명령어 실행 시 프로젝트 루트 폴더에 /build 폴더가 생성되며 contracts 폴더 아래에 있는 solidity 파일이 json 형태로 변경되어 생성된다.

#### Smart contract 배포

```shell
truffle(develop)> migrate
```

위 명령어 실행시 /build 폴더에 생성된 파일을 서버에 배포가 된다.

#### Smart contract 테스트

```shell
truffle(develop)> test
```

위 명령어 실행 시 /test 폴더에 있는 .js, .sol 파일을 실행하여 테스트를 수행한다.

주의 : solidity 파일로 테스트 파일을 생성할 때에 파일명은 contract 명과 일치하게 하며, contract name은 Test~ 로 시작하고, 함수명도 test~ 로 시작하여야 한다.

#### Truffle과 Ganache 연동

truffle 설정 파일인 truffle-config.js파일을 수정한다.

<img src="../../images/2022-09-26-blockchain_30th/image-20220926213522926.png" alt="image-20220926213522926" style="zoom:50%;" />

수정 후 truffle networks 확인을 진행한다.

```shell
truffle(develop)> truffle networks
```



이후로 진행할 경우에는 truffle develop을 빠져나와서 실행해야한다. 왜냐하면 truffle develop은 default가 http://127.0.0.1:9545/이기 때문이다.

### OpenZepplin

오픈제플린은 2015년 데미안 브리너와 마누엘 아라오스가 공동 설립한 블록체인 개발 회사이다.

오픈제플린은 솔리디티 기반의 스마트 컨트랙트를 개발하는 프레임워크인 오픈제플린과 스마트 컨트랙트를 관리하고 운영하는 플랫폼인 제플린OS를 제공하고 있다.

```shell
npm install -E openzeppelin-solidity
```

node_modules에서 open zeppelin-solidity 내부 구조를 확인할 수 있다.

#### ERC-20 스마트 컨트랙트 작성

OpenZeppelin 라이브러리를 활용하여 간단한 ERC-20 컨트랙트를 작성 후 배포

ZepplinTestToken.sol 파일 작성

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity 0.8.10;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol"; //라이브러리에 존재하는 ERC20.sol 파일을 가져와서 사용

contract ZeppelinTestToken is ERC20 {
    constructor() ERC20("ZeppelinTestToken", "ZTT") {
          _mint(msg.sender, 100000000e18);
    }
}
```

migration 폴더 안에 2_deploy_ZepplinTestToken.js를 작성

```solidity
var ZeppelinTestToken = artifacts.require("ZeppelinTestToken");

module.exports = function(deployer) {
    deployer.deploy(ZeppelinTestToken);
};
```

배포를 하기 전 사용할 openzepplin/contract 경로를 추가한다.

```shell
npm install @openzeppelin/contracts
```

이후 배포 진행하여 Ganache에서 블록 생성과 Metamask를 활용한 테스트를 실시한다.

```shell
truffle migrate --reset
```

