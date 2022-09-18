---
layout: single
title: "[블록체인] Geth 기초"
categories: blockchain
tag: [docker, geth, 계정 생성, 채굴, 트랜잭션 생성]
toc: true

---

## Docker로 Ubuntu 실행

1. 도커에서 우분투 이미지 다운

   ```shell
   docker search ubuntu
   docker pull ubuntu
   ```

2. 이미지 확인

   ```shell
   docker image ls
   ```

3. con_ubuntu라는 컨테이너를 생성한다.

   ```shell
   docker create -it --name con_ubuntu ubuntu
   ```

4. con_ubuntu 컨테이너를 시작한다.

   ```shell
   docker start con_ubuntu
   ```

5. 실행 중인 컨테이너 목록을 확인한다.

   ```shell
   docker ps
   ```

6. 터미널에 컨테이너를 연결한다.

   ```shell
   docker attach con_ubuntu
   ```
   <center>
   <img src="../../images/2022-09-15-blockchain_23th/image-20220915174318742.png" alt="image-20220915174318742" style="zoom: 50%;" />
   </center>
7. 컨테이너를 세팅한다.

   ```shell
   apt update -y && apt install -y software-properties-common
   ```

   실행 후 위치와 타임존을 선택해야 한다. 자신의 위치에 맞게 숫자를 입력한다.

   ```shell
   add-apt-repository ppa:ethereum/ethereum
   ```

   ```shell
   apt-get install vim -y
   apt update -y && apt install geth
   apt-get install git -y
   cd ~
   git clone https://github.com/ethereum/go-ethereum
   apt-get install -y build-essential golang
   ```

8. 설치한 geth의 버전 확인

   ```shell
   geth version
   ```

   

## Geth 기초(1) - 계정 생성과 채굴

### 1. 로컬 테스트넷에서 Geth 실행

로컬 테스트넷에서 Geth를 실행하기 위해서는 데이터 디렉터리와 genesis.json 파일이 필요하다.

- 데이터 디렉터리는 송수신한 블록 데이터와 계정 정보를 저장한다.
- genesis.json 은 블록체인의 Genesis 블록의 정보가 저장된 json 형태의 텍스트 파일이다.

1. 데이터 디렉터리와 gensis.json 파일을 만든다.

   ```
   go-ethereum
    - test_data
    	- genesis.json
   ```

2. geth를 실행하여 정상적으로 작동하는지 확인한다.

   ```shell
   geth
   ```

### 2. Geth console을 사용하여 계정 생성

1. 계정 생성

   ```shell
   geth --datadir test_data account new
   ```

   새로운 계정에서 사용할 비밀번호 입력

2. 계정 확인

   ```shell
   geth -datadir test_data account list
   ```

### 3.GenesisBlock 만들기

1. genesis.json 파일을 연다.

   ```shell
   vim test_data/genesis.json
   ```

   

2. genesis.json 속성 설정

   ```json
           {
             "config": {
               "chainId": 8484,
               "homesteadBlock": 0,
           	  "eip150Block": 0,
               "eip155Block": 0,
               "eip158Block": 0
             },
             "difficulty": "20",
             "gasLimit": "2100000",
             "alloc": {
               "계정의 주소값": { "balance": "300000" }
             }
           }
   ```

   - config : 이더리움 관련 설정이 들어있다.
   - config.chainId : chain id는 현재 chain을 구별하는 값이며 replay attack으로부터 보호해주는 역할을 한다.
   - config.homesteadBlock : homestead는 이더리움의 4단계 로드맵 중 두 번째 메이저 단계이다. 속성값이 0인 경우, true를 의미한다.
   - config.eip150Block : IO가 많은 작업에 대한 가스 변경 비용을 위한 설정이다.
   - config.eip155Block : EIP는 Ethereum Improvement Proposal의 약자로 개발자들이 이더리움을 업그레이드하기 위해 제안된 아이디어를 의미한다. EIP155는 chainId와 마찬가지로 replay attack을 막기 위한 설정이다.
   - config.eip158Block : EIP158은 계정의 상태가 변경되고 변경된 결과값으로 인해 계정의 nonce와 balance 값이 0이 되고 code와 storage가 빈 값이 되는 경우 해당 계정을 삭제한다.

   위의 4가지 Block 설정은 사설 블록체인을 만들때 기본적으로 동일한 설정이다.

   - difficulty : 채굴 난이도이다. 값이 클수록 난이도가 상승하며, 낮을 수록 난이도가 낮아진다.

   - gasLimit : 블록당 담을 수 있는 가스의 한도를 설정한다. 하나의 블록 안에 담을 트랜잭션 개수를 결정하는데 사용하는 옵션이다.

   - alloc : 제네시스 블록이 생성됨과 동시에 alloc에 등록된 주소로 이더를 전송한다.
     <center>
     <img src="../../images/2022-09-15-blockchain_23th/image-20220918201720848.png" alt="image-20220918201720848" style="zoom: 33%;" />
     </center>
   - parentHash : 부모 블록의 해시값을 넣는다. 제네시스 블록은 부모 블록이 없기 때문에 사용하지 않는다.

   - coinbase : 제네시스 블록 채굴 시 주어지는 보상이다.

   - nonce, mixhash : 블록이 올바르게 채굴되었는지 증명한다. 블록체인 작업증명을 위해서는 가장 최근에 추가된 블록의 해시값과 블록 헤더의 다양한 값, 임의의 값 nonce의 조합으로 특정 범위에 있는 수를 찾는다. mixhash는 nonce를 찾기 위한 중간 계산값이다. 이를 가지고 있는 이유는 공격자가 잘못된 nonce로 블록을 만드는 경우, 위조 여부를 빠르게 확인하기 위함이다.

     mixhash와 nonce는 "블록을 제대로 만들었는지 증명하는 용도"이다.

     제네시스 블록은 채굴을 통해서가 아닌 json파일로 직접 만들기 때문에 채굴에 사용되는 mixhash와 nonce값이 필요하지 않다. 다만 다른 누군가가 랜덤한 값을 넣어 우연히 똑같은 제네시스 블록으로 체인을 연결하지 않도록 할 수 있다.

   - timestamp : 해당 블록이 취득된 시점을 의미하는 값으로, 유닉스 타임스탬프값이 들어간다. 제네시스 블록은 최초의 블록이기 때문에 0으로 설정해도 된다. timestamp 값은 블록 간의 순서와 난이도를 조절하는데 사용된다.

### 4. Genesis Block을 생성 및 초기화

1. 제네시스 블록을 생성 미 초기화한다.

   ```shell
   geth --datadir test_data init test_data/genesis.json
   ```

2. test_data 디렉터리에 생성된 파일을 확인한다.

   tree모듈을 사용하여 트리 형태로 디렉터리 구조 확인

   ```shell
   apt-get install tree -y
   tree test_data/
   ```

### 5. Geth 실행

1. geth 실행

   ```shell
   geth --networkid 8484 --nodiscover --datadir test_data -allow-insecure-unlock --http.addr 0.0.0.0 --http --http.port 8545 --http.corsdomain "*" --http.api="db,eth,net,web3,personal,miner,admin" --miner.threads 1 console 2>> test_data/geth.log
   ```

   - -datadir test_data : 데이터 디렉터리를 지정한다.
   - networkid 8484 : 네트워크 식별자
   - http : rpc였으나 현재 http로 변경
   - http.addr "ip" : IP는 현재 사용 중인 IP를 입력한다.
   - http.port "port" : 포트 번호를 원하는 것으로 설정한다.
   - http.corsdomain "*" : 접속할 수 있는 RPC 클라이언트 URL을 지정하는 것인데 "*"경우 전체 허용이다.
   - -nodiscover : 생성자의 노드를 다른 노드에서 검색할 수 없게 하는 옵션이다. 즉 같은 제네시스 블록과 네트워크 ID에 있는 블록들이 연결되는 것을 방지한다.
   - http.api "db,eth,net,web3,personal" : rpc에 의해 접근할 수 있는 api
   - -maxpeers 0 : 생성자의 노드에 연결할 수 있는 노드의 수를 지정한다. 0을 지정하면 다른 노드와 연결하지 않는다.
   - 2>> /home/ngle/data_testnet/geth.log : 로그 파일을 만들 때 사용할 옵션으로 에러를 해당 경로의 파일에 저장한다.

   

### Etherbase 설정

EOA는 일반 사용자가 사용하는 계정으로 비밀키로 관리된다. Ether를 송금하거나 계약을 실행할 수 있다. CA는 컨트랙트는 블록체인에 배포할 때 만들어지는 계정으로 블록체인에 존재한다.

Geth console에서 personal.newAccount 명령으로 EOA를 만들 수 있다.

1. 계정 확인

   ```
   eth.accounts
   ```

2. 새로운 계정 추가

   ```
   personal.newAccount('password')
   ```

3. 채굴 시 보상받을 계정을 선택한다.

   이더리움을 채굴하고 보상받는 계정을 Etherbase라고 한다. Etherbase는 eth.coinbase 변수에 저장된다. 기본적으로 eth.accounts[0]이 설정된다.

   ```
   miner.setEtherbase(personal.listAccounts[0]);
   ```

4. 계정 잔고 확인

   ```
   eth.getBalance(eth.accounts[0])
   ```

5. wei가 아닌 ether 단위로 변환하여 표시

   ```
   web3.fromWei(eth.getBalance(eth.coinbase), 'ehter')
   ```

6. 블록의 수와 블록 정보 확인

   ```
   eth.blockNumber //생성된 블록 수 조회
   eth.getBlock(0) //0번째 블록의 정보 출력
   ```

7. 계정 상태 확인

   ```
   personal.listWallets[0].status //Locked 또는 Unlocked 출력
   ```

8. 잠긴 계정 해제

   3가지 명령어로 해제 가능

   ```
   personal.unlockAccount(eth.coinbase)
   personal.unlockAccount(eth.coinbase, "계정명")
   personal.unlockAccount("주소", "패스워드", 유효기간)
   //유효기간을 0을 입력하면 geth 프로세스가 종료될때까지 unlock 상태 유지
   ```

### 7. 이더리움 채굴

1. 채굴 시작

   miner.start(n) 명령어에서 n은 스레드의 개수이다.

   ```
   miner.start(1)
   ```

2. 채굴 진행 확인

   ```
   eth.mining
   ```

3. 최근에 추가된 블록의 숫자를 확인한다.

   ```
   eth.blockNumber
   ```

4. 채굴 종료

   ```
   miner.stop()
   ```

   

## Geth 기초(2) - 트랜잭션 생성과 채굴

### 1. 이더 송금과 트랜잭션 및 블록 정보 확인

1. 처리해야할 트랜잭션 목록 확인

   ```
   eth.pendingTransactions //출력이 []안에 담겨서 나옴
   ```

2. account0에서 account1로 1이더 전송

   ```
   eth.sendTransaction({
   	from:eth.accounts[0],
   	to:eth.accounts[1],
   	value:web3.toWei(2,'ether'),
   	data:web3.toHex("send message")
   })
   ```

   - from : 트랜잭션을 보내는 계정의 주소
   - to : 수신자 계정의 주소
   - value : 전송할 금액
   - data : 전송할 메시지
   - web3.toHex : 인자로 주어진 값을 16진수 값으로 변환. 문자열의 경우 UTF-8 문자열로 표현된다.

   정상적으로 트랜잭션이 만들어지면 터미널에 트랜잭션 해시가 출력된다.

   그리고 채굴을 시작하면 블록이 생성된다.

3. 이전에 트랜잭션을 생성하면서 얻었던 트랜잭션 해시값을 사용해, 트랜잭션에 대한 정보를 확인할 수 있다.

   ```
   eth.getTransaction("트랜잭션 해시값")
   ```

4. 블록번호를 통해서도 트랜잭션 내용을 조회할 수 있다.

   ```
   eth.getTransactionFromBlock(467) //blockNumber
   ```

5. 블록에 대한 정보 확인

   ```
   eth.getBlock(467)
   ```

### 2. 송금 수수료 확인

위에서 eth.accounts[0]에서 수수료가 빠져나가지 않은것은 채굴 수수료가 블록의 채굴자에게 돌아가게 되는데 eth.accounts[0] 계정은 송금자인 동시에 채굴자이기 때문이다.

gas와 gasPrice를 확인하면 되는데 gasPrice는 1gas의 가격이며, 단위는 wei/gas이다. gas는 지불할 수 있는 최대 gas이며, 실제로 해당 트랜잭션을 처리하는데 지불한 gas는 아니다.

```
지불한 수수료(wei) / gasPrice = 2,100,000,000,000 / 18,000,000,000 = 21000 gas
```

## 로컬에서 두 개의 노드 연결

실제 이더리움은 여러 개의 노드가 서로 연결되어 있으므로, 두 개의 노드를 서로 연결하여 동기화가 일어나도록 구성한다.

먼저 도커 CLI를 이용해 도커의 접속을 수정한다. 기존의 attach를 사용하면 서로 다른 여러 터미널로 도커에 접속하더라도 하나의 도커 터미널에 연결이 된다. 그래서 서로 다른 터미널로 도커에 접속했을때 각 터미널이 서로 다른 화면을 만날 수 있도록 해야한다.

```shell
# 실행중인 container list 확인
docker ps -a
# container 실행; 여기서는 'con_ubuntu'
docker start con_ubuntu
# container 이름에 따라 일부 수정하여 다음 명령어로 도커에 접속 실행
docker exec -it con_ubuntu bash
```

명령어 exec을 통해 하나의 도커에서 다양한 터미널 활동을 할 수 있다.
<center>
<img src="../../images/2022-09-15-blockchain_23th/image-20220918231037821.png" alt="image-20220918231037821" style="zoom:50%;" />
</center>
두 개의 Geth 노드를 생성하고 연결한다. 이를 위해 두 개의 터미널 모두 docker CLI에 접속하여야 한다.

두개의 폴더를 go-ethereum 폴더 안에 생성한다.

Go-ethereum 폴더는 홈폴더 아래에 있다. 따라서 geth 명령어가 실행되는 기본 경로는 ~/go-ethereum/ 이다.

```shell
mkdir test_node1 test_node2
```

Get 노드를 생성하기 위해 각 폴더 안에 genesis.json 파일을 생성한다.

```json
{
  "config": {
    "chainId": 1007,
    "homesteadBlock": 0,
    "eip150Block": 0,
    "eip155Block": 0,
    "eip158Block": 0
  },
  "difficulty": "0x20000",
  "gasLimit": "0x2fefd8",
  "alloc": {},
  "coinbase": "0x0000000000000000000000000000000000000000",
  "extraData": "",
  "nonce": "0x0000000000000000",
  "mixhash": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "timestamp": "0x00"
}
```

이번에는 alloc에 초기 지갑 주소가 없다.
<center>
<img src="../../images/2022-09-15-blockchain_23th/image-20220918232438728.png" alt="image-20220918232438728" style="zoom:33%;" />
</center>
### 1. Node 생성

genesis.json 파일로 genesis block을 생성한다.

```
geth --datadir test_node1 init test_node1/genesis.json
geth --datadir test_node2 init test_node2/genesis.json
```

### 2. 두 개의 노드 연결

1. 터미널 1에서 첫번째 노드에 연결한다.

```
geth --networkid 1007 --datadir test_node1 --nodiscover --port 30303 --allow-insecure-unlock --authrpc.port "8547" --http --http.port "8548" --http.addr "0.0.0.0" --http.corsdomain "*" --http.api "eth, net, web3, miner, debug, personal, rpc" console
```

터미널 2에서 두번째 노드에 연결한다.

```
geth --networkid 1007 --datadir test_node2 --nodiscover --port 30304 --allow-insecure-unlock --authrpc.port "8549" --http --http.port "8550" --http.addr "0.0.0.0" --http.corsdomain "*" --http.api "eth, net, web3, miner, debug, personal, rpc" console
```

서로 다른 노드에 접속했는지 확인하려면, 채굴을 진행하거나 각 노드에서 생성한 지갑 주소가 공유되고 있는지 확인하면 된다.

2. 터미널 1에서 다음 명령어를 입력한다.

   ```shell
   admin.nodeInfo.enode
   ```

   enode:// 로 시작하는 문자열이 출력되면 복사한다.

3. 터미널 2로 이동하여, 다음 명령어를 실행한다.

   ```
   admin.addPeer("첫 번째 노드의 enode 주소")
   ```

   명령어 admin.peers로 노드와 연결된 피어의 정보를 확인할 수 있다.
   <center>
   <img src="../../images/2022-09-15-blockchain_23th/image-20220919002904258.png" alt="image-20220919002904258" style="zoom: 33%;" />
   </center>
   

### 3. 채굴(마이닝)

1. 첫번째 노드에서 새로운 계정 생성

2. 계정을 생성한 후 miner.start()로 채굴 시작

3. miner.stop()으로 채굴 종료

4. 두 노드에서 eth.blockNumber를 입력해 블록의 숫자를 확인한다.

   두 노드의 블록 숫자가 동기화 된 것을 확인

### 4. 트랜잭션 생성

1. 첫번째 노드의 지갑의 잠금을 해제하고 트랜잭션을 두번째 노드의 지갑으로 보낸다.

   ```
   personal.unlockAccount(eth.coinbase)
   #PassPharse 입력
   #다음의 to에는 두번째 노드의 지갑 주소를 입력한다.
   eth.sendTransaction({
   	from: eth.coinbase, to: "0xb097f42d670da585b2939a9fa0d47b679cb6dfc4", value: web3.toWei(5, "ether")
   })
   ```

2. eth.pendingTransactions로 대기중인 Tx를 확인

3. 첫번째 노드에서 채굴을 시작하고 나서 중단한 후 두 번째 노드의 지갑 주소로 ETH가 들어온 것을 확인



## Geth 명령어 모음

**--networkid value**

geth로 생성된 블록체인 네트워크의 ID를 지정해준다. 1~4는 미리 정해진 숫자이기 때문에 다른 숫자를 입력해준다. 1은 Frontier, 2는 Morden, 3은 Ropsten, 4는 Rinkeby 이며, 별도로 지정되지 않을 시 디폴트 값은 1이다.

```
geth --datadir data --networkid 15
```

**--http 관련 옵션**

http-rpc 서버와 관련된 옵션이다. 해당 옵션을 사용하면 외부에서 geth에 접근할 수 있다. --http 옵션을 통해 geth에 접근할 때 어떤 포트로 접근하는지, 어떤 모듈을 사용하게 할 것인지 지정할 수 있다.

```
--http //Enable the HTTP-RPC server
--http.addr value //HTTP-RPC server listening interface(default : "localhost")
--http.port value //HTTP-RPC server listening port(default : 8545)
--http.api value //API's offered over the HTTP-RPC interface
--http.corsdomain value
```

**--ws 관련 옵션**

geth에서는 websocket을 지원한다.

```
--ws	//Enable the HTTP-RPC server
--ws.addr value	//HTTP-RPC server listening interface(default : "localhost")
--ws.port value	//HTTP-RPC server listening port(default : 8545)
--ws.api value	//API's offered over the HTTP-RPC interface
--ws.origins value //Origins from which to accept websockets requests
```

**외부 계정 unlock**

geth에서는 보안상의 이유로 rpc를 사용할 때 외부에서 계정을 unlock하는 것을 금지하고 있다. 따라서 외부에서 계정으로 unlock 하기 위해서는 다음의 옵션을 사용해야 한다.

```
--unlock value //Comma separated list of accounts to unlock
--allow-insecure-unlock	//Allow insecure account unlocking when account-related RPCs are exposed by http
--password value	Password file to use for non-interactive password input
```

