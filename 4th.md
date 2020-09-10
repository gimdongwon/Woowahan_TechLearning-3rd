## 목표

1. 컴포넌트 디자인 및 비동기

일반 컨텍스트

에로우 함수는 렉시컬 컨텍스트, 실행 컨텍스트 this가 고정되서 바인딩이 필요가 없다.

클래스 컴포넌트도 만듬. 클래스 컴포넌트는 당장 없애기앤 큰 문제가 있을 거 같아 명맥만 유지하는 중이다.

이름 앞에 *가 붙은 함수를 제러네이터

async가 붙으면 비동기 함수

Promise()랑 굉장히 밀접함, 혼용해서 굉장히 많이 쓰임, 현대 js에서 모던한 스펙

return 이 없는 js 함수는 프로시져

```jsx
// index.js

import React from "react";
import ReactDOM from "react-dom";
import App from "./App";

const rootElement = document.getElementById("root");
const sessionList = [
  { title: "1th : Overciew" },
  { title: "2nd : Redux 만들기" },
  { title: "3rd : React 만들기" },
  { title: "4th : component design and asyncronize" }
];

ReactDOM.render(
  <React.StrictMode>
    <App store={{ sessionList }} />
  </React.StrictMode>,
  rootElement
);

const p = new Promise(function (resolve, reject) {
  setTimeout(() => {
    resolve("1");
  }, 1000);
});

p.then(function (r) {});

function* makeNumber() {
  let num = 1;

  while (true) {
    yield num;
  }
}

const i = makeNumber();

console.log(i.next());

const delay = (rms) => new Promise((resolve) => setTimeout(resolve, rms));

function* main() {
  console.log("start");
  yield delay(3000);
  console.log("after 3 seconds");
}

async function main2() {
  console.log("start");
  await delay(3000);
  console.log("after 3 secondss");
}

main2();

const it = main();
const { value } = it.next();
value.then(() => {
  it.next();
});
```

```jsx
// app.js

import React from "react";

const SessionItem = ({ title }) => <li>{title}</li>;

const App = (props) => {
  const [displayOrder, toggleDisplayOrder] = React.useState("ASC");
  const { sessionList } = props.store;
  const orderedSessionList = sessionList.map((session, i) => ({
    ...session,
    order: i
  }));

  const onToggleDisplayOrder = () => {
    toggleDisplayOrder(displayOrder === "ASC" ? "DESC" : "ASC");
  };

  return (
    <div>
      <header>
        <h1>React and Typescript</h1>
      </header>
      <p>전체 세션 갯수 : {displayOrder}</p>
      <button onClick={toggleDisplayOrder}>ReSort</button>
      <ul>
        {orderedSessionList.map((session, i) => (
          <SessionItem title={session.title} key={i} />
        ))}
      </ul>
    </div>
  );
};

export default App;
```
