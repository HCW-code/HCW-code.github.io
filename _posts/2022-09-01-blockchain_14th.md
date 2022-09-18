---
layout: single
title: "[블록체인] 트릴레마 해소방안 연구"
categories: blockchain
tag: [blockchain, trilemma]
toc: true
---

## 트릴레마 해소방안 연구

### 유망한 솔루션

비트코인과 이더리움 상에서 확장성은 블록체인의 한계로 보인다.

이 문제에 대해서 대표적으로는 비트코인 캐시가 블록의 크기를 증가시켜 비트코인의 확장성을 높이려 했다.

비트코인은 기존 블록체인 레이어 위에 레이어를 추가해 확장성 문제를 해결하려 한다. 이 아이디어는 레이어 2 솔루션이 여러 트랜잭션을 함께 묶고 때때로 기본 레이어 블록체인을 쿼리한다는 것에서 기인하였다.

이더리움은 샤딩이 기본 레이어 블록체인을 확장하는 다소 하이브리드적인 접근 방식을 취하고 있으며 커뮤니티는 다른 레이어 2 솔루션이 처리량을 더 늘릴 것으로 기대하고 있다.

확장성의 관점에서 블록체인 데이터의 처리 과정에서 노드의 역할을 나눌 수 있는데, 특정 노드들에게만 블록 생성의 역할을 맡기고 다른 노드들은 데이터 생성에만 참여하도록 할 수 있다. 이렇게 중앙화와 탈중앙화 사이에 대치적으로 노드들의 역할을 나눔으로써 확장성을 높일 수 있다.

하지만 특정 소수 노드에게 너무 많은 역할이 배분되면 탈중앙화의 의미가 퇴색된다.

실제로 비트코인의 채굴 노드를 보면 소수 노드에 해시파워가 집중되는 경향을 보이며, PoS(Proof of Stake)를 채택하고 있는 블록체인(NEO 등)들도 지금까지 자본의 집중화를 통해 만들어지는 합의 권력의 집중화를 해결하지 못하고 있다.
<center>
<img src="../../images/2022-09-01-blockchain_14th/image-20220901165244474.png" alt="image-20220901165244474" style="zoom:40%;" />
</center>
또한 On-Chain과 Off-Chain의 결합을 통해 탈중앙화를 유지하면서도 확장성 문제 해결을 시도하는 경우라도 Off-Chain의 소수 노드가 관리하는 블록체인 원본 데이터 속성을 고려해 볼 때, 보안성 관점에서의 데이터 보안 취약, Off-Chain 노드들에게 발생할 수 있는 해킹 공격 등 취약점이 나타날 수 있다.

물론 반대로 많은 노드가 모든 정보를 가지고 있는 경우를 상정하면, 탈중앙화는 강화될 수 있으나, 확장성의 취약성과 보안의 또 다른 관점인 체인 분기와 같은 다른 종류의 취약점이 부각될 수 있다.

이처럼 트릴레마는 탈중앙화를 선택함으로써 발생하는 기회비용이 중앙화를 통해 얻을 수 있는 편익과 동일함으로써 발생하는 문제점이다.

탈중앙화와 안전성에 초점을 맞춘 비트코인과 이더리움 같은 경우 사용자 수가 아주 많은 지금에 와서는 트랜잭션 처리 속도가 매우 느려서 문제가 되고 있다. 아이러니하게도 블록체인이 확장성 문제를 해결하는 데 있어서 가장 큰 두 가지 걸림돌이 바로 탈중앙화와 보안이다.

차세대 블록체인이라 명명한 3세대 블록체인들이 이런 문제점을 해결하기 위해 나타나고 있지만 처리속도를 올려 확장성 문제를 해결했을 경우 탈중앙화나 보안에서 문제점이 발생하고 있다.

### 알트코인

알트코인은 대안(Alternative)과 화폐(Coin)의 합성어로, 비트코인을 개량한 암호화폐 전체를 의미한다. 비트코인은 프로그램 소스 코드를 공개하는 오픈소스이기 때문에 , 이를 참고해 새로운 암호화폐를 누구라도 개발할 수 있다. 전 세계에 알트코인의 종류는 2만개가 넘으며 대부분은 블록체인 기술로 작동한다.  
알트코인은 비트코인의 문제를 해결하기 위해, 비트코인을 하드포크하거나 제네시스 블록에서부터 새롭게 시작하여 만들어진다.

#### 비트코인 캐시
<center>
<img src="../../images/2022-09-01-blockchain_14th/image-20220901170249331.png" alt="image-20220901170249331" style="zoom:40%;" />
</center>
비트코인의 트랜잭션 속도가 느려지는 이유는 시간에 흐름에 따라 일정한 간격으로 생성되는 블록의 크기와 그 블록에 담을 수 있는 거래내역들이 한정되어 있기 때문이다.

비트코인에서 체인분기(하드포크)된 비트코인 캐시는 블록의 크기를 기존 것에 비해 2~8배까지 확장하는 방법으로 트랜잭션 속도를 올렸다. 비트코인 캐시는 기존에 비트코인이 가지고 있는 탈중앙화 구조를 유지하고 10분이라는 블록생성 주기를 조정하지 않은 상태에서 트랜잭션 속도를 올릴 수 있는 효율적인 방법이였다.

##### 비트코인과 비트코인 캐시의 차이점
<center>
<img src="../../images/2022-09-01-blockchain_14th/image-20220901170704750.png" alt="image-20220901170704750" style="zoom:50%;" />
</center>
##### 비트코인 캐시의 문제점

###### **제한된 확장성**

기존 구조를 거의 변경하지 않았다는 점에서 그 확장성의 효과는 제한적일 수 밖에 없다. 블록체인에 참여하는 노드의 수가 증가하고 앞으로 더 많은 트랜잭션들이 나타나게 되면 거래처리 속도는 지금의 지연상태와 같이 수시간 또는 수일동안 거래가 처리되지 않을 가능성이 높다.

###### 자원의 중앙화

비트코인과 체인이 분기된 알트코인 비트코인 캐시는 비교적 탈중앙 구조를 유지하고 있지만 블록을 생성하는 채굴 노드의 중앙화는 탈중앙 요소를 위협하는 새로운 문제로 제기되고 있다.  블록생성에 가치를 부여하고 해커들의 시도를 무력화하기 위한 PoW(Proof of Work)알고리즘이 자본의 집중으로 인한 채굴권력을 분산시키지 못한다는 점이다. 자본의 특성상 새로운 수익을 내기 위해서 자본은 집중화 되는 특성을 갖고 있다. 이러한 현상이 비트코인과 일부 알트코인 채굴에서 나타나고 있다.

비트코인의 채굴 알고리즘은 PoW로 채굴에 성공하기 위해서는 보통의 컴퓨터가 10분이라는 시간에 풀 수 있는 정도의 난이도를 가진 수학문제를 풀도록 되어 있다. 누군가 많은 컴퓨팅 자원으로 해당문제를 더 빨리 풀게 되면 인센티브인 코인을 소유할 수 있게 된다.

그렇다보니 컴퓨팅 자원을 누가 더 많이 확보하느냐에 따라 확률적으로 인센티브를 가져갈 확률이 올라가게 된다. 더 많은 컴퓨팅 자원을 확보하기 위해 컴퓨팅 자원의 농장화(Farm)가 나타났고 이것을 중심으로 더 많은 자본이 모이게 되었다. 이 농장을 운영하는 주체가 영향을 갖게 되었고 이들이 연합하여 채굴하지 않겠다고 선언하면 블록체인 네트워크는 심각한 손상을 초래할 수 있다. 만약 채굴농장(Mining Farm)이 전체 블록체인 채굴 컴퓨팅 파워의 51%이상을 가지게 되면 모든 정보의 소유권을 갖게 된다. 악의적인 공격행위와 해킹을 시도하면 모든 정보를 임의로 변경할 수 있게되는 것이다.
<center>
<img src="../../images/2022-09-01-blockchain_14th/image-20220901172024651.png" alt="image-20220901172024651" style="zoom:40%;" />
</center>
비트코인 캐시의 경우 블록의 사이즈를 늘려 부분적으로 거래처리 속도를 올릴 수 있었지만 블록을 채굴하는 해시파워의 50%이상을 주요 4대 채굴농장들이 점유하고 있다. 따라서 이런 형태는 탈중앙화의 형태로 보기 어렵고 특정 세력에 의해 전체 네트워크 운명을 달리 할 수 있다.

건전한 블로게인 생태계를 만들기 위해서는 자본과 수익지향 중심적인 인간의 욕망을 제어할 수 있는 기재가 블록체인 생태계 시스템에 반영되어 있어야한다. 달리 표현하면 관리가 필요하다. 불특정 다수가 암호경제적 관점에서 자발적으로 제어되는 블록체인의 특성외에도 선택과 유인, 그리고 큐레이션으로 탈중앙화된 가치를 유지시키기 위한 행위가 요구되는 것이다.

### 오프체인

#### 라이트닝 네트워크

라이트닝 네트워크는 양방향 채널이라는 아이디어를 기반으로 매우 저렴한 비용으로 거의 즉각적인 거래가 가능한 비트코인 레이어(또는 레벨) 2의 솔루션이다. 기본 블록체인과 마찬가지로 P2P 교환을 갖추고있지만 자금 관리를 위임하지 않은 채널 네트워크에서도 돈을 교환할 수 있다. 거래는 다른 모든 사람의 잔액에 대한 인증 역할을 하는 첫 번째와 마지막을 제외하고는 오프체인이다.

라이트닝 네트워크는 기존 비트코인의 느린 처리 속도를 해결하고 빠른 속도를 구현하기 위해 개별 거래를 별도의 채널(Off-Chain)에서 처리한 후 그 결과만 블록체인에 기록하는 방식으로 작동하는 알고리즘이다.  
라이트닝 네트워크는 탈중앙화와 보안을 기본으로 두고 확장성을 높이기 위한 작업으로,  개별 노드 간에 일상적으로 반복되는 소액 거래 내역을 처리할 수 있도록 메인 블록체인 외부에 별도 채널을 구축한 오프체인 솔루션이다. 여기서 거래된 내용은 모든 노드의 승인을 받지 않고 계약 당사자들끼리 합의를 통해 확정되고 블록체인에 저장되지도 않는다. 반복적인 거래가 모두 끝나고 오프체인을 닫을 때 비로소 최종 거래내역만 블록체인에 저장된다. 승인 과정이 간단하고 반복적인 소액 거래가 블록체인에 저장되지 않으니 당연히 처리 속도는 빨라진다.

그러나 오프체인 시스템 또한 탈중앙화 문제를 완벽하게 해결하지 못한다. 우선 블록체인 기술이 아니며 제 3자 세력이 필요하기 때문에 확장성 진영에서 이러한 시스템을 좋게 보지 않는다.

라이트닝 네트워크에는 이미 비트코인뿐만 아니라 비트코인의 DNA를 반을 보유하고 있는 퀀텀(Qtum) 역시 라이트닝 네트워크에 참여하고 있다. 사실상 비트코인과 DNA가 같으면 라이트닝 네트워크를 사용하는데 큰 지장에 없기 때문에 라이트닝 네트워크가 활발해지면, 비트코인의 확장성이 많이 개선될 것이다.

이러 방식으로 비트코인은 잠재적으로 확장성 요구 사항에 대한 솔루션을 찾았고 수백만은 아니더라도 수천에 이르는 TPS에 도달할 가능성이 있다.  
Joseph Poon과 Thaddeus Dryjark 2016년 비트코인 라이트닝 네트워크: 확장 가능한 오프체인 즉시 지불이라는 논문과 함께 제안한 솔루션은 유명한 블록체인 트릴레마를 해결하기 위한 마지막 부분을 추가하였다.

### 플랫폼

#### 카르다노

카르다노(에이다)는 3세대 블록체인으로 지분 증명 메인넷 중 가장 탈중앙화가 잘 이루어진 메인넷이다. 블록체인 트릴레마의 해결을 위해 거래와 연산을 구분하는 2개의 레이어를 사용해 스마트 컨트랙트 사용에 따른 트랜잭션 체증을 방지하였다. 또한 우로보로스 지분증명(Ouroboros PoS)이라는 합의 알고리즘을 사용해 지분 증명의 예상되는 공격들을 사전에 방지하여 안전성을 높였다. 그러나 카르다노는 스마트 컨트랙트 도입에서 어려움을 겪고 있다. 카르다노는 수년간의 개발을 통한 알론조 업그레이드로 네트워크에 스마트 컨트랙트를 도입하였으나 **동시성** 이슈로 인해서 스마트 컨트랙트 도입시의 확장성의 문제가 대두되고 있다. 이에 따라 현재 출시된 선데이스왑 등의 디앱에서 트랜잭션이 몰리면 처리 속도가 급격히 늦어지는 문제점이 발견되어 해결책이 필요한 상황이다.

동시성 : 동시성은 두개의 작업이 동시에 발생하는 경우를 일컫는다. 두 개 이상의 프로그램이나 작업을 동시에 비동기적으로 실행할 수 있고, 그 두 작업 모두 최종 결과에 영향을 주지 않는다.

카르다노는 UTxO 기반인 eUTxO 모델로 구동한다.  
eUTxO 모델은 자금을 주고받을 때 미사용 거래 금액(UTxO)으로 저장되고, 수행 시 각각 한번만 사용할 수 있다. 또한 카르다노의 스마트 계약은 UTxO를 저장하고 해당 스마트 계약에 저장된 UTxO를 사용할 수 있는 방법을 제어하는 특정 조건이 프로그래밍되어 있다. 이는, 한 블록당 한 사람만 상호 작용이 가능하다는 것을 뜻한다.

이것을 카르다노의 동시성 문제라고 칭한다.

#### 알고랜드

알고랜드(Algorand)는 블록체인의 트릴레마를 해결하기 위한 플랫폼을 위한 암호화폐이다. 알고랜드의 창시자이자 튜링상(Turing awarad)의 수상자이며 영지식증명(ZKP)의 권위자인 실비오 미칼리(Silvio Micali)는 알고랜드가 무허가형 순수지분증명(PPoS) 합의 알고리즘을 통해 블록체인이 트릴레마를 해결할 수 있다고 밝혔다. 순수지분 방식은 두 단계로 진행된다.  
첫 번째 단계에서는 알고랜드 네트워크의 블록 생성자가 토큰 보유자 중에서 무작위로 한명을 선정하고  
두번째 단계에서는 다시 무작위로 뽑힌 1천명이 1단계에서 선정된 위원이 생성한 블록을 검증한다.  
실비오 미칼리 교수는 "블록체인에서 어려운 것은 다음 블록을 생성하는 것"이라고 했는데, 이는 단순히 체인을 만들기는 쉬우나 누가 다음 블록을 선택할 것인가에 따라서 거래의 유용성과 효율성이 달라지기 때문이다. 알고랜드는 이에 다음 세가지 솔루션을 제시하였다.

- 순수지분증명(Pure Proof of Stake) : 모든 토큰에 할당된 권리는 같으며, 누구나 블록 생성에 참여할 수 있다. 또한 체인의 개념에서 이슈가 되는 포크(fork)가 일어날 수 없다.
- 즉각적인 제시와 합의(Immediate Propose & Agree) : 한 명의 사용자만이 블록을 생성하는 것이 아닌 전체가 블록을 선택하고 생성한다. 이 과정은 빠르고 정교하게 발생한다.
- 진화하는 합의(Consensual Evolvability) : 알고랜드의 합의는 99.9% 바로 이루어진다. 시스템을 개선해야할 때도 공정한 과정을 통해 진행되며, 토큰 알고리즘과 통화 정책도 마찬가지다.

##### 알고랜드의 트릴레마 대안

블록체인의 보안과 탈중앙화에 영향을 미치지 않고 확장성을 보장하려면 우선 신속한 트랜잭션을 필요로 하는 전 세계적인 수요를 해결해야 한다. 새로운 데이터를 추가하고 네트워크 내에서 공유하며 유효성을 검증하는 모든 과정이 빠르게 처리되어야 한다는 뜻이다.

현재 시점을 기준으로 세상에 1초당 최소 1000건의 트랜잭션을 처리할 수 있는 초당 트랜잭션 처리(TPS) 성능을 가준 원장이 필요하다. 이상적으로는 평균 16000 TPS를 기록하며 40000TPS 까지 도달할 수 있는 신용카드와 경쟁해야 한다. 그러나 중앙집중화된 주체가 운영하는 신용카드와 달리 블록체인의 목표는 트랜잭션을 처리할 뿐만 아니라 공유, 게시, 검증 가능한 상태까지 유지하는 것이다.

확장성이 뛰어난 블록체인 솔루션으로는 위임형 지분증명(DPOS)을 꼽을 수 있다. 이 경우 선별을 통해 정해진 검증자 그룹이 새 블록 추가를 처리한다. 중앙집중식 기관보다는 민주적인 접근법이지만, 탈중앙화의 관점에서 이것으로는 부족하다.

알고랜드는 **임의성**을 통해 블록체인 삼중고를 해결한다.

알고랜드는 새 트랜잭션을 추가하는 작업을 수행하는 검증자에 초점을 맞춘다. 블록체인의 주요 목표는 분산화 수준을 유지하고 확장성을 허용하는 방식으로 검증자에게 블록 검증을 위탁하는 것이어야 한다.

알고리즘은 모든 토큰 보유자 중에서 검증자를 임의로 선택하여 검증작업을 수행하고 네트워크는 다음 노드 그룹을 자동으로 선정하는 알고리즘을 활용해 블록을 추가하도록 한다. 이 접근 방식을 통하면 모든 사용자가 시스템에서 선택받을 수 있으므로 분산성이 유지되며, 다음 검증자가 누구일지 아무도 모른다는 사실은 보안을 보장해주게 된다.

임의성은 목표로 하는 분산화 수준을 달성하고 네트워크가 51% 공격에 당하지 않도록 예방해주는 강력한 도구이다.

알고랜드 네트워크를 손상하는 유일한 방법은 토큰 보유자중 자기 파괴적인 행동을 하는 보유자가 과반수를 차지하는 것뿐이다. 하지만 토큰의 가치를 잃고자 하는 보유자는 없으므로 실질적으로 불가능하다.

유일한 문제는 무작위 선택을 보장하기 위해 신뢰할 수 있는 시스템이나 주체가 있는지이다. 알고랜드에서 가장 중요한 요소도 여기에 있다. 알고랜드는 새로운 순수 지분 증명(PPoS) 컨센서스 알고리즘을 선택하여 삼중고를 해결하였기 때문이다.

##### 시스템의 작동 방식

본질적으로 토큰 보유자는 무작위로 자신을 선택한다. 악성 행위자가 검증 위원회의 일원이 되기 위해 계속해서 자기 자신을 검증자로 선정할수 있다.

여기서 주의할 점은, 창시자인 미칼리는 모든 토큰 보유자가 자기만의 추첨을 실행한다고 하였다. 즉, 슬롯머신의 레버를 한번만 당기는 것과 같다. 그러니 추첨 결과는 당첨과 탈락 중 하나로 결정된다.

추첨에서 당첨되면 알고랜드의 검증 위원회 1000명의 토큰 보유자중 한명이 된다. 미칼리는 이것이 암호화된 추첨이라고 설명하였다.

국가 전체에 비견될 정도로 강력하고 놀라운 컴퓨팅 파워를 갖춰도 토큰 중 하나가 추첨에서 당첨될 확률을 개선할 수는 없다.

따라서 모든 사람이 레버를 당겨 추첨에 참여하지만, 다음 블록의 검증이 가능한 것은 1000명의 당첨자 뿐이다. 1마이크로 초만에 추첨이 이루어진다는 점을 고려한다면 이러한 추첨 시스템은 확장성까지 갖추었다고 볼 수 있다.