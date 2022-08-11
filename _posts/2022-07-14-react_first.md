---
layout: single
title: "[React] React 기초"
categories: React
tag: [react, javascript]
toc: true
---

리액트는 프론트앤드 개발을 위한 JavaScript 오픈소스 라이브러리이다.<br>

### 리액트의 3가지 특징

- 선언형<br>
- 컴포넌트 기반<br>
- 범용성<br>

#### **선언형**

코드를 자세히 보지 않아도 코드의 의도를 분명히 알수 있게 작성하는 방식<br>
리액트는 한페이지를 보여주기 위해 HTML/CSS/JS로 나눠서 적기 보다는 하나의 파일에 명시적으로 작성할 수 있게 JSX를 활용한 선언형 프로그래밍을 지향한다.<br>

#### **컴포넌트 기반**

하나의 기능구현을 위해 여러가지를 묶어 놓은것<br>
리액트는 하나의 기능 구현을 위해 여러 종류의 코드를 묶어둔 컴포넌트를 기반으로 개발한다. 컴포넌트로 분리하면 서로 독립적이고 재사용 가능하기 때문에 기능 잧에 집중하여 개발할 수 있다.<br>

#### **범용성**

리액트는 JavaScript 프로젝트 어디에든 유연하게 적용될 수 있다.<br>
Facebook에서 관리하여 안정적이고, 가장 유명하며, 리액트 네이티브로 모바일 개발도 가능하다.<br>

### **JSX**

JSX는 JavaScript에서 확장된 문법이지만 브라우저가 바로 실행할 수 있는 Javascript코드가 아니다. 그래서 Babel을 이용하여 JSX를 브라우저가 이해할 수 있는 JavaScript파일로 컴파일한다.<br>

<center>
<img width="450" alt="babel" src="https://user-images.githubusercontent.com/72719325/178930918-1fd7fa83-9720-4eb2-acd5-272f85c88161.png"></center><br>
#### **JSX 규칙**

- JSX에서 여러 엘리먼트를 작성하고자 하는 경우, 최상위에서 opening tag와 closing tag로 감싸주어야 한다.<br>
<center>
<img width="450" alt="elements" src="https://user-images.githubusercontent.com/72719325/178930949-957594f3-24d6-4d44-b49b-6e7349098d85.png">
</center><br>
- React에서 HTML class 속성을 지정하려면 "className"으로 표기해야 한다.<br>
<center>
<img width="500" alt="className" src="https://user-images.githubusercontent.com/72719325/178930941-f2ab6b63-f055-49b8-aa42-e56e38fd5c6a.png">
</center><br>
- JSX에서 JavaScript를 쓰고자 한다면 꼭 중괄호를 이용해야 한다.<br>
<center>
<img width="270" alt="mid" src="https://user-images.githubusercontent.com/72719325/178937034-0fd11f83-cdb6-46b4-9ff2-ba68a2dbfd74.png"></center><br>
- 사용자 정의 컴포넌트는 대문자로 시작한다.<br>
<center>
<img width="450" alt="capital" src="https://user-images.githubusercontent.com/72719325/178930926-337f567c-80f4-41fb-ac9b-82397da0ff82.png"></center><br>
- 조건부 렌더링에는 삼항연산자를 사용해야 한다.<br>
<center>
<img width="350" alt="if" src="https://user-images.githubusercontent.com/72719325/178930952-98c376c3-0648-4eb2-a2e1-f5d7a08cec28.png"></center><br>
- 여러 개의 HTML엘리먼트를 표시할 때, map()함수를 이용한다.<br>
<center>
<img width="400" alt="map" src="https://user-images.githubusercontent.com/72719325/178931637-5707cfe2-bdeb-42d4-8acc-1d369f4c8dd9.png"></center>

**예시**<br>
map을 이용한 반복<br>

<center><div><img width="300" alt="map_ex" src="https://user-images.githubusercontent.com/72719325/178932736-34d8048c-494e-4692-b58d-d5a70f640e0e.png"><br>
[함수를 나눴을 때]</div></center><br>
<center><div><img width="300" alt="map_ex1png" src="https://user-images.githubusercontent.com/72719325/178932747-65706124-980c-4ce4-a225-d3e9a0ae43a9.png"><br>
[return문 안에 인라인으로 처리할 때]</div></center>
