---
layout: single
title: "[인증/보안] HTTPS, Hashing"
categories: Secure
tag: [https, hashing]
toc: true
---

## HTTPS

HTTPS : Hyper Text Transfer Protocol Secure Socket layer

HTTPS는 HTTP요청을 SSL혹은 TLS라는 알고리즘을 이용해, HTTP 통신을 하는 과정에서 내용을 암호화하여 데이터를 전송하는 방법이다.

인증에서 HTTPS 프로토콜을 사용해야만 하는 이유는 HTTP보다 상대적으로 안전한 방법이고, 데이터 제공자의 신원을 보장받을 수 있기 때문이다.

#### 암호화

HTTPS 프로토콜의 특징 중 하나는 암호화된 데이터를 주고받기 때문에, 중간에 인터넷 요청이 탈취되더라도 그 내용을 알아볼 수 없다. 기존에 배웠던 HTTP 프로토콜은 요청 미 응답을 탈취한다면 프로그램을 이용하여 해당 요청으로 전달되는 데이터의 내용을 확인할 수 있게 된다.

#### 인증서

HTTPS 프로토콜의 또 다른 특징 중 하나는 브라우저가 응답과 함께 전달된 인증서 정보를 확인할 수 있다는 점이다. 브라우저는 인증서에서 해당 인증서를 발급한 CA 정보를 확인하고 인증된 CA가 발급한 인증서가 아니라면 아래와 같이 화면에 경고창을 띄워 서버와 연결이 안전하지 않다는 화면을 보여준다.

<center>

<img src="../../images/2022-08-15-secure_first/image-20220815210719476.png" alt="image-20220815210719476" style="zoom: 33%;" />

</center><br>

이렇게 브라우저는 인증서의 도메인과 데이터를 제공한 도메인을 비교할 수 있기 때문에 인증서의 도메인 정보와 데이터 제공자의 도메인 정보가 다른 '중간자 공격'을 감지하여 보안 위협으로부터 사용자 및 사용자의 데이터를 보호할 수 있다.

또한 이런 경고를 직접 보여줌으로써 브라우저들은 인증된 CA가 발급한 인증서를 이용하여 데이터를 제공하는 안전한 서버를 사용할 수 있게 사용자를 유도한다.

### 사설 인증서 발급 및 HTTPS 서버 구현

macOS -> Homebrew를 통해 mkcert

```shell
$ brew install mkcert
```

#### 인증서 생성

```shell
$ mkcert -install
```

```shell
$ mkcert -key-file key.pem -cert-file cert.pem localhost 127.0.0.1 ::1
```

#### HTTPS 서버 작성

```js
const https = require('https');
const fs = require('fs');

https
	.createServer(
	{
		key: fs.readFileSync(__dirname + '/key.pem', 'utf-8'),
		cert: fs.readFileSync(__dirname + '/cert.pem', 'utf-8'),
	},
	function(req, res) {
		res.write('Congrats! you made https server now');
		res.end();
	}
	).listen(3001)
```

#### express.js 이용

```js
const https = require('https');
const fs = require('fs');
const express = require('express');

const app = express();

https
	.createServer(
	{
		key: fs.readFileSync(__dirname + '/key.pem', 'utf-8'),
		cert: fs.readFileSync(__dirname + '/cert.pem', 'utf-8'),
	},
	app.use('/', (req, res) => {
		res.send('Congrats! you made https server now')
	})
	).listen(3001)
```

## Hashing

Authentication(Plaintext)

<center>

<img src="../../images/2022-08-15-secure_first/image-20220815212421502.png" alt="image-20220815212421502" style="zoom: 33%;" />

</center>

Authentication(Plaintext) - 암호화

<center>

<img src="../../images/2022-08-15-secure_first/image-20220815212528775.png" alt="image-20220815212528775" style="zoom: 33%;" />

</center>

### Hashing

어떠한 문자열에 '임의의 연산'을 적용하여 다른 문자열로 변환하는 것

1. 모든 값에 대해 해시 값을 계산하는데 오래걸리지 않아야 한다.
2. 최대한 해시 값을 피해야 하며, 모든 값은 고유한 해시 값을 가진다.
3. 아주 작은 단위의 변경이라도 완전히 다른 해시 값을 가져야 한다.

<center>

<img src="../../images/2022-08-15-secure_first/image-20220815212723544.png" alt="image-20220815212723544" style="zoom: 33%;" />

</center>

Authentication(Hashing)

<center>

<img src="../../images/2022-08-15-secure_first/image-20220815212818045.png" alt="image-20220815212818045" style="zoom: 33%;" />

</center>

### Salt

암호화해야 하는 값에 어떤 '별도의 값'을 추가하여 결과를 변형하는 것

1. 암호화만 해놓는다면 해시된 결과가 늘 동일

   해시된 값과 원래 값을 테이블(레인보우 테이블)로 만들어서 decoding 해버리는 경우도 생긴다.

2. 원본값에 임의로 약속된 '별도의 문자열'을 추가하여 해시를 진행한다면 기존 해시값과 전혀 다른 해시값이 반환되어 알고리즘이 노출되더라도 원본값을 보호할 수 있도록 하는 안전 장치

3. 기존 : (암호화 하려는 값) => (hash 값)

   Salt 사용 : (암호화 하려는 값) + (Salt용 값) => (hash 값)

Authentication(Hashing) - Salt

<center>

<img src="../../images/2022-08-15-secure_first/image-20220815213154283.png" alt="image-20220815213154283" style="zoom: 33%;" />

</center>