---
layout: single
title: "[블록체인] 세그윗, 머글트리"
categories: blockchain
tag: [blockchain, 세그윗, 머글트리]
toc: true

---

## 세그윗(SegWit)

블록체인의 시작이자, 세계 최초의 암호화폐인 비트코인은 매우 느리고 제한된 서비스이다.

- 거래 기록 : 약 10분 단위로 저장
- 승인 : 안전한 거래를 위해서는 최소 6번의 승인 필요

안전한 트랜잭션을 위해서는 약 1시간 이상 소요된다는 문제점이 있다.

또한 용량 문제도 있는데 비트코인 블록은 약 1MB이다.

이러한 속도와 확장성 문제는 결제 및 송금 서비스 등 현실적인 활용을 어렵게 만들고 있다.

블록체인이 지역과 국가를 벗어난 탈중앙화 금융시스템으로 동작하게 하기 위해서는 강력한 탈중앙화, 보안 그리고 초당 3000건 이상 트랜잭션을 처리할 수 있는 속도, 확장성이 필요하다.

| 속도                                                      | 확장성                                                       |
| --------------------------------------------------------- | ------------------------------------------------------------ |
| 합의에 도달하여 거래기록이 장부에 기록되는 데 걸리는 시간 | 갑자기 많은 트래픽이 발생했을 경우 다운이나 지연없이 서비스 연속성이 보장되는 성질 |

현재 블록체인의 속도와 확장성을 개성하기 위한 여러 방법은 크게 4가지가 있다.

1. 블록의 용량 증대
2. 블록체인 내 기술 도입: 샤딩 등
3. 블록체인 외부와 연계
4. 합의 알고리즘 재설계

여기서 **세그윗(SegWit)**은 1. 블록의 용량 증대를 통한 개선 방법 중 하나이다.

### 세그윗
<center>
<img src="../../images/2022-08-25-blockchain_7th/image-20220825134709686.png" alt="image-20220825134709686" style="zoom: 50%;" />
</center>
세그윗이란 Segregated Witness의 약자로서, 비트코인의 블록에서 디지털 서명 부분을 분리함으로써 블록당 저장 용량을 늘리는 소프트웨어 업그레이드를 말한다.

즉, 고정된 블록의 가용 공간을 늘려서 속도를 개선하자는 것이 핵심이다.

기존 비트코인의 블록구조는 디지털 서명 데이터 75%, 그 외 데이터 25% 였다.

그래서 비트코인 관련 커뮤니티에서는 **디지털 서명 데이터를 별도의 공간에 저장하고, 대신 블록에 더 많은 트랜잭션을 담자**는 **세그윗(SegWit)**이라는 제안이 나왔다.

이때 우지한을 비롯한 채굴 세력들을 주축으로 비트코인 시스템에서 블록의 크기 자체를 늘리자는 하드포크 방식도 제안되었지만, 비트코인 커뮤니티는 보다 안정적인 개선이 가능한 세그윗, 즉 소프트 포크 방식을 택하게 되었다.

2017년 8월 1일 기준으로 비트코인은 세그윗을 적용하였다.

디지털 서명 부분만 별도로 Off-Chain에서 작동하게 분리함으로써 기존 시스템에는 영향을 주지 않으면서 처리 속도를 개선할 수 있게 되었다.

### 세그윗의 특징

- 거래 속도의 확장성을 해결
  <center>
  <img src="../../images/2022-08-25-blockchain_7th/image-20220825135431513.png" alt="image-20220825135431513" style="zoom: 50%;" />
  </center>
  비트코인은 1초에 visa나 mastercard에 비해 현저히 적은 수치의 거래밖에 처리하지 못한다.  
  이를 **거래 속도의 확장성 문제**라고 한다.

  비트코인 블록은 디지털 서명을 저장하는 공간, 그 외 데이터(트랜잭션 등)로 구성된다.
  <center>
  <img src="../../images/2022-08-25-blockchain_7th/image-20220825135629378.png" alt="image-20220825135629378" style="zoom:50%;" />
  </center>
  서명란에 실제 서명 데이터가 차지하는 크기는 크지 않지만, 서명란 자체가 차지하는 부피가 크다.  
  세그윗은 서명 부분을 따로 Witness라는 데이터 영역으로 분리해 더 많은 거래를 처리할 수 있도록 업데이트한다.

  단순히 블록의 크기를 늘리는 것도 방법이지만 블록의 크기가 더 커지면 더 많은 해시파워를 요구하고 그렇게 되면 소수의 해시파워를 가진 채굴 노드들로 인해 탈중앙화에서 점차 멀어질 수 있다.

- 거래 가변성 문제를 해결

  모든 비트코인 거래는 해당 거래를 식별할 수 있는 거래의 ID(Transaction ID : TXID)를 포함한다.  
  TXID가 ID라면 TXID를 따라다니는 디지털 서명은 비밀번호라고 할 수 있다.

  거래 가변성은 실질적인 거래 내용에는 변화가 없지만 거래 ID(TXID)만 변경하여 새로운 거래를 만들어 낼 수 있는 일종의 버그이다.

  예를 들어

  1. 유저 1은 유저 2에게 1BTC를 송금한다. 이것을 거래 A
  2. 1BTC 송금을 확인한 유저2는 해당 거래의 txid만 바꿔서 거래 B를 만든다.
  3. 유저 2가 만들어낸 거래가 네트워크에 전파되고 검증된다.
  4. 유저2는 유저1에거 거래 A의 txid를 확인할 수 없다고 한다.(이미 거래 B를 통해 1BTC는 지불된 상태)
  5. 유저 1은 유저2에게 다시 1BTC를 송금한다.

  즉, 위와 같이 두 개 이상의 거래 ID로 서로 다른 거래처럼 보이지만 실제 거래 내역은 동일한 거래를 가질 수 있는 것이 가변성의 문제이다.

  이러한 문제를 막기 위해 서명을 거래와 따로 분리하자는 의견이 제시되었고 이것이 바로 세그윗이다.

  세그윗이 TXID를 따로 보관하고 관리함으로써 여러 개의 ID를 가지고 장난을 치거나 동일한 거래 내역 여러 개를 만드는 것을 방지할 수 있다.

- 버전 호환

  세그윗은 하드포크가 아닌 소프트포크이다.

  비트코인 소프트웨어의 업그레이드를 하지 않아도 세그윗 이전과 세그윗 적용 버전을 모든 노드에서 사용할 수 있다.

  0.13.1버전 이전의 비트코인 코어(비트코인 소프트웨어)는 크기가 1MB 이상인 블록을 읽을 수 없지만 디지털 서명 부분만 빠져있기 때문에 호환이 가능하다.  
  단, 서명 부분이 빠져있기 때문에 구버전의 노드를 이를 검증하지 않고 그냥 받아들이지만, 세그윗이 적용된 버전의 노드들은 디지털 서명을 사용해 신원을 증명한다.

  | 블록 용량 증가                        | 트랜잭션 속도 증가                                      | 트랜잭션 가변성 해결                                         |
  | ------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------------ |
  | 디지털 서명 데이터 분리               | 더 많이 저장할 수 있는 블록을 통해 트랜잭션 속도를 증가 | 서명이 더 이상 트랜잭션 데이터의 일부가 아니기 때문에 해당 데이터를 변경 불가 |
  | 실질 블록 크기는 1MB에서 4MB까지 증가 | 하나의 트랜잭션에 30달러 이상에서 1달러 미만으로 절감   | 서명 조작 불가                                               |

  

## 머클트리(MerkleTree)

머글트리는 여러 데이터에 대해 단계적으로 해시함수를 적용하여 하나의 해시값으로 나타내는 데이터 구조이다.

머클트리는 블록체인에 있는 데이터의 위변조를 방지하고, 데이터가 변하지 않았음(무결성)을 보장하는데 사용한다.

### 머클트리의 동작 방식
<center>
<img src="../../images/2022-08-25-blockchain_7th/image-20220825162852330.png" alt="image-20220825162852330" style="zoom:33%;" />
</center>
머클트리는 위의 그림처럼 여러개의 데이터를 여러 단계를 거쳐 하나의 해시값으로 만드는 트리이다.  
이렇게 여러 데이터를 모아 만들어진 하나의 해시값을 "**머클 루트(Merkle Root)**"라고 한다.

#### 머클 루트가 만들어지는 과정

1. 머클 루트를 만들기 위한 데이터 A, B, C, D가 있다.
2. 각 데이터를 해시함수에 넣어, 해시값을 만든다.
3. 각 해시값을 두개씩 짝지어서 연결한다.
4. 연결된 두 해시값을 해싱한다. hA와 hB를 하나로 연결하고, 이를 해시 함수에 넣어 해싱한다.
5. 이런식으로 최종적으로 하나의 해시값만 남을 때까지 반복한다.
6. 마지막으로 남은 해시값을 다시 한번 해싱한다.

머클트리는 데이터가 1바이트만 변해도 해시함수에 의해 출력값이 변하기 때문에 머클트리는 해시 함수의 충돌 저항성을 활용하여 여러 데이터의 집합 중 단 하나라도 변경되었는지 찾을 수 있다.

### 블록체인에서 머클트리를 사용하는 방법

비트코인의 블록 구조는 다음과 같다.
<center>
<img src="../../images/2022-08-25-blockchain_7th/image-20220825164246438.png" alt="image-20220825164246438" style="zoom:33%;" />
</center>
모든 블록은 고유한 해시값을 갖고 있다.

헤더에는 이전 블록의 해시값, 버전, 난이도, 머클루트, 블록 생성 시간, 논스 등 블록에 대한 내용이 들어있다.

그리고 트랜잭션들이 담겨 있다.

블록의 해시값은 블록 헤더의 모든 값들을 연결하여 해싱한 값이 블록의 고유한 해시값이 된다.

또한 1번 블록의 해시값은 그 다음으로 이어지는 2번 블록의 헤더에 포함된다. 따라서 모든 블록은 자신 바로 앞의 블록 해시값을 가지고 있다.
<center>
<img src="../../images/2022-08-25-blockchain_7th/image-20220825164439319.png" alt="image-20220825164439319" style="zoom:33%;" />
</center>
블록 헤더에 머클루트 = 트랜잭션을 사용해 머클 트리를 만들고 그 결과로 나온 머클 루트 값이다.
<center>
<img src="../../images/2022-08-25-blockchain_7th/image-20220825165011735.png" alt="image-20220825165011735" style="zoom:33%;" />
</center>
블록에 담긴 모든 트랜잭션에 대한 무결성을 보장하는 머클루트 값이 블록 해시에도 들어가게 된다.
<center>
<img src="../../images/2022-08-25-blockchain_7th/image-20220825165707865.png" alt="image-20220825165707865" style="zoom: 50%;" />
</center>
만약 누군가가 악의적으로 트랜잭션 1개를 변경했다면 머클 트리의 특성에 따라 머클루트값도 변하고 블록의 Hash값도 바뀌게 된다.

그래서 특정 블록에 들어있는 트랜잭션을 단 하나라도 변경하는 경우, 블록은 체인처럼 모두 연결되어 있기 때문에 해당 블록 이후에 연결된 블록을 모두 수정해야한다. 블록의 논스값을 찾는데 10분정도 걸리기 때문에, 트랜잭션을 하나 수정하기 위해서는 연결된 모든 블록의 논스값을 다시 찾는 것은 매우 비용이 많이 들 것이다.

따라서 블록체인에 올라간 데이터를 수정하는데 많은 비용이 들기 때문에, 위변조를 하기 매우 어렵다.
