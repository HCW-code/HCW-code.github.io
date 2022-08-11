---
layout: single
title: "[React] Props, State"
categories: React
tag: [react, props, state]
toc: true
---

### **Props**

#### **props의 특징**

- props는 성별이나 이름처럼 변하지 않는 외부로부터 전달받은 값으로 웹 어플리케이션에서 해당 컴포넌트가 가진 속성에 해당한다.
- 부모 컴포넌트로부터 전달받은 값이다.
- props로 어떤 타입의 값도 넣어 전달할 수 있도록 props는 객체의 형태를 가진다.
- props는 외부로부터 전달받아 변하지 않는 값이므로 함부로 변경될 수 없는 읽기 전용 객체이다.

#### **props 사용법**

1. 하위 컴포넌트에 전달하고자 하는 값(data)과 속성을 정의한다.
2. props를 이용하여 정의된 값과 속성을 전달한다.
3. 전달받은 props를 렌더링한다.  

```react
function Parent() {
return (
  <div className="parent">
    <Child text={"hello"} />
  </div>
	);
}

function Child(props) {
return (
	<div className="child">
	 <p>{props.text}</p>
	</div>
	);
}
```

<center>[Props 사용법 1]</center>

<br>

```react
function Parent() {
return (
  <div className="parent">
    <Child>hello</Child>
  </div>
	);
}

function Child(props) {
return (
	<div className="child">
	 <p>{props.children}</p>
	</div>
	);
}
```

<center>[Props 사용법 2]</center>

### **State**

state는 Toggle Switch나 Counter처럼 컴포넌트 내부에서 변할 수 있는 값이다. 

#### **useState 사용법**

-useState를 이용하기 위해서는 React로부터 useState를 불러와야 한다. import 키워드로 useState를 불러와야한다.

```react
import {useState} from "react";
```

-이후 useState를 컴포넌트 안에서 호출해준다. 아래 예시의 isChecked, setIsChecked는 useState의 리턴값을 구조 분해 할당한 변수이다.

```react
const [isChecked, setIsChecked] = useState(false);
```

```react
const [state 저장 변수, state 갱신 함수] = useState(상태 초기 값);
```

#### **주의점**

React state는 상태 변경 함수 호출로 변경해야한다. 강제로 변경을 시도할 경우 리렌더링이 되지 않는다거나 state가 제대로 반영되지 않는다.

##### **이벤트 처리 Hands-on**

React의 이벤트 처리 방식은 DOM의 이벤트 처리 방식과 유사하지만 문법차이가 있다.  
```html
<button onclick="handleEvent()">Event</button> #HTML
```

```react
<button onClick={handleEvent}>Event</button> #React
```

#### **onChange**

Input, textarea, select와 같은 폼(Form) 엘리먼트는 사용자의 입력값을 제어하는데 사용된다. React에서는 이러한 변경될 수 있는 입력값을 일반적으로 컴포넌트의 state로 관리하고 업데이트한다. onChange 이벤트가 발생하면 e.target.value를 통해 이벤트 객체에 담겨있는 input값을 읽어올 수 있다.

```react
function NameForm(){
	const [name, setName] = useState("");

const handleChange = (e) => {
	setName(e.target.value);
}

return (
	<div>
		<input type="text" value={name} onChange={handleChange}></input>
	</div>
	)
};
```

#### **onClick**

onClick 이벤트는 사용자가 클릭이라는 행동을 하였을 때 발생하는 이벤트이다. 버튼이나 a태그를 통한 링크 이동 등과 같이 주로 사용자의 행동에 따라 애플리케이션이 반응해야 할 때 자주 사용하는 이벤트이다.

```react
function NameForm(){
	const [name, setName] = useState("");

const handleChange = (e) => {
	setName(e.target.value);
}
const handleClick = () => {
  alert(name);
}

return (
	<div>
		<input type="text" value={name} onChange={handleChange}></input>
    <button onClick={() => alert(name)}>Button</button> #1
    <button onClick={handleClick}>Button</button> #2
	</div>
	)
};
```

onClick이벤트에 alert함수를 바로 호출하면 컴포넌트가 렌더링될 때 함수 자체가 아닌 함수 호출의 결과가 onClick에 적용된다. 때문에 버튼을 클릭할 때가 아닌 컴포넌트가 렌더링될 때에 alert이 실행되고 따라서 그 결과인 undefined가 onClick에 적용되어 클릭했을 때 아무런 결과도 일어나지 않는다.  
따라서 onClick이벤트에 함수를 전달할 때는 함수를 호출하는 것이 아니라 아래와 같이 리턴문 안에서 함수를 정의하거나 리턴문 외부에서 함수를 정의 후 이벤트에 함수 자체를 전달해야한다. 단, 두가지 방법 모두 arrow function을 사용하여 함수를 정의하여야 해당 컴포넌트가 가진 state에 함수들이 접근할 수 있다.

### React 데이터 흐름

<center>

<img src="../../images/2022-07-18-react_third/image-20220718180307393.png" alt="image-20220718180307393" style="zoom:50%;" />

</center>  
컴포넌트는 컴포넌트 바깥에서 props를 이용해 데이터를 마치 인자 혹은 속성처럼 전달 받을 수 있다. 즉 데이터를 전달하는 주체는 부모 컴포넌트가 되며 이는 데이터 흐름이 하향식(top-down) 임을 의미한다.  
이 단방향 데이터 흐름(one-way data flow)은 React를 대표하는 설명중 하나일 정도로 중요하다.
