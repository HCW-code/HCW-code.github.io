---
layout: single
title: "[블록체인] 보안"
categories: blockchain
tag: [보안, 이중지불, 51%공격, 샤딩]
toc: true

---

### 블록체인의 보안적 특징

1. 데이터 무결성

   - 블록체인에서는 합의 알고리즘을 사용해 데이터의 무결성을 보장한다. 합의 알고리즘을 통해 블록에 입력된 데이터에 대해 분산된 각 노드가 모두 동일한 결과를 가질 수 있도록 한다.
   - 합의 알고리즘은 네트워크상에 존재하는 신뢰할 수 없는 노드들이 절차에 맞게 상호 검증하여 네트워크 전체의 무결성을 보장하는 알고리즘이다.

2. 거래 투명성

   - 퍼블릭 블록체인의 경우, 누구나 블록체인 네트워크에 접속해 트랜잭션 기록을 확인할 수 있다. 프라이빗 블록체인도 허가된 사용자라면 누구나 트랜잭션 기록을 볼 수 있다.
   - 거래 기록에 누구나 공개적으로 접근할 수 있기 때문에, 송금 과정을 투명하게 하기 위한 규제 비용을 절감할 수 있다.

3. 감시 가능성

   - 블록체인은 데이터 추가만 가능한 데이터베이스이다.
   - 이 과정에 사용되는 기술이 바로 해시 알고리즘으로 새로 생성되는 블록의 헤더에는 이전 헤더의 해시값이 포함되어 있기 때문에 연결된 모든 블록의 무결성 검증에 사용된다.
   - 그리고 블록에 담긴 트랜잭션을 나타내는 머클 트리의 루트 해시값이 블록 헤더에 함께 포함되어 있으며, 만약 트랜잭션에 변경이 일어나면 머클 해시값이 변경되므로, 블록체인에 대한 위변조 시도를 바로 발견할 수 있다.

   

### 이중지불 문제

이중 지불이란 디지털 현금 시스템 내에 동일한 하나의 자산이 두 명의 수신자에게 동시에 전송되는 문제를 의미한다.

#### 이중지불 문제를 막는 방법

- 중앙화된 접근법 : 데이비드 차움의 eCash
- 탈중앙화된 접근법

#### 비트코인 이중 지불

1. 51% 공격

   단일 주체나 조직이 50% 이상의 해시 레이트를 가지게 될 경우 이들은 원치 않는 트랜잭션을 배제하거나 트랜잭션 순서를 조작할 수 있게 된다. 비트코인에서 해당 공격이 발생할 가능성은 매우 낮지만 규모가 작은 다른 네트워크에서는 발생할 수 있다.

2. 레이스 공격(Race Attacks)

   동일한 자금을 사용하는 두 개의 충돌하는 트랜잭션이 연속으로 전송되지만, 하나의 트랜잭션만 승인되는 것이다. 레이스 공격은 수신자가 체인에 올라가지 않은 트랜잭션을 결제로 수용할 때 가능하다.

3. 핀니 공격(Finney Attacks)

   공격자는 네트워크에 즉각적으로 트랜잭션을 전송하지 않고, 코인을 자신의 다른 지갑으로 전송하는 트랜잭션을 미리 생성해두고, 블록을 미리 채굴해두어 해당 블록에 기록한다. 동일 코인을 다른 트랜잭션에서 사용하는 대신, 이전에 채굴한 블록만을 전송하며, 결제는 무효화된다. 핀니 공격은 특정한 순서에 따라 사건이 발생해야 하며, 수신자는 체인에 올라가지 않은 트랜잭션을 수용해야 발생할 수 있다.

이중 지불은 디지털 현금 시스템에서 경제적 이익을 얻기 위해 동일한 자금을 여러번 사용하는 것이다. 이중 지불 문제는 적절한 해결책이 없었기 때문에, 디지털 현금 시스테의 발전에 큰 걸림돌이었다. 그러나 은닉 서명이 중앙화된 경제 체계에 해결책을 제시하였다. 또한 작업 증명 메커니즘과 블록체인 기술의 개발로 탈중앙화된 자산의 형태인 비트코인이 탄생했으며, 비트코인은 수천 개의 암호화폐 프로젝트에 영감을 주었다.



### 리플레이 공격

리플레이 공격이란 공격자가 보안 네트워크 통신을 가로채고, 해당 통신의 수신자에게 공격자가 원하는 일을 수행하도록 하기 위해 통신을 지연시키거나 재전송하는 방식이다.

리플레이 공격은 해커가 네트워크에서 메시지를 가로챈 후 메시지를 복호화하기 위한 별도의 과정이 필요하지 않으며, 메시지를 포함한 통신 전체를 다시 전송하는 것으로도 공격을 성공할 수 있다.
<center>
<img src="../../images/2022-10-04-blockchain_32th/image-20221004141158100.png" alt="image-20221004141158100" style="zoom: 25%;" />
</center>
#### 암호화폐에서 리플레이 공격이 위함한 이유

하드포크가 진행되면, 원장 데이터는 하드 포크 이전 버전과 이후 버전으로 나누어지게 된다. 하드포크가 진행되어 체인이 A와 B로 나누어졌다고 가정하면 하드 포크 이후 생겨난 B체인에서 처리한 트랜잭션은 이론적으로 A체인에서도 유효하게 사용할 수 있다.

따라서 A와 B에 모두 계정이 있는 사용자는 B에서 트랜잭션을 발생시켰을 때, A체인에서 누군가가 해당 트랜잭션을 탈취해 브로드캐스팅하면 A체인에서도 해당 트랜잭션이 처리된다.



#### 리플레이 공격 대안

1. 세션 식별자 추가

   통신 당사자간 일회용 토큰을 해싱한 값을 공유하여 리플레이 어택을 피한다.

   1. 앨리스가 밥에게 일화용 토큰을 보낸다.
   2. 밥은 토큰을 암호화하여 앨리스에게 보낸다.
   3. 앨리스는 밥과 동일한 방식으로 토큰을 암호화하고, 그 값이 밥으로부터 받은 값과 같은 경우 통신을 진행한다.
   4. 공격자가 이 암호화된 값을 가로채고 다른 통신에서 사용하려고 해도, 앨리스가 밥에게 다른 일회용 토큰을 보내면 다른 암호화된 값이 나올것이기 때문에 공격자가 가로챈 값은 사용 불가하다.

2. 일회용 비밀번호

   아주 짧은 세션 시간을 가진 비밀번호를 두 통신 당사자가 공유하여 공격자가 가로채 재사용하지 못하도록 한다.

3. 타임 스탬프

   앨리스가 네트워크에 시간을 MAC와 함께 브로드캐스트한다. 밥은 앨리스에게 통신을 요청할 때 자신의 통신 메시지에 앨리스가 브로드캐스트한 시간을 기준으로 예상 시간을 포함해 인증을 진행한다. 앨리스는 타임 스탬프가 예상 시간 범위 내에 있는 메시지만 수락한다.



### 이클립스 공격

공격자가 네트워크상의 노드를 방해하기 위한 공격으로 정교한 공격을 준비하기 위해 네트워크에 혼란을 야기시킬 때 주로 사용한다.

이클립스 공격은 전체 네트워크를 공격하기보다는 특정 노드를 격리해 정직한 다른 노드로부터 정보를 수신받지 못하게 여러 악의적인 공격자 노드가 네트워크를 독점한다. 이 공격 노드들은 가짜 트랜잭션이 담긴 블록을 격리한 노드들에 브로드 캐스트하여 이중 지불 공격을 가능하여지도록 만든다.

#### 이클립스 동작 방식

공격자는 공격 대상의 이웃 노드들을 자신의 노드로 구성하여, 공격 대상 노드가 가짜 트랜잭션이 담긴 블록을 받도록 한다. 이를 통해 다음과 같은 공격 효과가 발생한다.

- 엔지니어링 블록 레이스(Engineering Block Races)

  블록 레이스는 채굴 노드들이 가장 먼저 유효한 논스 값을 찾아 블록을 생성하는 경쟁을 의미한다. 이클립스 공격에서는 이클립스 공격 대상 노드와 공격자의 노드가 동시에 블록을 생성한 경우, 공격 대상 노드가 생성한 블록을 숨김으로써 해당 블록은 고아 블록이 되고, 자신의 블록이 네트워크에 올라갈 수 있도록 한다.

- 채굴 파워 분할(Splitting Mining Power)

  공격자가 51% 공격하기 위해 네트워크의 전체 채굴 파워를 쪼갤 수 있다. 이러한 방식으로 공격자의 채굴 파워가 네트워크의 쪼개진 파워보다 커지게 되면 쉽게 51% 공격을 개시할 수 있다.

- N - 컨펌 이중 지불(N-Confirmation Double Spending)

  이클립스 공격자에 의해 여러 채굴 노드들이 공격 대상이 되어 격리된 경우, 공격자는 자신의 트랜잭션을 이클립스 공격대상인 채굴 노드에게 제공하여 블록체인에 추가하도록 한다. 이 노드들은 이후에도 블록을 계속 생성하면서 공격자의 트랜잭션이 든 블록이 컨펌되도록 한다.

  이클립스 공격 대상이 된 가게 주인은 트랜잭션이 들어있는 블록이 컨펌되는 것을 보고 물건을 제공한다. 이후, 공격자가 격리된 노드들이 만든 블록체인을 전체 네트워크에 공유하면, 해당 블록체인의 노드들은 고아 블록이 되면서 트랜잭션 자체가 취소되게 된다.

#### 이클립스 공격 대처 방법

- 무작위 노드 선택

  노드가 피어를 선택할 때 무작위가 아닌 경우, 공격자가 자신 주변의 노드를 공격 대상으로 선택할 수 있게 된다. 따라서 노드가 피어를 랜덤으로 선택하게 하여 공격자가 공격 대상 노드를 정하기 어렵게 만들 수 있다.

- 정보 저장

  노드가 다른 노드에 대한 정보를 기억하도록 하면, 해당 노드가 네트워크를 떠났다가 재접속 했을 때 이전에 연결했던 정직한 노드와 연결하여 정직한 피어 관계를 지속할 수 있다.

- 연결 수 늘리기

  하나의 노드에 연결된 피어의 개수를 늘리면, 노드가 정직한 노드에게 연결될 가능성이 커진다.

### 인적 문제로 발생할 수 있는 보안적 이슈

- 크립토재킹
- 더스팅 공격
- 시빌 공격

### 구현된 블록체인에서 생길 수 있는 보안적 이슈

- DAO 사건
- 패리티 멀티시그 지갑 동결 사건



### CAP 이론과 PACELC 이론
<center>
<img src="../../images/2022-10-04-blockchain_32th/image-20221004150921222.png" alt="image-20221004150921222" style="zoom:33%;" />
</center>
CAP 이론은 분산 데이터베이스 시스템을 바탕으로, 네트워크 분할 허용이 이루어지는 경우에 일관성, 가용성을 동시에 만족하는 것은 불가능하며, 일관성과 가용성 중 하나만 가질 수 있다는 이론이다.

CAP 이론에 따르면 모든 분산 네트워크는 일관성을 지키는 상황과 가용성을 지키는 상황으로 나눌 수 있다. 데이터를 업데이트하는 과정에서 다른 작업이 불가능하기 때문에 업데이트가 진행되는 시간에는 일시적으로 데이터베이스에 접속할 수 없어 서비스가 중지된다.

#### CAP요소

- 분할 허용 : 여러 개의 네트워크가 동작하고 있을 때 접속이 단절되어 서로 메시지를 주고 받지 못하더라도 서비스가 잘 동작해야 한다.
- 일관성 : 분산 시스템에서의 요청 및 응답 과정에서, 노드가 여러개 있더라도 마치 한 노드에서 실행되는 것처럼 동작해야한다.
- 가용성 : 분산 시스템이 지속해서 가용하기 위해서 장애 없는 노드에 수신된 모든 요청은 반드시 응답돼야 한다.

#### CAP의 상관관계

- CA : 일관성과 가용성을 충족하지만 분할 허용을 충족하지 못한다. 데이터에 대한 강한 신뢰를 부여할 수 있지만, 네트워크 문제가 시스템의 중단을 야기할 수 있다.
- CP : 일관성과 분할 허용을 충족하지만 가용성을 충족하지 못한다. 높은 확장성으로부터 성능을 확보할 수 있지만 일부 데이터가 비가용할 수 있다.
- AP : 가용성과 분할 허용을 충족하지만 일관성을 충족하지 못한다,. 부정확한 응답을 허용하는 고성능 시스템에 적합하다.

#### PACELC Theorem

CAP 이론에 따르지면 일관성과 가용성은 완전한 대립 관계에 있지만 사실 완벽한 CP 시스템과 AP 시스템은 쓸모가 없다. 그리고 완벽한 CA 시스템은 가질 수 없다.

- 완벽한 CP : 완벽한 일관성을 갖는 분산 시스템에서는 하나의 트랜잭션에 대한 복사본을 모든 노드가 가져야 한다. 시스템의 전체 성능은 네트워크에서 가장 낮은 성능의 노드에 종속되며, 만일 단 하나의 노드라도 문제가 발생하면 트랜잭션 처리는 실패한다.
- 완벽한 AP : 완벽한 가용성을 갖는 분산 시스템은 네트워크 분할로 인해 고립된 노드가 발생하더라도 서비스를 제공한다. 고립된 노드는 업데이트를 반영하지 못해 일관성이 결여된 잘못된 정보를 가지고 있지만, 완벽한 AP 시스템에서는 어찌됐건 가용한다. 사용자는 잘못된 정보를 받고 활용하게 된다.
- 완벽한 CA : 완벽한 CA 시스템을 위해선 절대로 장애가 발생하지 않는 네트워크를 구성해야 한다. 앞서 살펴봤든이 이는 불가능하다.

실제로는 일관성과 가용성의 절충안에 해당하는 연속적인 중간 영역이 존재한다. 이러한 중간 영역을 고려하고 네트워크의 정상 상황과 분할 상황을 모두 담아낼 수 있는 표현법으로 Daniel Abadi가 제시한 PACELC 이론이 있다.
<center>
<img src="../../images/2022-10-04-blockchain_32th/image-20221004154120614.png" alt="image-20221004154120614" style="zoom:50%;" />
</center>
PACELC은 분할이 발생했다면 가용성과 일관성 사이의 트레이드 오프가, 그렇지 않다면 지연시간과 일관성 사이의 트레이드 오프가 있음을 의미한다.

- 네트워크 분할 상황 : 분할 상황(P)에서는 단절된 노드에 접근할 수 없기 때문에 일관성을 포기하고 가용성을 제공할지(PA), 가용성을 포기하고 일관성을 유지할지(PC)의 정도를 결정해야한다.
- 네트워크 정상 상황 : 정상 상황(E)에서는 모든 노드에 업데이트를 반영해 일관성을 유지하기 위한 긴 대기 및 응답 시간을 가질지(EC), 일관성을 포기하고 짧은 지연시간을 가질지(EL)의 정도를 결정해야한다.


<center>
<img src="../../images/2022-10-04-blockchain_32th/image-20221004154426614.png" alt="image-20221004154426614" style="zoom: 33%;" />
</center>
블록체인에서 네트워크 분할은 분기라는 논리적 사건을 이유로 발생하기도 한다. 비슷한 시점에 같은 높이의 블록이 채굴되거나 새로운 원장이 제시될 경우 분기가 발생하고, 네트워크는 일시적인 분할 상황에 부딪힌다. 그러나 시간이 지남에 따라 포크 선택 규칙에 의해 하나로 합의하게 된다.

CAP 관점에서 보면 블록체인은 가용성과 분할 허용을 충족하는 AP 시스템이다. 그러나 통상의 AP 시스템은 고성능을 위하지만 블록체인 시스템은 자가 제한을 통해 성능을 제한한다는 점이 특이한 점이다. 대신 이를 통해 과거 블록의 위/변조를 어렵게 만들고 궁극적 일관성을 확보했다. 이러한 특징은 블록체인 트릴레마로 이어진다.

한편 PACELC 관점에서 보면 블록체인은 일관성보다는 가용성과 지연시간을 중시한 분산 시스템이다. 그러나 마찬가지로 시간이 지남에 따라 과거의 블록 및 트랜잭션에 대한 궁극적 일관성을 확보한다.

- 네트워크 분할 상황 : 분할 상황에서 블록체인은 일관성보다는 가용성에 초점을 둔다. 채굴자는 자신이 참조하고 있는 블록이 네트워크에서 아직 합의를 이루지못했다고 할지라도 이전 블록으로 삼아 채굴을 이어간다.
- 네트워크 정상 상황 : 정상 상황에서 블록체인은 일관성보다는 짧은 지연시간에 초점을 둔다. 블록체인에서는 채굴된 새 블록 혹은 더 무거운 체인 등을 통해 원장의 업데이트가 제안되는데, 모든 노드가 이를 따를 필요는 없다.

정리하자면 블록체인은 가용성과 지연시간을 중시하지만 충분한 완결성이 부여된 블록에 대해서는 높은 확률로 일관성을 보장하는 분산 시스템이다. 블록은 상태와도 같으므로, 현재 상태에 대해서는 가용성과 지연시간을 중시하고 과거 상태에 대해서는 일관성을 중시하는 분산 시스템이라고도 말할 수 있다.

### 샤딩(Sharding)

샤딩이란 하나의 거대한 데이터베이스나 네트워크 시스템을 여러 개의 작은 조각으로 나누어 분산 저장하여 관리하는 것을 말한다. 샤딩을 통해 나누어진 블록들의 구간(Epoch)을 샤드(Shard)라고 부른다.  
이는 단일의 데이터를 다수의 데이터베이스로 구간별로 쪼개어 나누는 걸 말하는데, 단일의 데이터베이스에서 저장하기 너무 클때 사용한다. 이를 통해 노드에 무겁게 가지고 있던 데이터를 빠르게 검증할 수 있어, 트랜잭션 속도를 향상 시킬 수 있다.
<center>
<img src="../../images/2022-10-04-blockchain_32th/image-20221004155627794.png" alt="image-20221004155627794" style="zoom:33%;" />
</center>
샤딩은 데이터베이스 저장기법 중 하나이며, 대용량의 데이터를 처리하기 위해 테이블을 수평 분할하여 데이터를 분산 저장하고 처리하는 것을 일컫는다. 블록체인에서는 전체 네트워크를 분할한 뒤 트랜잭션을 영역별로 저장한다. 그리고 이를 병렬적으로 처리하여 블록체인에 확장성을 부여하는 온체인 솔루션으로 데이터를 샤드라는 단위로 나눠서 저장 및 처리한다.

만약 10만큼의 데이터와 10명의 노드가 참여했다고 가정한다면 기존의 블록체인은 10명의 노드 개개인은 10만큼을 모두 가지고 있으면서 공유한다. 그러나 샤딩은 10을 조각내서 10명의 노드 개개인은 1만큼씩만 보관함으로써 보관 데이터가 가벼워져 거래처리 속도가 크게 향상된다.

#### 샤딩의 특징

샤딩은 관계형 데이터베이스에서 대량의 데이터를 처리하기 위해서 데이터를 파티셔닝하는 기술이다.  
파티셔닝은 DBMS에서 지원하기도 하는데, 일부 DBMS에서는 지원하지 않으며 DBMS 레벨에서 데이터를 나누는 것이 아니다.  
파티셔닝은 데이터베이스 자체를 분할하는 방식으로 애플리케이션 레벨에서 구현해야한다. 공개형 블록체인의 맥락에서, 네트워크에 올려진 트랜잭션은 네트워크상의 서로 다른 노드들로 이루어진 여러 샤드로 분할된다. 각각의 노드는 들어오는 트랜잭션들의 일부만을 처리할 수 있게 되고, 네트워크상에서 병렬식으로 다른 노드들에서도 똑같이 실행된다. 따라서 네트워크를 여러 샤드로 쪼개면 동시에 더 많은 트랜잭션을 처리하고 증명할 수 있다. 이 속성을 병렬식 확장이라고도 한다.

##### 수평 분할(Horizontal Partitioning)

스키마가 같은 데이터를 두 개 이상의 테이블에 나누어 저장하는 디자인을 말하고 가령 주민 데이터를 처리하기 위해 스키마가 같은 '서현동 주민 테이블'과 '정자동 주민 테이블'을 사용을 뜻하며, 인덱스의 크기를 줄이고, 작업 동시성을 늘리기 위한 것이지만 보통 수평 분할을 한다고 했을 때는 하나의 데이터베이스 안에서 이루어지는 경우를 지칭한다.

##### 샤딩의 장점

- 필요한 데이터만 빠르게 조회할 수 있기 떄문에 쿼리 자체가 가볍다
- 오래돼서 조회가 안되는 데이터를 클라우드에 올리거나 별도의 디스크에 저장해서 운영상의 스토리지 이득을 볼 수 있다.

##### 샤딩의 문제점

샤딩을 적용할 경우 한 샤드 내에서의 전송이 아닌 여러 샤드 간의 전송은 절차가 훨씬 복잡하고 느려진다. 여러 샤드로 쪼갤수록 인터샤드 트랜잭션은 확률적으로 많아지는데 각 샤드는 자기 샤드의 데이터만 있고, 다른 샤드의 데이터는 가지고 있지 않으므로 샤드 간 데이터를 어떻게 참조할 것인지, 어떻게 검증할 것인지 문제가 생겨서 알고리즘이 복잡해진다. 만약 이 단계에서 거래 결과가 뒤집어지면(비확정적합의) 상황은 더욱 복잡해지기 때문에 확정 합의가 거의 필수이다.

그리고 샤딩이 들어가게 되면 전체의 안정성은 보장이 된다하더라도 시간이 지나면 샤드 간 불균형이 일어나 일부 샤드의 안정성이 취약해지는 문제가 발생할 수 있다. 샤드마다 트랜잭션의 빈도, 노드의 수, 밸리데이터의 비율 등에서 차이가 나기 때문에 한 번 샤드가 정해진 다음에도, 샤드의 구성원을 재배치하여 샤드 간 균형을 맞추는 알고리즘이 필요하다. 그뿐만 아니라 예상했던 것보다 전체 트래픽이 높아질 경우, 처음 설정해둔 샤드의 수를 늘릴 필요가 있다. 한 번 쓰인 데이터를 해쉬나 서명으로 묶어 위변조나 조작하지 못하도록 만들어진 분산 원장 구조에서는 샤드를 중간에 추가하는 등의 동적 샤딩 기술을 구현하기가 매우 어렵다.

확장성의 문제를 해결방책으로 나온 샤딩에 중앙화의 문제와 보안성의 문제를 가지게 되는데 보안의 문제에는 100개의 샤드의 시스템에서는 오직 1%의 Hash Rate로 샤드를 지배할 수 있어 샤드간의 커뮤니케이션이 너무 빈번하게 일어난다면 커뮤니케이션으로 인한 시간 지연의 문제가 생기게 된다. 데이터 재분배로는 샤딩 된 DB의 물리적인 용량 한계나 성능 한계에 따라 샤드의 수를 늘리는 Scale-up 작업이 필요하며 서비스 정지없이 Scale-up 할 수 있도록 설계 방향을 잡아야 하며, Global Transaction을 사용하면 샤드 DB 간의 트랜잭션도 가능하여 XA임에도 성능 저하의 문제가 있다.

#### 데이터베이스를 나누는 방법

- Vertical Partitioning : 테이블별로 서버를 나누는 방식으로 구현이 간단하고, 전체 시스템에 큰 변화가 필요없다는 장점이 있고 단점으로는 각 서버의 데이터가 점점 거대해지면 추가 샤딩이 필요하다.
- Range Based Partitioning : 하나의 Feature가 점점 거대해지는 경우 서버를 분리하는 방식이며, 유저별로 서버를 분리하거나, 년도 별로 분리, 거래정보라면 우편번호를 이용하고 주의 사항으론 데이터를 나누는 방법이 예측할 수 있어야한다.
- Key or Hash Based Partitioning : 엔티티를 해쉬함수에 넣어서 나오는 값을 이용해서 서버를 정하는 방식으로 해쉬결과 데이터가 균등하게 분포되도록 해쉬 함수를 정하는 게 중요하며, 서버의 수를 늘리기 위해 해쉬 함수를 변경하는 작업이 정말 비싼 작업이라는 단점이 있다.
- Directory Based Partitioning : 파티셔닝 메커니즘을 제공하는 추상화된 서비스를 만드는 것으로 샤드 키를 look-up 할 수 있으면되므로, 구현은 DB와 CACM을 적절히 조합해서 만든다.

#### 샤딩 체인 동작 방식

- Proposer가 되고 싶은 네트워크 참여자는 SMC를 통해 Balance를 예치한다.

- Collator가 되고 싶은 네트워크 참여자는 SMC를 통해 Deposit을 예치한다.

- Collator들은 주기적으로 SMC Status를 확인해서, 자신이 Collator에 선정되었는지 여부를 확인한다.

- Collator들은 SMC에 의해 각 샤드 체인에 Pseudo-Random하게 배정되고, Look Ahead Period 동안에 해당 샤드의 이전 기록을 다운받으면 선택된 Proposal을 제안한 Proposer로부터 Proposal Bid를 받는다.

- Proposer는 트랜잭션을 담은 Proposal을 Collator에게 제출하는데, Proposal은 아직 검증되지 않은 Collation을 의미하며, 선택된 Proposal을 제출한 Proposer는 트랜잭션 발송자로부터 트랜잭션 Fee를 받는다.

- Collator들은 해당 Proposal에 속한 트랜잭션들이 Valid한지를 검증하는 투표를 한다.

  표에서 2/3이상의 Collator들이 Proposal에 포함된 트랜잭션이 Valid하다고 찬성할 경우, 해당 Proposal은 유효한 Collation이 된다.

##### 주요 용어

- Collation : 샤드 체인에서 메인 체인의 블록과 같은 역할을 하며, 크게 Collation Header와 트랜잭션 목록으로 구성된다.
- Collation Header : Collation을 구성하는 정보를 담고 있으며, Proposer의 Sign을 거쳐 메인 체인에 제출하고, 트랜잭션 목록은 Collation에 담긴  트랜잭션들의 목록이다.
- Proposer : 제안자라는 뜻으로 트랜잭션을 모아 Proposal을 만들고 Collator에게 제출하며, Proposal은 검증되지 않은 Collation이다.
- Collator : Proposer가 제출한 Proposal을 검증한다. Period마다 한 샤드에는 여러 Collator들이 배정되는데 이들은 해당 Period에 진입하기 일정 기간 이전에 무작위로 선정된다.
- Executor : Collation header를 메인체인의 SMC(Sharding Manager Contract)에 전달하고, 샤드 체인의 실제 State가 변경된다.
- Period : 메인 체인에서 샤드 체인의 Collation header를 제출받는 주기이며, 단위는 메인체인에선의 블록의 개수로 PERIOD_LENGTH = 5 라면 5개의 블록이 생성되는 것이 1 Period이다.
- Look Ahead Period : Collator는 샤드 체인에서 Collation을 검증하기 이전에 SMC에 의해 Pseudo-Random하게 배정되는데 'Look Ahead Period'는 Collator가 몇 Period에 앞서서 어떤 샤드 체인에 배정되는지를 나타내고, LOOKAHEAD_PERIODS = 4이면 4Period 이전에 Collator는 샤드 체인에 배정되므로 Collator는 사전에 자신이 배정된 샤드 체인의 State 정보를 다운받는 시간을 확보할 수 있다.
- Sharking Manager Contract(SMC) : SMC는 샤드 체인에서 가장 중요한 역할을 하는 스마트 컨트랙트로 SMC는 메인 체인과 샤드 체인을 연결하며, Collator, Proposer, Collation Tree 를 관리하며, 샤드 체인이 메인 체인에 참여하기 위해서는 필수적이다.

#### 이더리움 샤딩

이더리움 샤딩은 메인 체인이 처리해야 할 블록들을 조각내어 샤드(Shard)라고 불리는 오프 체인(Off-chain)에 할당하는데 오프 체인들은 주어진 조각에 대해서만 유혀성을 검증한다. 샤드들이 각자 할당된 조각들의 검증을 모두 끝내면 다시 묶어 이러한 개념을 통해 블록을 검증하는데 걸리는 시간을 단축한다.

샤드별로 Merkel Patricia Tree를 만들고 그 샤드의 Root들로 만들어진 Merkel Patricia Tree의 Root만을 블록체인에 올리는 것으로 모든 Miner가 모든 트랜잭션을 실행할 필요 없이 샤드별로 Miner를 분산시켜 실행할 수 있기 때문에 전체 실행 속도가 올라간다.

##### 이더리움 샤딩의 문제점

- 난수 생성 : 난수를 사용하여 검증자를 샤드에 배정하는데, 공격자가 난수를 예측하거나 조작할 수 있어, 샤딩 보안에 문제가 생긴다.
- 빠른 샤드 전환 : 샤드에 대한 공격 성공 가능성을 줄이려면 검증자를 빠르게 전환해야 하는데 이전부터 Look Ahead Time을 두어 검증자가 자신이 맡을 샤드블록를 미리 동기화시키고, 미리 동기화하기 위해서는 동기화할 자료를 줄여서 빠르게 검증자를 준비할 수 있는 Stateless Client를 제안한다. Stateless Client는 블록 헤더만을 저장하지만 블록헤더 만을 저장하기 때문에 거래에 대한 검증은 불가능하여 거래 검증하려면 거래를 만들 때, 검증에 필요한 Witness를 첨부해야 한다.
- 자료 가용성 : 모두가 Stateless Client라면 블록의 내용을 손실할 수 있기 때문에 누군가는 State를 저장하고 있도록 적절한 보상과 검증이 필요하다. Fisherman 딜레마는 Erasure Coding으로 해결했다.
- 검증자간 효율적인 통신 : 샤드 배정이 자주 바뀌는 상황에서 샤드 검증자들끼리의 효율적인 P2P 통신은 필수적이며 libs 2p의 Flood Sub과 Gossip Sub가 사용된다.
- 샤드 간 비동기 통신 : 거래 당사자나 스마트 계약이 여러 샤드에 나누어져 있다면 샤드 간의 통신(Cross-Shard Communication)이 필요하지만 여러 단계를 거치게 되어 시간이 오래 걸리므로 결국 메인 체인에 무리를 주게 되고 이렇게 샤드 간 통신이 너무 자주 일어난다면 샤딩의 장점은 사라진다. 이에 이더리움은 Cross Link를 가지고 메인체인의 무리를 덜고, Yanking으로 필요한 스마트 계약을 현재 샤드로 가져와 샤드 간의 통신을 줄이고자 현재 지연상태 전이(Delayed State Transition)를 통한 샤드 간의 비동기 통신도 구상 중이라고 한다.

