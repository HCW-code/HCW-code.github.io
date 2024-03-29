---
layout: single
title: "[블록체인] 다양한 지갑"
categories: blockchain
tag: [지갑, Wallet]
toc: true

---

### 핫 월렛 & 콜드 월렛

- 핫 월렛 : 온라인
- 콜드 월렛 : 오프라인

이 둘을 구분하는 기준은 인터넷 연결 유무이다.

#### 핫 월렛(Hot Wallet)

세상에는 수많은 핫 월렛이 존재하고, 월렛마다 지원하는 코인, 토큰의 수가 다르다.

핫월렛 또는 온라인 지갑은 인터넷 주소가 네트웤에 연결되어 있어 온라인 상태에서 실시간으로 거래 정보를 주고 받을 수 있다는 장점이 있다.  
하지만 개인키가 온라인에 노출되기에 해킹 등 보안 문제에 취약하다는 단점이 있다.

대표적으로 웹 월렛, 데스크탑 월렛, 모바일 월렛이 있다.

이더리움 플로그인인 메타마스크, 클레이튼의 카이카스, 클립 역시 핫월렛의 일종이다.

#### 콜드 월렛(Cold Wallet)

콜드 월렛은 지갑의 개인 키를 오프라인으로 보관하는 지갑을 의미한다.

콜드 월렛은 오프라인이기 때문에 보안 측면에서 안전하다는 장점이 있다. 하지만 인터넷이 차단되어 있기에 실시간 거래가 불가능해 불편하다는 단점이 있다.

대표적으로 페이퍼 월렛, 하드웨어 월렛이 있다.

### 스마트 컨트랙트 월렛

스마트 컨트랙트를 이용하는 월렛을 스마트 컨트랙트 월렛이라고 부른다.

일반적으로 이더리움에서 사용자는 EOA로 자신의 자산을 관리한다.  
EOA는 기능이 제한적인데, 코드(스마트 컨트랙트)를 담을 수 없기 때문이다.

반면 CA를 사용해 자산을 관리하는 경우, CA에 있는 컨트랙트 코드를 이용해 누가 어떤 조건에서 자산에 접근할 수 있는지를 프로그래밍화 할 수 있다.

스마트 컨트랙트 월렛은 개인 키가 아닌 스마트 컨트랙트로 관리하기 때문에, 기존의 단일 키를 사용하는 EOA 기반 월렛보다 더 높은 수준의 보안, 유연성, 편의성을 제공한다. 사용자는 스마트 컨트랙트 코드를 사용해

- 멀티 시그 트랜잭션
- 일일 송금 제한
- 긴급 계정 동결
- 안전한 계정 복구

등의 고급 기능을 사용할 수 있을 뿐더러 다른 dApp과도 상호작용 할 수 있다.

#### 특징

- 2단계 인증

  인증 앱 또는 기본 지갑 솔루션을 통해 추가 보안 기능을 제공한다.

- ATM과 같은 인출 제한

  트랜잭션 금액 제한을 설정할 수 있다. 이는 사용자가 잘못 판단하여 높은 금액의 인출 가능성을 줄이고 공격자가 한 트랜잭션에서 지갑의 모든 금액을 가져가는 것을 방지할 수 있다.

- 화이트리스트 및 블랙리스트

  사용자는 자신이 지정한 주소(화이트리스트)로만 전송할 수 있고, 차단한 주소(블랙리스트)에는 전송을 제한한다.

- 사기 경보 및 긴급 잠금

  장치를 분실하거나 도난 당한 경우 계정을 잠그거나 손상된 장치에서 계정에 대한 액세스를 비활성화할 수 있다.

#### 웹 월렛

웹 월렛은 웹 기반으로 호스팅되는 지갑으로 사용자가 계정을 생성하고 보관할수 있다.  
항상 인터넷에 노출되어 있어 보안에 가장 취약하지만, 즉시 거래가 가능하다는 측면에서 가장 실용적이다.

#### 모바일 월렛

모바일 월렛은 데스크톱 & 웹 지갑의 모바일 형태이다.

인터넷 접속 여부에 따라 위에서 다룬 핫 or 콜드 월렛으로 작동할 수 있다.

스마트폰 앱으로 다운받아 사용할 수 있으며, 역시 언제 어디서나 거래가 가능하다는 점에서 편리하다.

#### 하드웨어 월렛

하드웨어 월렛은 거래에 서명할 때 개인 키를 인터넷에 노출하지 않기 때문에 온라인 상태에서 자산에 액세스하는 가장 안전한 방법이다.

#### 멀티시그 월렛

멀티 시그 월렛은 멀티시그를 통해서만 송금이 가능하다는 특징이 있다.

기존의 핫 월렛과 콜드 월렛은 하나의 개인 키를 사용하기 때문에 이 단일 키가 노출될 경우 탈취자가 해당 개인 키에 연결된 자산에 쉽게 접근할 수 있다는 단점이 있다. 이러한 단점을 보완하기 위한 것이 멀티 시그 월렛이다.

멀티 시그 월렛은 하나의 지갑에 N명의 사용자가 지갑에 대한 소유 권한을 갖고, 해당 지갑에서 트랜잭션을 만들기 위해서는 N명중 k명이 트랜잭션에 서명해야 한다. 멀티 시그 월렛은 일반 지갑에 비해 보안이 우수하다는 장점이 있으며, 실수로 송금이 일어나는 경우를 방지할 수도 있다.

그러나 컬티 시그 월렛은 스마트 컨트랙트 상에서 구현되기 때문에 사용성이 부족하다.  
가령 대부분의 암호화폐 거래소에서는 일반 지갑 간에 이루어진 트랜잭션만 처리하기 때문에 멀티 시그 월렛에서 일어난 트랜잭션을 인식하지 못하기도 한다.

또한 멀티 시그 월렛은 스마트 컨트랙트 상에서 구현되기 때문에 컨트랙트 코드의 오류로 인해 문제가 발생할 수 있다. 2017년 멀티 시그 월렛을 사용하는 패리티(Parity)에서는 스마트 컨트랙트 버그를 이용한 해킹 사례가 있었다.

멀티 시그 월렛에는 Consensus, Gnosis, Argent, BitGo 등이 있다.

### 비결정적 월렛 & 결정적 월렛

#### 비결정적 월렛

비결정적 월렛은 매번 비밀 키를 무작위로 생성하는 방식의 지갑이다.  
매 트랜잭션마다 새로운 주소를 위한 새로운 지갑 파일을 만들어야 한다는 특징이 있다.  
기본적으로 암호화폐를 사용할 때는 개인 정보 보호를 위해 암호화폐 주소를 재사용하는 것은 바람직하지 않다.

하지만 이렇게 매번 무작위로 비밀 키를 생성하다 보면 문제가 생길 수 있다.  
실수로 지갑 데이터를 분실하는 경우, 해당 비밀키에 저장된 코인과 해당 비밀키로 생성한 스마트 컨트랙트에 접근하지 못하게 된다.  
이는 지갑 데이터를 자주 백업해야 한다는 관리의 측면에서 불편함이 있다.

#### 결정적(시드) 월렛

이러한 비결정적 월렛의 불편함을 해결하는 방식의 지갑이 바로 결정적 월렛이다.  
결정적 지갑은 하나의 시드에서 하나의 시드 키를 가지고 있으며, 이 시드 키는 비밀 키를 만들기 위한 난수이다.

- 이를 니모닉 코드 단어(mnemonic code words)라고 한다.  
  비밀 키는 시드 키를 인덱스 또는 다른 데이터와 결합하여 만든다.  
  이 시드 키는 자신으로부터 만들어진 비밀 키를 복구할 수 있다.  
  이러한 특징 때문에 시드 키로부터 만들어지는 모든 비밀키는 그 값이 미리 정해져 있다고 볼 수 있다.  
  따라서 시드 키를 이용한 지갑 방식을 결정적 지갑이라고 한다. 결정적 지갑을 사용하면 하나의 시드 키만 알고 있어도 시드 키에서 파생된 모든 비밀 키를 알 수 있기 때문에 모든 비밀 키를 관리할 필요 없이, 시드 키 하나만을 관리하면 된다.

결정적 지갑의 대표적인 예시

##### HD 월렛
<center>
<img src="../../images/2022-08-29-blockchain_11th/image-20220829172200520.png" alt="image-20220829172200520" style="zoom: 40%;" />
</center>
HD Wallet은 Hierarchical Deterministic Wallet(계층적 결정적 지갑)의 약자로, 하나의 시드(Seed) 값만 가지고 있으면 여러 개의 주소를 쉽게 생성할 수 있는 암호화폐 지갑이다.

쉽게 설명하자면, 증권사에서 필요에 따라 계좌를 여러 개 쓰는 것과 동일하다.

여러 개의 키를 관리할 때 하나로 관리하면 되기 때문에 하나의 키로 다목적 관리를 할 수 있다는 장점이 있다.

Hierarchical은 하나에서 다른 하나를 유도하는 것, Deterministic은 트리구조가 상위의 비밀 키만 알면 하위는 다 알 수 있다는 뜻이다.  
부모 키가 연속된 자식 키를 유도할 수 있고, 각각의 자식 키는 손자 키를 유도할 수 있는 트리 구조로 이루어져 있으며 이러한 구조는 부모 키가 자식 키의 시퀀스를 유도할 수 있고, 각각의 자식은 다시 또 손자 키의 시퀀스를 유도할 수 있다.

HD Wallet은 BIP-32에서 제안되었고, BIP-44에서 개선되었다.

##### HD Wallet 계정 생성 주요 개념

HD Wallet으로 계정을 만들기 위해서는 크게 두 가지가 필요하다. 하나는 정수로 된 시드(seed)값이고 다른 하나는 그 계정까지의 경로(path)이다. HD Wallet의 경로는 여러 개의 정수로 구성되며, 개수에 제한은 없다.

- 시드(seed)

  HD Wallet은 시드로부터 마스터키를 생성한다. 시드는 128, 256, 512비트의 루트 시드(root seed)로 만들며, 니모닉(mnemonic)으로부터 생성된다. HD Wallet의 모든 키는 루트 시드에서 결정적으로 파생되었으며, 생성된 시드로부터 자손 HD Wallet을 재생성할 수 있다. 이렇게 루트 시드를 파생시킨 니모닉을 전송하는 것만으로도 수천 혹은 수백만개의 키가 포함된 HD Wallet의 내보내기, 백업, 복원 가져오기를 쉽게 할 수 있다.

- 경로(path)

  HD Wallet 키의 경로(path)에는 규칙을 사용하여 식별하며, 각 트리 레벨은 슬래스(/) 문자로 구분한다. 마스터 비밀 키로부터 파생된 비밀 키는 m, 마스터 공개키에서 파생된 공개키는 M으로 시작한다.예를 들어 m/0은 마스터 비밀 키의 첫번째 자식 비밀 키이고, M/0은 첫번째 공개키가 된다. m/0/1은 마스터 비밀키의 첫번째 자식의 두번째 자식 비밀 키이며, 마스터키의 손자의 비밀키가 된다.

##### 추가

**BIP-32** : BIP-32에서는 결정적 지갑을 이진 트리 형식으로 계층화 하여 끝없이 비밀 키를 생성할 수 있는 구조를 제안하였다.  
HD 지갑은 BIP32에서 제안한 지갑 구조를 프로그래밍화 한 것이다.  

**BIP-44** : BIP-44는 여러 계정이 여러 목적에 맞게 여러 지갑을 사용할 수 있는 HD 지갑 구조를 제안하였다.  
BIP-44는 다섯가지 트리 레벨로 구성된다.

1. 목적 : 항상 44로 설정된다.
2. 코인 종류 : 어떤 코인인지 나타낸다. SLIP-0044 문서에 각 코인의 종류와 할당된 번호가 있다.
3. 계정 : 사용자는 자신의 지갑을 논리적 계정으로 나눌 수 있다.
4. 잔액 계정 여부 : 비트 코인의 잔액 계정 여부. 하위 트리에 있는 값이 입금 주소인지 잔액 주소인지 표기하며, 잔액 주소이면 1을 넣고, 아니면 0을 넣는다. 이더리움에서는 UTXO가 아닌 어카운트 기반이기 때문에 늘 잔액 주소가 필요없어 늘 이 값이 0이다.
5. 사용 가능한 주소 : 입금 주소나 잔액 주소를 표기한다.

**DRBG** : 일반적으로 컴퓨터가 만들어내는 난수는 예측이 가능한 가짜 난수이기 때문에 안전하지 않다. 따라서 컴퓨터로 만들어낸 난수를 해싱한 값을 사용하는데 이는 해시 알고리즘이 공개되지 않는 이상 완전한 난수이기 때문이다. 이렇게 만든 난수를 해시함수를 통해 진짜 난수로 만드는 알고리즘을 DRBG(Deterministic Random Bits Generate)이라고 한다. HD 지갑에서는 시드 키를 생성할 때 DRBG를 사용한다.



**HMAC-SHA512** : HD 지갑에서는 부모 키를 통해 자식 키를 확인할 수 있어야 하므로, HMAC 방식을 사용하여 자식 키를 만든다. HMAC-SHA512는 부모의 키 값을 패딩하여 XOR 연산을 하고, 그 결과값을 해싱한다. 마스터키는 시드 키에 HMAC-SHA512를 연산한 결과값이다.

### 기타 월렛

**브레인 월렛**

비밀 키를 랜덤하게 생성하지 않고 일련의 단어 목록이나 문장(Seed Pharse)을 사용해 비밀 키를 만드는 지갑이다.  
따라서 비밀 키를 만들 때 사용한 단어 목록이나 문장을 기억하고 있으면 언제든지 비밀 키를 복구할 수 있기 때문에 저장 방식이 간편하다는 장점이 있다.  
또한 사용자에게 익숙한 문장을 시드로 삼는 경우 어딘가에 기록하지 않고도 사용할 수 있기 때문에 안전하다.  
그러나 사용자가 비밀 키를 생성할 때 사용한 단어 목록이나 문장을 잊어버리는 경우 해당 비밀 키에 있는 자산에 영영 접근할 수 없게 된다.  
또한 인간이 만들어 내는 문장은 컴퓨터가 만들어내는 난수에 비해 임의성이 부족하기 때문에 무차별 대입 공격을 통해 비밀 키를 해킹당할 수 있다.  
따라서 오늘날 브레인 월렛은 잘 사용되지 않는다.