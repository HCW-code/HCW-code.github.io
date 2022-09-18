---
layout: single
title: "[블록체인] 채굴 Mining"
categories: blockchain
tag: [채굴, mining]
toc: true

---

## 채굴(Mining)

**블록체인 네트워크에 노드로 트랜잭션을 검증하여 분산원장을 기록하고, 보상으로 암호화폐를 얻는 것**을 뜻한다.

새로운 블록을 만드는 것이 바로 채굴의 핵심이며 특정 컴퓨터 연산 작업을 통해 만들어지게 된다.  
비트코인의 경우, 10분에 한번씩 일정량의 블록이 생성되는 이 생성된 비트코인을 채굴에 참여한 작업자 중 해시 퍼즐이라는 문제를 푼 작업자에게 지급하게 되며, 이 해시퍼즐은 특정한 조건을 갖춘 해시를 찾아내는 일련의 과정을 말한다.  
블록체인 기반의 암호화폐에서 새로운 블록을 생성하고 그 대가로 암호화폐를 지급받는 노드들이 바로 **채굴자(Miner)**이다
<center>
<img src="../../images/2022-09-07-blockchain_19th/image-20220907142259715.png" alt="image-20220907142259715" style="zoom:50%;" />
</center>
토큰 이코노미와 크립토 이코노미의 생태계를 통해 채굴자들은 이익을 위해서 채굴을 한다는 것을 알 수 있다.

### 채굴자가 하는 일

노드(Node)가 비트코인 네트워크에 접속하면, 비트코인 채굴자는 다음과 같이 몇 가지 작업을 수행한다.

- 네트워크 동기화 : 새 노드가 비트코인 네트워크에 합류하면, 다른 노드에게 과거의 블록들을 요청해 블록체인을 다운로드한다.
- 트랜잭션 검증 : 새로운 트랜잭션을 수신한 노드는 반드시 해당 트랜잭션이 올바른 트랜잭션인지 검증하는 과정이 필요하다.

**비트코인에서 트랜잭션 검증하는 단계**

1) 원본 데이터를 자신의 개인키로 암호화를 진행하여 디지털 서명을 진행
2) 원본 데이터와 디지털 서명된 데이터를 노드에 전파
3) 트랜잭션을 받은 노드는 해당 트랜잭션이 진짜인지에 대한 검증을 위해 트랜잭션을 송신한 노드의 공개키를 이용하여 복호화 진행
4) 난독화된 거래 데이터와 원본 데이터를 비교하여 수정된 데이터가 있는지 데이터의 무결성을 검증
5) 수신받은 트랜잭션이 진짜 거래로 판단될 경우 블록체인에 해당 트랜잭션을 업데이트하고 블록체인 네트워크에 연결된 노드들에게 해당 트랜잭션을 다시 전파

- 블록의 유효성 검사 : 채굴자와 풀 노드는 특정 규칙에 따라 수신한 블록을 평가하여 유효성 검사를 시작한다.
- 새로운 블록 생성 : 채굴자는 네트워크에 브로드캐스팅된 트랜잭션의 유효성을 검사한다.
- 작업 증명(PoW) 수행 : 채굴 과정의 핵심으로 채굴자가 해시 퍼즐을 풀어 유효한 블록을 찾는다. 이때, 블록 헤더에 있는 논스(Nonce)를 사용하여 채굴자는 논스값을 계속 바꿔가며 결과 해시값이 미리 결정된 목표값보다 작을 때까지 반복 계산한다.

**블록 헤더에 있는 논스(Nonce)와 트랜잭션의 논스(Nonce)의 차이**

블록 헤더에 있는 논스는 입력값 중의 하나로 해서 계산되는 블록의 해시값이 특정 숫자보다 작아지게 하는 값으로 쓰인다.  
이더리움에서 트랜잭션의 논스(Nonce)는 발신 주소의 속성이며, 발신 주소의 컨텍스 안에서만 의미를 갖는다.  
그러나 논스는 명시적으로 블록체인 계정 상태에 저장되지 않고 해당 주소에서 발생한 확인된 트랜잭션 건수를 세어서 동적으로 계산되는 값으로 쓰인다.

- 보상 수령 : 해시 퍼즐(PoW)의 해를 구한 노드는 즉시 결과를 브로드캐스팅하고, 다른 노드들은 그 결과를 검증하여 그 블록을 승인한다.  
  승인되면 채굴자는 비트코인과 관련된 트랜잭션 수수료를 보상으로 받는다.

#### 이더리움 채굴

네트워크의 채굴 노드는 이더해시(Ethash)라는 독자적인 작업증명 알고리즘을 사용해 블록을 생성하고자 경쟁한다.  
이더해시 알고리즘에 대한 입력은 논스라고 하는 임의로 생성된 숫자를 포함하는 블록 헤더이며 그 출력은 32바이트의 16진수이다.  
논스를 수정하면 출력도 수정되는데 예측할 수 없는 방식으로 수정된다.  
네트워크가 채굴된 블록을 수용하려면 블록 헤더에 대한 이더해시 출력이 네트워크 난이도보다 적어야 하며 또 다른 32바이트의 16진수가 채워질 대상으로 사용되며 목표 난이도를 상회하는 블록을 브로드캐스트하는 모든 채굴자는 블록 보상을 받게 된다.

### 보상

해시 퍼즐(PoW의)의 해를 구한 노드는 즉시 결과를 브로드캐스팅하고, 다른 노드들은 그 결과를 검증하여 블록을 승인한다.  
블록이 승인되면, 채굴자는 비트코인과 관련된 트랜잭션 수수료를 보상으로 받는다.  
비트코인의 작업증명(PoW) 해를 구하는 시간으로 10분이 소요되도록 알고리즘이 형성되어 있기 때문에, 더 많은 채굴자가 등장하고, 빨리 채굴할수록 채굴 난이도가 상승하게 되어있다.  
이 보상은 일정량을 지속해서 보상하는 것이 아니라, 반감기로 인하여 2009년 초반에는 블록 하나를 생성할 때마다 50개의 비트코인을 보상으로 받을 수 있었고 2018년에는 12.5개의 비트코인을 받을 수 있는 등 시간이 지나면 지날수록 블록 보상에도 변화가 생긴다.  
이에 따라 비트코인의 총공급량은 약 2100만개가 되며, 그에 따른 희소 가치가 부각될 것이다.

#### 거래 수수료

블록 보상 난이도가 어려워지고 반감기로 인해 수령하는 코인의 개수가 줄어들어도 채굴자들은 거래 수수료라는 이익이 있다.

거래 수수료란, 채굴자들이 특정 거래 기록들을 블록에 포함해서 블록체인에 추가할 수 있도록 제공되는 인센티브이다.  
거래 수수료는 블록체인 네트워크와 관련하여 몇 가지 중요한 목적을 갖고 있다.

그중 하나가 바로 **트랜잭션을 승인하는 데 도움을 제공**하거나 **스팸 공격으로부터 네트워크를 보호**하는 데 일조한 **채굴자와 검증자**에게 보상으로 지급하는 것이다.

대부분의 암호화폐는 두 가지 중요한 이유에서 트랜잭션 수수료를 사용한다.

- 네트워크 상의 스팸 공격을 줄이기 위해

  거래 수수료는 대규모 스팸 공격과 이를 실행하는 데 무척 많은 비용이 들도록 한다.

- 거래 수수료는 트랜잭션을 확인하고 유효성을 검증하는 사용자에게 인센티브를 제공

  이를 네트워크에 일조하는 행동에 대한 보상이라 이해할 수 있다.

대부분의 블록체인에서 트랜잭션 수수료는 합리적인 수준으로 저렴하지만, 네트워크 트래픽에 따라 비싸질수 있다. 얼마의 수수료를 지불하기로 결정하느냐에 따라 우리의 트랜잭션이 다음 블록에 추가되는 우선순위가 정해진다.

#### 해시율(Hashrate)

해시율은 기본적으로 초당 해시 계산 개수 비율을 나타낸다. 다른 표현으로는, 블록을 찾기 위해 비트코인 네트워크상의 채굴자들이 해시를 계산하는 속도이다.  
비트코인 초기에 이 값은 개인의 CPU 자원이 사용되었기에 꽤 낮았다. 그러나, 전문 마이닝풀과 Application Specific Integrated Circuits(ASICs)가 도입되며, 해시율은 기하급수적으로 증가하였다. 이 결과 비트코인 난이도도 급격하게 증가하였다.

아래 그래프는 초당 Tershashes 변화를 보여준다. 150m Terahashes/s는 15,000,000,000,000,000,000 개의 해시값이 초마다 계산됨을 의미한다.
<center>
<img src="../../images/2022-09-07-blockchain_19th/image-20220907160220048.png" alt="image-20220907160220048" style="zoom: 33%;" />
</center>
**TPS(Transaction per Second)**

실제로 이더리움, 비트코인을 전송해보면 몇 시간이 걸리기도 하고, 높은 수수료까지 지불해야한다. 그래서 확장성 문제를 해결하고자 많은 프로젝트가 치열한 경쟁을 하고 있다.  
TPS란 1초당 처리할 수 있는 트랜잭션의 개수를 의미한다.

원장이 분산화되고, 참여노드가 증가할수록 TPS는 느려지고, 수수료는 증가한다.

### 채굴 풀(Mining Pool)

채굴 풀은 채굴하는 채굴자들이 모여서 만들어진 채굴자 조합이다.

#### 채굴 풀이 생긴 이유

채굴자들이 모이게된 이유는 비트코인 채굴 원리에서 찾을 수 있다.

비트코인은 알고리즘을 해결하고, 거래장부에 블록을 생성하게 되면, 보상으로 비트코인을 받는 방식으로 채굴된다.  
A와 B라는 채굴자가 있을 경우 해시파워가 높은 쪽이 먼저 작업을 수행하고 비트코인을 보상으로 받게 된다.

**해시파워(Hash Power)**란, 블록체인 네트워크에서 채굴자들이 가지고 있는 채굴 역량을 뜻한다.  
쉽게 말해, 10해시 파워와 20해시 파워가 있다면 10대의 PC와 20대의 PC가 경쟁한다고 생각하면 된다.

그런데 여기에서 15해시파워를 갖고 있는 C 가 A를 돕는다면 해시파워가 25인 A와 C가 B보다 먼저 블록을 생성하게 된다.

이렇게 생성된 블록으로 지급받은 비트코인은 두 채굴자가 일정 비율로 나눠야하지만 아예 채굴을 못하는 것보단 이렇게 힘을 합치는게 더 나을 것이다.

이러한 개념에서 발생한 것이 바로 채굴자 집단인 채굴 풀이다.
<center>
<img src="../../images/2022-09-07-blockchain_19th/image-20220907162908071.png" alt="image-20220907162908071" style="zoom: 33%;" />
</center>
#### 채굴 풀 종류

비트코인 채굴 풀 중 하나인 BTC.com의 홈페이지를 보면 각 채굴 풀의 해시레이트를 확인할 수 있다. 우리나라 사람이 만든 채굴조합에는 마이닝 풀 허브가 있다.

해시레이트 : 연산 처리능력을 측정하는 단위로 해시 속도를 의미한다.
<center>
<img src="../../images/2022-09-07-blockchain_19th/image-20220907163319358.png" alt="image-20220907163319358" style="zoom: 33%;" />
</center>
#### 채굴 풀의 위험성

채굴 풀이 존재함으로 51% 공격으로 인해 네트워크에 영향을 끼치는 위험성이 있을 수 있다.  
51% 공격이란, 블록체인의 전체 노드 중 50%를 초과하는 해시파워를 확보한 뒤, 거래 정보를 조작함으로 써 이익을 얻으려는 해킹 공격을 뜻한다. 이 경우 이중 지불 공격을 성공할 수 있으며, 합의에 영향을 미치고 실제로 비트코인 네트워크에 다른 버전의 거래 내역을 강요할 수 있게 된다.

이러한 사건은 비트코인의 역사에서 딱 한번 발생했는데, 대형 채굴 풀인 지해시가 51%이상의 네트워크 점유를 확보했다가 지해시에 해싱파워를 제공했던 개인들이 해당 채굴풀에서 빠져나오면서 문제는 일단락되었다. 후에 이를 해결하기 위해 지분증명(PoS)방식이 생겨난다.

#### 새로운 채굴 풀 모델

**커스터디 서비스 형태의 채굴 풀**

거버넌스 블록체인의 채굴 풀의 경우, 우리가 알고 있는 일반 채굴 풀과는 다른 형태이다.

본래 커스터디(Custody)란, 보호, 관리라는 뜻으로 금융거래에 있어 수탁업무를 말하며 다른 사람의 자산 관리를 위탁받는것을 말한다. 결국 남의 코인을 위임받아서 운용하는 서비스, 자산운용이다.

전통의 지분 증명(PoS) 서비스를 이용하려면 특정 노드가 자산으로 **스테이킹**해서 운영하게 된다. 그런데 그 자산이 어느정도 이상 있어야 많은 돈을 받을 수 있는 구조라 돈이 적은 사람은 상대적으로 취약할 수 밖에 없는 방식으로 생각할 수 있다.

스테이킹 : 자신이 보유하고 있는 가상화폐중 일정 지분량을 고정하는 것으로, 가상 화폐의 보유자는 가격의 등락과 상관없이 가상 화폐를 예치하고 예치 기간 일정 수준의 이익을 얻을 수 있다.

그래서 채굴 풀이란걸 이용해서 돈이 적은 사람도 PoS 채굴풀에 합류해서 함께 파이를 나눠서 이익을 얻고, 사용자들은 돈만 제공해주고 노드는 채굴풀이 돌리니 보상에서 일정 수수료를 제외하고 자신이 받아가는 형태의 새로운 채굴풀이 등장하게 된다. 이런 형태의 채굴 풀이 한 단계 성장한 방식이 위임지분 증명(DPoS)방식을 사용하는 채굴 풀인데, 이것은 사용자가 시스템에 스테이킹을 해두고 투표를 통해 채굴자(노드)를 선정하는 시스템이 된다.

#### 채굴의 문제점

수천, 수만 대 컴퓨터를 24시간 내내 가동하고 열기를 식히기 위한 냉방까지 필요한 가상 화폐 채굴이 전기 요금이 싼 저개발 국가를 중심으로 만연하면서 전력소모량이 크게 늘었다. 그리고 이로 인해 거래마다 평균 이산화탄소 300kg 을 생산한다고 비판받고 있다.
<center>
<img src="../../images/2022-09-07-blockchain_19th/image-20220907165601278.png" alt="image-20220907165601278" style="zoom: 33%;" />
</center>
### 채굴 시스템

#### CPU

CPU 채굴은 오리지널 비트코인 클라이언트에서 사용할 수 있었던 첫 번째 타입의 방식이다. 현 시점에서 CPU 채굴은 더 이상 이익이 되지 않으며 ASIC 기반의 방식과 같은 더욱 발전된 방법이 사용된다. CPU 채굴은 비트코인이 탄생하고 1년정도 채굴자들 사이에서 사용된 후 다른 방법으로 대체되었다.

#### GPU

비트코인 네트워크의 난이도가 증가하고 점점 더 빠르게 채굴하는 방법을 찾으며, 채굴자들은 GPU나 그래픽 카드를 사용해 채굴을 수행하였다.  
GPU는 보통 OpenCL언어를 사용하여 프로그램된 빠르고 병렬적인 계산을 제공한다. GPU는 성능면에서 CPU보다 매우 우수하여 사용자들은 Overclocking과 같은 기술을 사용해서 GPU Power를 최대치로 누릴 수 있도록 하였다.  
또한 병렬적으로 여러 그래픽 카드를 사용할 수 있다는 점이 더욱 비트코인 채굴에 그래픽 카드를 사용하는 원동력이 되었다.  
그러나 GPU 채굴은 특별한 Motherboards를 요구하고, 여러 그래픽 카드를 수용하기 위해 추가적인 하드웨어가 필요하다거나 Overheating 된다거나 하는 제약들이 존재하였다. 그리고 게이머나 그래픽 소프트웨어 사용자의 수요도 존재했기에 가격이 비쌌다.

#### FPGA

GPU 채굴이 얼마 지나지도 않아서 채굴자들은 Field Programmable Gate Arrays(FPGAs)를 사용해 채구하는 또 다른 방법을 찾아냈다.  
FPGA는 기본적으로 특정 연산을 수행하도록 프로그래밍 가능한 집적회로이다. FPGAs는 보통 Verilog나 VHDL과 같은 Hardware Description Languages(HDLs)에 프로그램되어 있다.  
Double SHA256은 빠르게 FPGA 프로그래머들에게 매력적인 작업이 되었고 몇 개의 오픈소스 프로젝트도 시작하였다.  
FPGA는 GPU와 비교해 더욱 뛰어난 성능을 제공한다. 그러나 접근성, 프로그래밍 난이도, FPGA를 설정하고 프로그래밍하기 위해 특별한 지식을 요구하는 부분 등으로 인해 널리 이용되지는 못하였다.

이후 ASICs의 도입은 FPGA 기반 시스템을 빠르게 사라지게 했다. GPU채굴은 여전히 며몇 코인 채굴에 있어서는 이익이 나지만, 비트코인의 난이도는 너무 높아서 오직 병렬로 실행되는 ASICs로만 적절한 이익을 얻을 수 있다.

#### ASICs

ASICs는 SHA256 연산을 수행하기 위해 디자인되었다. 이 특별한 칩은 다양한 제조사에서 판매되며 매우 높은 해시율을 제공한다. 어떤 경우에는 이익을 내며 잘 수행되나, 채굴 난이도가 급격히 올라가며 싱글-유닛 ASICs는 더 이상 이익이 나질 않는다.

현재 이익이 발생하는 채굴 플랫폼을 만들기 위해서는 막대한 양의 에너지와 자금이 필요하기 때문에 개인이 진입하기는 매우 어렵다.  
오늘날에는 전문적인 채굴 센터가 수천개의 병렬 ASIC 유닛을 사용자에게 채굴계약 형태로 제공해주고 있다.  
기술적인 제약이 거의 없어서 단일한 사용자가 수천 개의 ASICs를 병렬로 실행할 수 있으나 채굴만 하는 데이터 센터와 하드웨어가 필요하기에 일반 개인이 지불하기에는 매우 큰 비용이 든다.