## aim

1. React를 기본적인 내용들
2. React를 JS로 구현하기

## note

> 이름만 잘 지어도 70%는 먹고 들어간다

너무 높은 수준의 무언가를 추구하다 기본적인 것을 소홀히 하면 안된다

realDOM을 가지고 html을 조작하면 안정성이 떨어진다 ⇒ realDOM을 직접적으로 다루면 row level 의 다루는 방식이다. 

```jsx
const list = [
  { title: "React에 대해 알아봅시다" },
  { title: "Redux에 대해 알아봅시다" },
  { title: "TypeScript에 대해 알아봅시다" }
];

const rootElement = document.getElementById("root");

function app(items) {
  rootElement.innerHTML = `
    <ul>
      ${items.map((item) => `<li>${item.title}</li>`).join("")}
    </ul>
  `;
}

app(list);
```

React의 컨셉은 간단하다.

### React 판서

![img1](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6b83031f-298d-4c9f-99de-105e596039c2/_2020-09-08_19.57.16.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20200910%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20200910T151129Z&X-Amz-Expires=86400&X-Amz-Signature=547069c459b4494664222032942d685903daece4b6bc71558f32fc6b36aa9693&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22_2020-09-08_19.57.16.png%22)

까다로운 친구를 감싸서 접근하면 덜 까다롭다. 다루기 쉬운 구조를 만들어서 복잡한 구조를 다루면 좋다.

브라우저는 string 이라 다루기 쉬운 DOM Tree로 만들어서 사용

이게 V-DOM 개념이다.

![img2](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/77ec11c4-7f1e-4634-af1d-6fa80a554b2f/_2020-09-08_19.58.29.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20200910%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20200910T150052Z&X-Amz-Expires=86400&X-Amz-Signature=767be920374f4bc075d37767c5b7fdbdccf28e9613a338412ead111f41994774&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22_2020-09-08_19.58.29.png%22)

이게 React의 컨셉. ⇒ 개발하기 쉽게 만든 JSX

오늘 v-dom도 만들 것임.

> 좋은 컨셉은 좋은 효과를 창출함 ⇒ 이름 잘 지어라

```jsx
import React from "react";
import ReactDOM from "react-dom";

const vdom = {
  type: "ul",
  props: {},
  children: [
    { type: "li", props: { className: "item" }, childeren: "React" },
    { type: "li", props: { className: "item" }, childeren: "Redux" },
    { type: "li", props: { className: "item" }, childeren: "TypeScript" },
    { type: "li", props: { className: "item" }, childeren: "Mobx" }
  ]
};

function createElement(type, props = {}, ...children) {
  return { type, props, children };
}

function StudyList() {
  React.createElement("ul", {}); // createElement는 vdom 만드는데 render할 때 화면에 붙임.
  return (
    <ul>
      <li className="item" label="haha">
        React
      </li>
      <li className="item">Redux</li>
      <li className="item">TypeScript</li>
      <li className="item">Mobx</li>
    </ul>
  );
}

function App() {
  const vdom = createElement("ul", {}, createElement("li", {}, "React"));
  return (
    <div>
      <h1>Hello?</h1>
      <StudyList item="abcd" id="hoho" />
    </div>
  );
}

ReactDOM.render(<App />, document.getElementById("root")); // realdom으로 compote 하는 애임
```

jsx는 바벨이 다 해줌 /* jsx H */ ⇒ createElement 이름을 바꿔줌.

대문자는 함수 React 사용자 컴포넌트는 대문자로 시작하자.

```jsx
// 틀린 코드

import React from "react";
import ReactDOM from "react-dom";

/*  @jsx React.createElement*/
// const vdom = {
//   type: "ul",
//   props: {},
//   children: [
//     { type: "li", props: { className: "item" }, childeren: "React" },
//     { type: "li", props: { className: "item" }, childeren: "Redux" },
//     { type: "li", props: { className: "item" }, childeren: "TypeScript" },
//     { type: "li", props: { className: "item" }, childeren: "Mobx" }
//   ]
// };

function renderElement(node) {
  const el = document.createElement(node.type);
  node.children.map(renderElement).forEach((element) => {
    el.appendChild(element);
  });
  return el;
}

function render(newVdom, container) {
  let vdom;
  container.appendChild(renderElement(newVdom));
}

function createElement(type, props = {}, ...children) {
  if (typeof type === "function") {
    return type.apply(null, [props, ...children]);
  }
  return { type, props, children };
}

function Row(props) {
  return <li>{props.label}</li>;
}

function StudyList(props) {
  // React.createElement("ul", {}); // createElement는 vdom 만드는데 render할 때 화면에 붙임.
  return (
    <ul>
      <Row label="하하하 음메" />
      <li className="item">React</li>
      <li className="item">Redux</li>
      <li className="item">TypeScript</li>
      <li className="item">Mobx</li>
    </ul>
  );
}

function App() {
  // const vdom = createElement("ul", {}, createElement("li", {}, "React"));
  return (
    <div>
      <h1>Hello?</h1>
      <StudyList item="abcd" id="hoho" />
    </div>
  );
}

console.log(<App />);
render(<App />, document.getElementById("root"));

// ReactDOM.render(<App />, document.getElementById("root")); // realdom으로 compote 하는 애임
```

## Hook

```jsx
import React, { useState } from "react";
import ReactDOM from "react-dom";

class Hello extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 1
    };
  }

  componentDidMount() {
    this.setState({ count: this.state.count + 1 });
  }
  render() {
    return <p>HI!</p>;
  }
}

// const hello = new Hello();
// hello.render();

// if (hello.hasOwnProperty("componentDidMount")) {
//   hello.componentDidMount();
// }

function App() {
  const [counter, setCounter] = useState(1);

  return (
    <div>
      <h1 onClick={() => setCounter(counter + 1)}>State {counter}</h1>
      <Hello />
    </div>
  );
}

ReactDOM.render(<App />, document.getElementById("root"));
```

## Reference

[https://stackoverflow.com/questions/46989454/class-vs-classname-in-react-16/46991278](https://stackoverflow.com/questions/46989454/class-vs-classname-in-react-16/46991278)
