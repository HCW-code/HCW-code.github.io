---
layout: single
title: "[블록체인] Web3.js"
categories: blockchain
tag: [web3, 이더리움]
toc: true

---

### Web3.js

이더리움을 사용한 블록체인 어플레케이션을 개발에는 솔리디티 언어를 사용해 스마트 컨트랙트를 개발하거나, 블록체인과 상호작용하는 클라이언트를 개발하는 것을 의미한다.

Web3.js를 사용하는 것은 후자에 해당한다. Web3.js는 이더리움 블록체인과 상호작용하는 클라이언트를 개발하는 데 사용한다.  
Web3는 다른 계정으로 이더를 전송하거나, 스마트 컨트랙트에서 데이터를 읽고 쓰거나, 스마트 컨트랙트를 만드는 등 다양한 액션을 수행할 수 있게 해주는 라이브러리의 집합이다.

#### 클라이언트가 이더리움 블록체인과 상호작용하는 법
<center>
<img src="../../images/2022-10-10-blockchain_35th/image-20221010232644444.png" alt="image-20221010232644444" style="zoom: 50%;" />
</center>
Web3.js는 이더리움 블록체인과 JSON RPC를 사용하여 소통한다. JSON RPC는 "Remote Procedure Call" 프로토콜의 약자이다.  
Web3.js는 네트워크에 있는 데이터를 읽거나 써야할 때 JSON RPC를 사용해 하나의 이더리움 노드에게 요청을 보낸다.

JSON RPC는 XMLHttpRequest를 사용하는 것과 똑같다. 웹에서는 클라이언트가 XMLHttpRequest라는 정해진 형식에 맞춰서 서버에 데이터를 요청한다. 마찬가지로 이더리움에서는 클라이언트가 JSON RPC라는 정해진 형식에 맞춰서 이더리움 노드에 데이터를 요청하는 것이다.

Web3.js 에는 다음과 같은 다양한 모듈이 있다.

- web3-eth : 이더리움 블록체인과 스마트 컨트랙트 모듈
- web3-shh : P2P 커뮤니케이션과 브로드캐스트를 위한 위스퍼 프로토콜 모듈
- web3-bzz : 탈중앙화 파일 스토리지를 위한 스왐 프로토콜 모듈
- web3-utils : dApp개발자를 위한 유용한 헬퍼 함수들을 모아둔 모듈

window.ethereum - 공급자 객체

EIP-1139를 통해, 메타마스크와 같은 지갑 소프트웨어는 웹 페이지에 자바스크립트 객체 형태로 자신의 API를 노출한다. 이 객체를 '공급자(provider)'라고 한다.

이전에는 각 지갑 소프트웨어들이 자신의 API를 브라우저에 공급자 객체 형태로 표현하였다. 지갑마다 공급자 객체를 구현하는 인터페이스나 동작이 조금씩 달랐기 때문에, 브라우저에서 이 공급자 객체들이 충돌하는 문제가 있었다. EIP-1139는 이더리움 공급자 API를 통일하여 지갑 간 상호 운용이 가능하여지도록 하였다.

EIP-1139에서 지정한 이더리움 공급자 객체는 브라우저 내에서 window.ethereum으로 지정되어 있다.
<center>
<img src="../../images/2022-10-10-blockchain_35th/image-20221011001853137.png" alt="image-20221011001853137" style="zoom:50%;" />
</center>
#### Infura

**블록 동기화 없이 원격 이더리움 노드에 접근하기**

https://infura.io/

Infura는 원격 이더리움 노드를 통해 이더리움 네트워크에 접근할 수 있게 해주는 서비스이다. Infura에서는 RPC URL과 API Key를 제공하기 때문에, 직접 이더리움 네트워크에 접근하여 블록을 동기화하지 않아도 네트워크에 접근할 수 있다.


<center>
<img src="../../images/2022-10-11-blockchain_35th/image-20221011004752653.png" alt="image-20221011004752653" style="zoom:50%;" />
</center>
- Project ID : API Key이다.
- Project Secret : 프로젝트의 비밀 키이다.
- Endpoints : 원격 이더리움 노드를 통해 이더리움 네트워크에 접속할 수 있는 URL이다.

#### Etherscan API

etherscan : https://etherscan.io/ 에서 API키를 가져온다.

공식문서 : https://docs.etherscan.io/

이더스캔에서드 Infura와 같은 이더리움 개발자에게 노드 환경을 제공하는 이더스캔 API를 제공한다.

해당 키를 사용하면 GET/POST 요청 방식으로 이더 스캔 API를 사요할 수 있다.

#### Coingecko

Coingecko는 암호화폐의 시가총액과 시세를 제공한다.

Coingecko에서는 실시간 가격, 거래량, 과거 데이터, 컨트랙트 정보와 같은 다양한 데이터를 API형태로 제공한다.

https://www.coingecko.com/ko