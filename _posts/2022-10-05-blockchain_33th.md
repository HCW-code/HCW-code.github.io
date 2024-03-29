---
layout: single
title: "[블록체인] DID"
categories: blockchain
tag: [did, ssi]
toc: true

---

### DID

Decentralized Identity(탈중앙 신원증명)는 **데이터의 주권이 개개에게 있고, 개개인의 데이터를 중앙화된 시스템을 거치지 않고 증명할 수 있는 기술**이다. DID는 **분산원장기술**(DLT)을 기반으로 사용자의 데이터를 저장하여 안전하고 편리하게 인증할 수 있도록 한다.

따라서 DID는 **데이터 저장소(Registry), 데이터 제공자(Provider), 인증기관(Certificate Authorities)**을 분리하고, 탈중앙화 방식으로 동작할 수 있도록 설계된다.

DID의 근간이 되는 개념은 SSI로 SSI의 개념을 탈중앙화 방식의 신원증명을 통해 구현한 것이 DID이다.

SSI(Self-Sovereign Identity) : 자기 자신이 신원 증명에 대한 권한을 갖고록 하는 개념

DID 구현의 가장 큰 걸림돌은 중앙화되지 않은 저장소에 개인의 신원을 증명할 수 있는 데이터를 보관하면서, 동시에 데이터의 무결성과 보안성을 확보하는 것이 어렵다는 것이었다.

그러나 블록체인 기술이 등장하고 대중화되면서 DID를 구현할 때 탈중앙화된 방식을 사용해 사용자의 신원 데이터를 저장하고 증명하는 방법을 모색하게 된다.

### W3C 표준화 - DIDs(탈중앙화 식별자)

DIDs는 마스터키를 활용하여 만들 수 있으며, 누구나 DID 메소드로 자신의 주소를 만들 수 있다.

#### DIDs 관련 개념과 용어에 대한 설명

- **Identity(식별자)**

  식별자는 개인 혹은 단체 등을 구별할 수 있는 고유값이다. 예) 이메일

- **DID 문서**

  DID 문서는 특정 DID를 어떻게 사용하는지에 관해 설명해 놓은 간단한 문서이다. 각 DID 문서는 암호학적 요소, 검증 메소드, 서비스 엔드포인트 등으로 표현될 수 있다. 즉, DID 식별자와 주체가 상호작용하기 위한 서비스 엔드포인트들을 포함한다.  
  DID 문서에서 가장 중요한 점은 DID 인증정보가 들어간다는 것이다. DID 인증정보는 해당 DID의 제어권과 소유권을 증명할 수 있는 공개키와 각종 메타데이터를 의미한다.

- **DID 메소드**

  DID 메소드는 특정 분산 원장 또는 네트워크에서 DID와 관련된 DID 문서들을 생성, 읽기, 갱신, 그리고 비활성화하는 메커니즘이다.

- **DID 형식**
  <center>
  <img src="../../images/2022-10-05-blockchain_33th/image-20221005133938886.png" alt="image-20221005133938886" style="zoom:50%;" />
  </center>
  - did : 문자열이 did이믈 나타내며, 이 주소가 did 스키마에 따른 것임을 나타낸다. 항상 did로 시작
  - example : did 메소드의 이름이고, did는 메소드별로 다르게 처리된다.
  - 123456789abcdefghi : DID 메소드 안에서 사용되는 고유 아이디이다.
  - did 아이디가 주는 가장 중요한 정보는 "DID 문서가 어디에 있는지" 이다.
  - ID와 관련된 정보는 did 문서에 담겨있다.

- **DID 문서 내용**
  <center>
  <img src="../../images/2022-10-05-blockchain_33th/image-20221005134206805.png" alt="image-20221005134206805" style="zoom:50%;" />
  </center>
  DID 문서 내용의 핵심적인 정보는 id의 제어권, 소유권 등을 증명할 수 있는 공개키와 인증정보이다.

  - id : 이 did 문서를 설명하고 있는 아이디이다.
  - 공개키 : 이 아이디와 관련된 공개키 리스트이다.
  - 인증정보 : 이 아이디의 소유권을 증명하기 위한 정보이다.
  - 서비스 : 이 아이디와 상호작용이 가능한 서비스들의 리스트이다.

  **중요한 것은 어떤 개인정보도 저장하지 않는다는 점이다.**

- **DID Registry**
  <center>
  <img src="../../images/2022-10-05-blockchain_33th/image-20221005134440241.png" alt="image-20221005134440241" style="zoom:50%;" />
  </center>
  만약 각 DID 메소드가 다르고, DID를 사용하는 블록체인 플랫폼이 모두 다른 상황에서 DID Document를 가져온다면 굉장히 복잡해진다. 이러한 문제점을 해결할 방법이 W3C 공식문서 DID Registry 파트에 담겨있다.

- **DIF 글로벌 조직**

  DIF는 전 세계의 사용자들이 DID를 더욱 쉽게 사용할 수 있도록 지원하기 위해 만든 조직이다. 주요 가입 회사로는 Sovrin, uport, Civic, MS, IBM, Master Card 등이 있다.

  DID 소유자가 Agent일때 DID로 Universal Resolver에서 DID Document를 뽑아낼 수 있다. DIF는 DID 표준을 만들며 DID를 활용하는 소프트웨어를 만드는 주요한 역할을 하고 있다.

- **DID 인증**

  DID 인증 절차

  - 회사에서 DID 소유권자에게 DID의 유무를 확인하기 위해 소유권자에게 challenge를 신청한다.
  - 소유자인 나는 회사에 응답으로 인증정보가 포함된 DID를 전달한다.
  - 회사는 응답받은 DID로 Universal Resolver에서 DID document를 가져온다.
  - DID document 안에 기록된 인증정보로 소유자에게 받았던 response를 검사하여 확인한다.
  <center>
  <img src="../../images/2022-10-05-blockchain_33th/image-20221005135036047.png" alt="image-20221005135036047" style="zoom: 33%;" />
  </center>
  위 그림과 같이 누군가의 신원을 검증하고자 할때, Universal Resolver에 있는 DID document에서 인증정보를 가져와 DID 소유자의 소유권을 확인할 수 있다.

  소유자가 제시한 DID와 Universal Resolver의 DID document 안에 기록된 정보를 서로 확인한다. 이를 통해 소유자가 제시한 정보의 진위여부를 확인하는 절차를 거친다.

### SSI

DID는 SSI를 탈중앙화된 방식으로 구현한 것이다.

SSI는 블록체인을 기반으로 자신을 증명할 수 있는 정보를 스스로 관리 및 보관하고, 신원 증명이 필요한 서비스를 이용할 때, 인증정보를 제3자에게 맡기는 것이 아닌 사용자가 직접 관리하도록 하여 데이터 주권을 사용자에게 돌려주는 기술 개념이다.

따라서 DID는 이러한 SSI의 개념을 탈중앙화된 방식으로 구현한, 자신의 개인정보를 선택적으로 제출할 수 있게 하는 **탈중앙화된 자기주권형 신원기술**이다.

SSI는 스스로가 독립적인 권한을 가진 신원, 다시 말해 '자신이 스스로 부여한 신원'이다. 신원의 소유권을 가진 주체가 신원에 대한 권리를 가지고 공개대상과 범위를 선택할 수 있는 개념이다.

#### 신원 관리 모델의 종류
<center>
<img src="../../images/2022-10-05-blockchain_33th/image-20221005163108743.png" alt="image-20221005163108743" style="zoom:33%;" />
</center>
- 1세대 개별 신원 모델(Siloed Identity)

  개별신원모델은 개별 서비스(인터파크, 11번가 등)마다 이용자의 아이디와 패스워드를 저장하고 신원확인 서비스를 제공하는 형태이다.

  개별 신원 모델은 서비스 제공자에게는 정보보호의무가 가중되며, 천문학적인 비용이 들고, 개인에게는 서로 다른 서비스의 정책에 따른 ID, Password를 관리해야하는 불편함을 야기시킨다.

  - 개인이 개별 사이트 ID, Password 관리해야함
  - 개별 서비스 제공자 정보보호의무 가중, 천문학적 비용 발생
  - 개인정보 유출 우려
  <center>
  <img src="../../images/2022-10-05-blockchain_33th/image-20221005163446890.png" alt="image-20221005163446890" style="zoom:33%;" />
  </center>
- 2세대 연합형 신원 모델(Federated Identity)

  연합형 신원 모델은 구글과 카카오 같은 연합신원을 제공하는 기업이 신원 확인 서비스를 제공하는 모델이다.

  신원관리 주체는 중앙화된 연결 서비스 제공자(구글, 카카오, 페이스북)이고 이용자는 스스로 선택한 신원관리 서비스 제공자를 통해 ID, Password을 관리할 수 있다. 신원관리 주체인 중앙화된 연결 서비스는 로그인(OpenID, Oauth)을 제공하고, 개인정보를 이용하고자 하는 다른 개별서비스(urclass 등)에 서비스를 제공한다.

  - 사용자의 편의성 제고
  - 글로벌 기업의 개인정보 독접적 확보
  - 사용자 개인정보에 대한 권리 주장 어려움
  - 개인정보가 독점되고 계속하여 유출 위험성 존재
  <center>
  <img src="../../images/2022-10-05-blockchain_33th/image-20221005163700476.png" alt="image-20221005163700476" style="zoom:33%;" />
  </center>
- 3세대 자기 주권 신원 모델(Self-Sovereign Identity)

  자기 주권 신원은 개인이 디지털 상의 신원 주권을 가지게 될때, 개인정보를자신 스스로 소유하는 개념이다.

  개인은 개인정보 발급 내역만 블록체인과 같은 분산원장에 기록하고, 특정한 상황에서 개인정보가 필요할 때 개인정보 발급자에게 개인의 신원을 증명할 신원 정보를 받아서 검증자(verifier)에게 신원 정보를 공유할 수 있는 모델이다.

  다만 자신의 데이터에 대한 주권을 가지게 된다는 것은 그만큼 데이터에 대한 책임과 의무가 강화될 수 밖에 없다. 가령, 비밀번호를 잃어버렸을 경우 복구가 불가능하다.

  **예시**

  1. 대학 졸업 증명서는 분산원장에 저장되어 있다. 대학(신원정보 발행자, Issuer)에 자신의 신원증명정보(DID)를 주고 대학 졸업 증명서(VC)를 받는다.
  2. 대학(Issuer)은 김블록에게 받은 신원증명정보와 분산원장에 저장되어 있는 대학졸업증명서의 소유자의 정보가 일치하는지를 확인한다.
  3. 일치할 경우, 김블록에게 대학졸업증명서를 발급한다.
  4. 김블록이 입사를 희망하는 회사(Verifier)에게 졸업증명서(VP)를 제공하고, 졸업증명서의 소유자임을 증명하는 정보도 함께 제공한다.
  5. 김블록이 입사하는 회사는 김블록이 제공한 졸업증명서가 김블록의 소유가 맍는지, 분산원장에 저장된 정보를 가지고 검증한다. 이렇게 하여 김블록은 대학졸업증명서를 제출하고, 그에 따른 진위여부를 판별받게 된다.

  - 신원이 분산 관리되어 이전세대의 신원관리모델보다 가용성과 무결성이 높음
  - 통합된 분산원장 관리가 가능하다면 확장성이 더 높음
  - 신원확인 정보를 블록체인에 공유하여 신원확인이 필요한 서비스를 활용할 때 사용
  - 비밀번호를 잃어버렸을 경우, 다시 찾기 어려움
  <center>
  <img src="../../images/2022-10-05-blockchain_33th/image-20221005164331324.png" alt="image-20221005164331324" style="zoom:50%;" />
  </center>




#### SSI 요소

SSI를 구성하는 4가지 개념

- DIDs(탈중앙화 식별자)

  DIDs는 검증가능하고 탈중앙화된 디지털 신원을 위한 새로운 형식의 식별자이다. 누구나 DID 메소드로 자신의 주소를 만들 수 있으며, DID는 주소이면서 마스터키를 활용하여 만들 수 있다.

- DID Auth

  DID 소유자가 개인키를 가지고 있다는 것을 간단히 인증할 방법을 다룬다.

- DKMS(탈중앙 키 관리 시스템)

  신원을 증명하는 데 사용하는 개인키를 어떻게 관리할 것인가를 다룬다.

- Verifiable Credentials(검증가능한 크레덴셜)

  아이디의 소유자가 어떤 것을 할 수 있는 자격을 갖추었음을 검증하는 방법을 다룬다.

#### SSI를 구현하기 위한 요소
<center>
<img src="../../images/2022-10-05-blockchain_33th/image-20221005165528857.png" alt="image-20221005165528857" style="zoom:40%;" />
</center>
1. Issuer(발행자) : 발행자

   Issuer는 신원 정보를 발급하는 주체이다. Verifiable Credential(검증가능한 크리덴셜, 이하 VC)을 발행하는 주체이며, 정보 주체의 요구에 의해 신원정보와 DID를 발급하는 기관이다. 발행자는 발급한 정보에 대해 신뢰할 수 있는 신원정보를 전달한다.

2. Holder(소유자) : 자격증명 소유자

   Holder는 신원 정보를 소유한 주체이다. 즉, 정보 주체로 DID를 활용하여 본인의 신원을 증명하고자 하는 사용자이다. 시스템에서는 DID를 발급 받고, 제출한다.

3. Verifier(검증자) : 자격증명 검증자

   Verifier는 신원정보를 검증하는 주체이다. 정보 주체인 Holder로부터 Verifiable Presentation(검증가능한 프레젠테이션, 이하 VP)을 받아 신원정보를 검증하는 주체이다.

   DID로 신원을 확인한 후 검증자는 이 신원 정보가 발급기관인 Issuer가 발급한 유효한 신원정보인지, 검증데이터 저장소를 통해 검증한다.

4. Verifiable Data Registry(검증데이터 저장소) : 블록체인 등 분산 저장소

   정보 주체의 식별자와 Issuer의 인증서, 신원증명 해지내역, 신원 증명 스미카 등이 등록된 분산원장 기반의 데이터 무결성이 확보된 저장소이다. Verifiable Data Registry(검증데이터 저장소)는 반드시 블록체인일 필요는 없으며, Holder, Issuer, Verifier가 합의한 분산원장이면 사용할 수 있다.

### Verifiable Credential(검증가능한 크리덴셜)

Credential은 신원 확인에 필요한 정보이다.

물리적 Credential로는 주민등록, 운전면허, 여권 등으로 신원을 주장하는데 디지털 세계에서는 사용할 수 없기 때문에 이러한 문제를 해결하고자 ㄴ온 표준이 W3C의 Verifiable Credentials Data Model이다.

자기주권 신원(SSI)체계에서는 디지털 세계에서 개인의 신원을 증명할 수 있는 체계를 검증가능한 크리덴셜이라 한다. 검증가능한 크리덴셜의 목적은 디지털 세계에서의 크리덴셜을 통해 물리적 세계의 신분증과 동일한 정보를 제공하는 것이다.

#### VC 구성요소

- 클레임(Claim)

  디지털 세계에서 신원정보는 데이터로 표현할 수 있으며, 각 단위 데이터를 Claim이라고 하며, 아래와 같이 주체-속성:값의 구조를 가진다.

  예를 들어 A라는 주체(Subject)의 이름으라는 속성(Property)은 김블록이라는 값(Value)을 가진다. 라는 문장이 하나의 Claim이 된다.
  <center>
  <img src="../../images/2022-10-05-blockchain_33th/image-20221005170910854.png" alt="image-20221005170910854" style="zoom:33%;" />
  </center>
  Claim은 다른 Claim과 결합하여 아래와 같은 연결정보(Graph of Information)를 생성할 수 있다.
  아래의 도식을 해석하면, 'Pat은 Example 대학의 졸업생입니다.'라는 정보를 확인할 수 있다. 또 'Sam의 직업은 교수이다.'라는 Claim에 'Pat은 Sam을 알고 있다'는 정보를 추가하면 'Example 대학교 졸업생인 Pat은 교수인 Sam을 알고 있다.'는 연결 정보를 도출할 수 있게 된다.
  <center>
  <img src="../../images/2022-10-05-blockchain_33th/image-20221005172426288.png" alt="image-20221005172426288" style="zoom:33%;" />
  </center>
- W3C 문서의 Credential

  DID체계에서는 Credential을 주체에 대한 하나 혹은 그 이상의 Claim으로 구성된 데이터의 집합이라고 정의할 수 있다.

  예를 들어 주민등록증의 신원 정보를 확인하여 생각해볼 수 있다.

  - 이름
  - 주민등록번호
  - 주소
  - 발급 일자
  - 발급 주체

  등이 담겨있고 이 각각의 신원정보가 클레임이다. 이러한 클레임들이 모여 크리덴셜이 된다.



#### VC

탈중앙 신원체계에서는 단순히 Credential이 아닌 검증가능한 Credential이라고 표현한다. Verifiable Credential(검증가능한 크레덴셜)은 아래와 같은 구조를 띤다.
<center>
<img src="../../images/2022-10-05-blockchain_33th/image-20221005171450233.png" alt="image-20221005171450233" style="zoom:33%;" />
</center>
- Credential Metadata : Credential을 해석할 수 있도록 설명해주는 메타데이터
- Claim(s): 주체에 대한 Claim 집합
- Proofs : Credential을 검증가능하도록 만드는 암호학적 요소들이 포함된 증명

이러한 기록은 분산원장 플랫폼을 기반으로 한다. 따라서 분산원장 상에 기록된 각 주체의 전자 서명을 확인하면서, 궁극적으로 개인이 제시하고 있는 신원정보가 발급된 사실과 다르지 않다는 것을 검증할 수 있도록 한다.
<center>
<img src="../../images/2022-10-05-blockchain_33th/image-20221005171951215.png" alt="image-20221005171951215" style="zoom:50%;" />
</center>
Verifiable Crendential 그래프

- Claim으로 정보를 확인하고, Digital Proof를 통해 검증
- Issuer와 Holder의 Digital Signature(전자 서명) 포함
- 발급 내역이 Data Registry에 쓰이며, 취소된 Credential인지 아닌지 확인
- 제대로 된 포맷인지 Schema 검증

**이를 통해 검증가능한 크레덴셜은 적합한 발급자인지 확인하기 위해 다음의 4가지를 확인한다.**

- Issuer가 발급한 DID인지 진위여부
- Holder의 DID인지 진위여부
- 블록체인의 발급내역이 유효, 무효 여부
- Schema 확인을 통해 형식이 맞는지를 확인

### Verifiable Presentation(검증가능한 프레젠테이션)

SSi의 핵심은 프라이버시 보호이다. 주민등록증을 VC로 만든다면, 주민등록증의 모든 Claim들이 VC에 포함되어 있을 것이다.

그런데 특정 상황에서 모든 정보를 제공해아 하는 경우는 거의 없다.

이때 자기 주권 신원에서는 최소한의 정보공개를 원칙으로 하여 증명이 필요한 정보들로만 구성된 새로운 형식이 필요하다. 그것이 바로 VP이다.
<center>
<img src="../../images/2022-10-05-blockchain_33th/image-20221005172836005.png" alt="image-20221005172836005" style="zoom:33%;" />
</center>
편의점에서 맥주 한캔을 구매한다고 가정하고 VP를 통해 선택적으로 나이만 공개한다면 19세 이상이라는 사실여부만 선택적으로 공개할 수 있게 된다.
<center>
<img src="../../images/2022-10-05-blockchain_33th/image-20221005172937682.png" alt="image-20221005172937682" style="zoom:50%;" />
</center>
### Ecosystem of Verifiable Credential(검증가능한 크리덴셜 생태계)

하나 이상의 VC를 발급하고, 스마트폰 앱의 디지털 지갑의 VC를 저장한다. Verifier에게 증명하기 위해 VC 중 필요한 정보를 VP로 구성한다. 검증자에게 VP로 검증한다.
<center>
<img src="../../images/2022-10-05-blockchain_33th/image-20221005173310995.png" alt="image-20221005173310995" style="zoom:50%;" />
</center>
#### 자기 신원 인증 과정

Issuer

- Issuer는 Holder에 대한 검증 가능한 크리덴셜(VC)을 발급하여 전달한다.
- VC의 유효성을 확인할 수 있는 ID와 Schema의 발급 내역을 블록체인에 기록한다.

Holder

- Issuer에게 VC를 받고 자신이 증명서를 받았다는 내용과 스키마 정보를 가져온다.
- Verifier가 필요로 하는 정보를 담아 VP 형태로 보낸다.

Verifier

- Verifier는 VP내용과 블록체인에서 내용을 확인한다.
  - 블록체인
    - 발급 내역
    - Schema
  - VP
    - Issuer DID
    - Holder DID
- 위의 내용들을 검증하여 VP 내용의 사실 여부를 검증한다.

#### DID 기술을 활용한 입사 지원 시나리오
<center>
<img src="../../images/2022-10-05-blockchain_33th/image-20221005173925355.png" alt="image-20221005173925355" style="zoom:50%;" />
</center>
1. 입사지원자(holder)는 대학교(Issuer)에 본인의 졸업 정보(ex, 학위번호, 학위명, 수여 일자 등)를 요청한다.
2. 대학교(Issuer)는 요청정보를 확인하고 문제가 없다고 판단되면 Digital Signature(전자서명) 후 입사지원자(holder)에게 졸업증명서(Verifiable Credential)를 발행한다.
3. 이때, 대학교(Issuer)의 DID 정보가 졸업증명서(Verifiable Credential)에 함께 저장된다.
4. 입사지원자(Holder)는 인증서를 모바일 전자지갑에 보관하며, 입사 지원 시 인증서에 Digital Signature(전자서명)하여 지원기업(Verifier)에 제출한다.
5. 지원기업(Verifier)은 입사지원자(Holder)와 대학교(Issuer)의 DID를 통해 블록체인에 저장된 Digital Signature(전자서명) 검증정보를 전달받아 졸업증명서(Verifiable Credential)의 졸업정보를 확인한다.





### DID를 활용한 졸업증명서 개발

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity 0.8.10;

abstract contract OwnerHelper {
    address private owner;

  	event OwnerTransferPropose(address indexed _from, address indexed _to);

  	modifier onlyOwner {
		require(msg.sender == owner);
		_;
  	}

  	constructor() {
		owner = msg.sender;
  	}

  	function transferOwnership(address _to) onlyOwner public {
        require(_to != owner);
        require(_to != address(0x0));
    	owner = _to;
    	emit OwnerTransferPropose(owner, _to);
  	}
}

abstract contract IssuerHelper is OwnerHelper {
    mapping(address => bool) public issuers;

    event AddIssuer(address indexed _issuer);
    event DelIssuer(address indexed _issuer);

    modifier onlyIssuer {
        require(isIssuer(msg.sender) == true);
        _;
    }

    constructor() {
        issuers[msg.sender] = true;
    }

    function isIssuer(address _addr) public view returns (bool) {
        return issuers[_addr];
    }

    function addIssuer(address _addr) onlyOwner public returns (bool) {
        require(issuers[_addr] == false);
        issuers[_addr] = true;
        emit AddIssuer(_addr);
        return true;
    }

    function delIssuer(address _addr) onlyOwner public returns (bool) {
        require(issuers[_addr] == true);
        issuers[_addr] = false;
        emit DelIssuer(_addr);
        return true;
    }
}

contract CredentialBox is IssuerHelper {
    uint256 private idCount;
    mapping(uint8 => string) private alumniEnum;
    mapping(uint8 => string) private statusEnum;

    struct Credential{
        uint256 id;
        address issuer;
        uint8 alumniType;
        uint8 statusType;
        string value;
        uint256 createDate;
    }

    mapping(address => Credential) private credentials;

    constructor() {
        idCount = 1;
        alumniEnum[0] = "SEB";
        alumniEnum[1] = "BEB";
        alumniEnum[2] = "AIB";
    }

    function claimCredential(address _alumniAddress, uint8 _alumniType, string calldata _value) onlyIssuer public returns(bool){
        Credential storage credential = credentials[_alumniAddress];
        require(credential.id == 0);
        credential.id = idCount;
        credential.issuer = msg.sender;
        credential.alumniType = _alumniType;
        credential.statusType = 0;
        credential.value = _value;
        credential.createDate = block.timestamp;

        idCount += 1;

        return true;
    }

    function getCredential(address _alumniAddress) public view returns (Credential memory){
        return credentials[_alumniAddress];
    }

    function addAlumniType(uint8 _type, string calldata _value) onlyIssuer public returns (bool) {
        require(bytes(alumniEnum[_type]).length == 0);
        alumniEnum[_type] = _value;
        return true;
    }

    function getAlumniType(uint8 _type) public view returns (string memory) {
        return alumniEnum[_type];
    }

    function addStatusType(uint8 _type, string calldata _value) onlyIssuer public returns (bool){
        require(bytes(statusEnum[_type]).length == 0);
        statusEnum[_type] = _value;
        return true;
    }

    function getStatusType(uint8 _type) public view returns (string memory) {
        return statusEnum[_type];
    }

    function changeStatus(address _alumni, uint8 _type) onlyIssuer public returns (bool) {
        require(credentials[_alumni].id != 0);
        require(bytes(statusEnum[_type]).length != 0);
        credentials[_alumni].statusType = _type;
        return true;
    }

}
```

