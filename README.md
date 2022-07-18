# RealEstateDAPP
블록체인 이더리움 부동산 댑(Dapp)

# RealEstateDapp
#BlockChain
#Ethereum
#SmartContract
#Dapp

## 개발 환경 버전
* Solidity v0.4.25
* Truffle v4.1.15
* MetaMask 10.17.0
* Ganache v2.5.4
* Node.js v16.13.2

## ganache네트워크를 이용하여 배포
<center>
<img width="827" alt="스크린샷 2022-01-20 오후 5 12 23" src="https://user-images.githubusercontent.com/64346003/150340497-fddc8d3e-6d43-4a93-8e7a-58c76fd96905.png">
</center>

## 가나슈에서 메타마스크 연동 후 거래
![Hnet-image (3)](https://user-images.githubusercontent.com/64346003/150349381-db53b797-67f6-4abd-b69e-501f77519b6c.gif)

## 강의 자료
https://www.inflearn.com/course/blockchain-%EC%9D%B4%EB%8D%94%EB%A6%AC%EC%9B%80-dapp/dashboard

## + 리믹스를 사용하여 Ropsten 테스트넷 컨트랙 배포 및 테스팅
1. Remix를 이용하여 컨트랙트 배포
<img width="500" alt="스크린샷 2022-01-23 오후 4 28 22" src="https://user-images.githubusercontent.com/64346003/150668868-ff3cd294-fb69-4a59-bbdb-11ca38656ebf.png">

2. 메타마스크를 초기화 시키고 다시 사이트와 연동시켜서 각각 Account1과 Account2에 이더를 기부받는다.(기부 사이트 : https://faucet.metamask.io/)
  - Account 1 : Owner
  - Account 2 : Customer

<img width="600" alt="스크린샷 2022-01-23 오후 4 40 35" src="https://user-images.githubusercontent.com/64346003/150669188-b76f08bf-83e8-4c06-ae70-6bd143857d3b.png">

<img width="600" alt="스크린샷 2022-01-23 오후 4 30 56" src="https://user-images.githubusercontent.com/64346003/150668887-c187a0cc-b668-4767-813c-f998241ec695.png">

3. Ropsten네트워크 ID 인 3으로 변경하며 기부받은 Account1의 주소로 address를 변경
<img width="679" alt="스크린샷 2022-01-23 오후 4 34 31" src="https://user-images.githubusercontent.com/64346003/150669196-fc01ffbe-8ee9-4309-9b46-5d13194d844d.png">

4. Ropsten네트워크에서의 거래

![Hnet-image (4)](https://user-images.githubusercontent.com/64346003/150670576-5ebf73b6-bf92-4c0d-b39a-003f565cd747.gif)

