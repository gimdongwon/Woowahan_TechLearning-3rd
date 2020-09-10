20.09.01

스터디의 공용 목표

> 내가 잘하고 있나?

네트워킹을 잘 이어나가면 좋겠다. 코드 품질, 아키텍쳐, 적정 기술

기술을 왜 선택하였느냐, 어떤 상황에서 제대로 된 선택을 하였는가

전달하고 싶은 것

1. 도구

    소프트웨어를 만든다는 것은 굉장히 오래걸리는 것이었다. 여기서 언어는 TypeScript, 도구는 React

![img](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/083775ca-adb5-4b77-b394-48ddf3096c21/_2020-09-01_19.56.35.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20200910%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20200910T145655Z&X-Amz-Expires=86400&X-Amz-Signature=38dcddd297c327c110afa154d500353f67298a7c565d5209308e6afa0b5c9626&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22_2020-09-01_19.56.35.png%22)

제한을 둔 이유는 3년차 미만의 수준이 일치하고 싶었다. React에 대한 이해, Typescript가 무엇인가에 대한 점은 알고 있으면 좋을 대상으로 선택

Typescript, React, Redux, Mobx, Redux-Saga, CodeSandbox, Bludprint(React, TS랑 잘 맞을것), Testing-Library

암묵적인거 보다는 명시적인 것이 더 좋다.

요즘은 짧고 암묵적이고 난해한 코드보다 읽기 쉽고 명시적인 코드(길더라도)

> React에 Typescript 를 넣으면 인터페이스와 alias 위주로 넣어서 90% 이상 마이그레이션 이 가능하다.

### React

—template typescript 를 넣으면 typescript기반의 cra가 만들어짐.

## 배운점

1. Type alias

    ```tsx
    type Age = number;

    let age: Age = 10;
    let weight: number = 72;
    ```

2. 컴파일타임에 동작하는 코드, 런타임에만 동작하는 코드로 나뉜다. 하지만 좋은 기능들은 컴파일 타임에 동작하는 코드들이 많다.

      ```tsx
      // function isDateBoolean(obj:any): boolean {
      //     return typeof obj==='object' && 'toISOString' in obj;
      // }
      type Age = number;

      let age: Age = 10;
      let weight: Age = 72;

      // 장점은 일반화 되어 있어서 다양한 용도로 사용할 수 있다.
      // 

      type Foo = {
          age: Age;
          name: string;
      }

      interface Bar {
          age: Age;
          name: string;
      }

      const foo: Foo = {
          age: 10,
          name: 'kim'
      }

      const bar: Bar = {
          age:10,
          name: 'kim'
      }
      ```

3. typealias vs interface 어떤 것을 사용해야 하나?

4. mobx

mobx는 redux에 대체제가 아니라 상태관리의 방법이 아예 다르다. 단순한 형태를 가지면 원하는 형태로 가이드하기 편하다.

## 질문하고 싶은 점

1. cra로 product 만들었을 때 문제점.

    cra가 제공하지 않는 구성을 세팅하는데 까다롭다. 

    cra가 고쳐줬으면 하는 cs를 거의 받아주지 않는다.

    다양한 환경에 대한 대응이 어렵다. local, product 환경을 나누기 어렵다.

    ⇒ 프로덕션용 앱으로는 적합하지 않다.

## Reference

[https://www.typescriptlang.org/play](https://www.typescriptlang.org/play)

[https://codesandbox.io/index2](https://codesandbox.io/index2)

[https://reactjs.org/](https://reactjs.org/)

[https://redux.js.org/](https://redux.js.org/)

[https://mobx.js.org/README.html](https://mobx.js.org/README.html)

[https://redux-saga.js.org/](https://redux-saga.js.org/)

[https://blueprintjs.com/](https://blueprintjs.com/)

[https://testing-library.com/](https://testing-library.com/)
