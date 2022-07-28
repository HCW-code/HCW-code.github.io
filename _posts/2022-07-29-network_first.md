---
layout: single
title: "[HTTP/네트워크] 기초"
categories: Network
tag: [http, network]

---

### **클라이언트-서버 통신과 API**

클라이언트와 서버 간의 통신은 요청과 응답으로 구성되며 요청이 있어야만 응답이 온다.

프로토콜(Protocol) : 통신 규약

HTTP : 웹 어플리케이션 아키텍처에서 클라이언트와 서버가 서로 대화를 나누는 프로토콜

주요 프로토콜

<center>

<img src="../../images/2022-07-28-network_first/image-20220728222631344.png" alt="image-20220728222631344" style="zoom: 33%;" /></center><br>



**API(Application Programming Interface)**

서버는 클라이언트에게 리소스를 잘 활용할 수 있도록 인터페이스를 제공해줘야 하며 이것을 API라고 한다.  
서버가 리소스 전달을 위한 메뉴판, 즉 API를 구축해놓아야 클라이언트가 이를 활용할 수 있으며 보통 인터넷에 있는 데이터를 요청할 때에는 HTTP라는 프로토콜을 사용하며, 주소(URL, URI)를 통해 접근할 수 있게 된다.

HTTP메소드

- GET - 조회(Read)
- POST - 추가(Create)
- PUT or PATCH - 갱신(Update)
- DELETE - 삭제(Delete)

### **URL과 URI**

URL(Uniform Resource Locator)

네트워크 상에서 웹 페이지, 이미지, 동영상 등의 파일이 위치한 정보를 나타낸다. URL은 scheme, hosts, url-path로 구분 할 수 있다.  
scheme은 통신 방식(프로토콜)을 결정하고 hosts는 웹 서버의 이름이나 도메인, IP를 사용하며 주소를 나타낸다. 그리고 url-path는 웹 서버에서 지정한 루트 디렉토리부터 시작하여 웹 페이지, 이미지, 동영상 등이 위치한 경로와 파일명을 나타낸다.

URI(Uniform Resource Identifier)

일번적으로 URL의 기본 요소인 scheme, hosts, url-path에 더해 query, bookmark를 포함한다.

<center>

<img src="../../images/2022-07-28-network_first/image-20220728223943373.png" alt="image-20220728223943373" style="zoom:50%;" />

</center><br>

### **IP와 Port**

**IP**는 Internet Protocol의 줄임말로, 인터넷 상에서 사용하는 주소체계이다.  
인터넷에 연결된 모든 PC는 IP주소체계를 따라 네덩이의 숫자로 구분되며 이렇게 네덩이의 숫자로 구분된 IP주소체계를 IPv4라고 한다.  
IPv4는 Internet Protocol version 4의 줄임말로 IP주소체계의 네번째 버전을 뜻한다.

IPv4는 각 덩어리마다 0부터 255까지 나타낼 수 있으며 몇가지는 이미 용도가 정해져 있다.

- localhost, 127.0.0.1 : 현재 사용중인 로컬 PC를 지칭한다.
- 0.0.0.0, 255.255.255.255 : broadcast address, 로컬 네트워크에 접속된 모든 장치와 소통하는 주소이다.

IPv6는 IPv4로 할당할 수 있는 PC가 한계를 넘어서게 되면서 생긴것으로 IPv6는 표기법을 달리 책정하여 2^128개의 IP주소를 표현할 수 있다.

<center>

<img src="../../images/2022-07-28-network_first/image-20220728224625380.png" alt="image-20220728224625380" style="zoom:33%;" />

</center><br>



**port**는 IP주소가 가리키는 PC에 접속할 수 있는 통로이다.  
0~1024번까지의 포트 번호는 주요 통신을 위한 규약에 따라 이미 정해져 있으며 그중에 서 잘 알려진 포트 번호는 22번 SSH, 80번 HTTP, 443번 HTTPS가 있다.

### **도메인과 DNS**

Domain name : 웹 브라우저를 통해 특정 사이트에 진입을 할 때, IP 주소를 대신하여 사용하는 주소

DNS(Domain Name System) : 호스트의 도메인 이름을 IP주소로 변환하거나 반대의 경우를 수행할 수 있도록 개발된 데이터베이스 시스템



### **HTTP**

HTTP(HyperText Transfer Protocol) : HTML과 같은 문서를 전송하기 위한 Application Layer 프로토콜이다. HTTP는 웹 브라우저와 웹 서버의 소통을 위해 디자인되었다. 

HTTP messages는 클라이언트와 서버 사이에서 데이터가 교환되는 방식이다. HTTP message에는 다음과 같은 두 가지 유형이 있다.

- 요청(Requests)
- 응답Responses)

<center>

<img src="../../images/2022-07-28-network_first/image-20220728231139145.png" alt="image-20220728231139145" style="zoom:50%;" />

</center>

1. start line : start line에는 요청이나 응답의 상태를 나타낸다. 응답에서는 status line이라고 부른다.
2. HTTP headers : 요청을 지정하거나 메시지에 포함된 본문을 설명하는 헤더의 집합이다.
3. empty line : 헤더와 본문을 구분하는 빈 줄이다.
4. Body : 요청과 관련된 데이터나 관련된 데이터 또는 문서를 포함한다. 요청과 응답의 유형에 따라 선택적으로 사용한다.

이 중 start line과 HTTP headers를 묶어 요청이나 응답의 헤드(head)라고 하고, payload는 body라고 한다.

#### **요청(Requests)**

**Start line**

HTTP 요청은 클라이언트가 서버에 보내는 메시지로 세가지 요소가 있다.

1. 수행할 작업(GET, PUT, POST 등)이나 방식(HEAD or OPTIONS)을 설명하는 HTTP method를 나타낸다
2. 요청 대상(일반적으로 URL이나 URI) 또는 프로토콜, 포트, 도메인의 절대 경로는 요청 컨텍스트에 작성된다. 이 요청 형식은 HTTP method마다 다르다.
   - origin 형식 : ?와 쿼리 문자열이 붙는 절대 경로다. POST, GET, HEAD, OPTIONS 등의 method와 함께 사용한다.
   - absolute 형식 : 완전한 URL 형식으로 프록시에 연결하는 경우 대부분 GET method와 함께 사용한다.
   - Authority 형식 : 도메인 이름과 포트 번호 이루어진 URL의 authority component이다. HTTP터널을 구축하는 경우, CONNECT와 함께 사용할 수 있다.
   - asterisk 형식 : OPTIONS와 함께 별표(*)하나로 서버 전체를 표현한다.

3. HTTP 버전은 메시지의 다른 구조를 결정한다. 이를 위해 HTTP 버전을 함께 입력한다.

**Headers**

요청의 Headers는 기본 구조를 따른다. 대소문자 구분 없는 문자열과 콜론( : ), 값을 입력한다. 값은 헤더에 따라 다르며 여러 종류의 헤더가 있고 다음과 같이 그룹을 나눌 수 있다.

- General header : 메시지 전체에 적용된다.
- Request headers : User-Agent, Accept-Type, Accept-Language과 같은 헤더는 요청을 보다 구체화 한다. Referer처럼 컨텍스트를 제공하거나 If-Nonde과 같이 조건에 따라 제약을 추가할 수 있다.
- Entity headers : Content-Length와 같은 헤더는 body에 적용되며 body가 비어 있는 경우 entity headers는 전송되지 않는다.
<center>
<img src="../../images/2022-07-28-network_first/image-20220728233055880.png" alt="image-20220728233055880" style="zoom:40%;" />
</center><br>
**Body**

요청의 본문은 HTTP messages 구조의 마지막에 위치한다. 모든 요청에 body가 필요하지는 않으며 GET, HEAD, DELETE, OPTIONS처럼 서버에 리소스를 요청하는 경우에는 본문이 필요하지 않다. POST나 PUT과 같은 일부 요청은 데이터를 업데이트하기 위해 사용한다. body는 다음과 같이 두 종류로 나눌 수 있다.

- Single-resource bodies(단일 - 리소스 본문) : 헤더 두 개(Content-Type과 Content-Length)로 정의된 단일 파일로 구성된다.
- Multiple-resource bodies(다중 - 리소스 본문) : 여러 파트로 구성된 본문에서는 각 파트마다 다른 정보를 지닌다.

#### **응답(Responses)**

**Status line**

응답의 첫줄은 Status line이라고 부르며 다음의 정보를 포함한다.

1. 현재 프로토콜의 버전(HTTP/1.1)
2. 상태 코드 - 요청의 결과를 나타낸다.(200, 302, 404 등)
3. 상태 텍스트 - 상태 코드에 대한 설명

**Headers**

응답에 들어가는 HTTP headers는 요청 헤더와 동일한 구조를 가지고 있다. 대소문자 구분 없는 문자열과 콜론( : ), 값을 입력한다. 값은 헤더에 따라 다르며 요청의 헤더와 마찬가지로 몇 그룹으로 나눌 수 있다.

- General headers : 메시지 전체에 적용된다.
- Response headers : Vary, Accept-Ranges와 같이 상태 줄에 넣기에는 공간이 부족했던 추가 정보를 제공한다.
- Entity headers : Content-Length와 같은 헤더는 body에 적용되며 body가 비어있는 경우 entity headers는 전송되지 않는다.
<center>
<img src="../../images/2022-07-28-network_first/image-20220728234119805.png" alt="image-20220728234119805" style="zoom:35%;" />
</center><br>
**Body**

응답의 본문은 HTTP messages구조의 마지막에 위치한다. 모든 응답에 body가 필요하지는 않으며 201, 204와 같은 상태 코드를 가지는 응답에는 필요하지 않다. 응답의 body는 다음과 같이 두 종류로 나눌 수 있다.

- Single-resource bodies(단일 - 리소스 본문) :
  - 길이가 알려진 단일-리소스 본문은 두 개의 헤더(Content-Type, Content-Length)로 정의한다.
  - 길이를 모르는 단일 파일로 구성된 단일-리소스 본문은 Transfer-Encoding이 chunked로 설정되어 있으며, 파일은 chunk로 나뉘어 인코딩되어 있다.
- Multiple-resource bodies(다중 - 리소스 본문) : 서로 다른 정보를 담고 있는 body이다.



**Stateless(무상태성 - HTTP의 큰 특징)**

Stateless는 말 그대로 상태를 가지지 않는다는 뜻이다. HTTP로 클라이언트와 서버가 통신을 주고 받는 과정에서 HTTP가 클라이언트나 서버의 상태를 확인하지 않는다.  
HTTP는 통신 규약일 뿐이므로 상태를 저장하지 않으며 필요에 따라 다른 방법(쿠키-세션, API 등)을 통해 상태를 확인할 수 있다.