20.09.03 (목)

## 목표

자바스크립트를 전체적으로 훑는 시간을 가지자.

리덕스를 직접 만들어보자 

Javascript의 함수는 값을 변환하게 되어 있다. 다른 곳에서는 값을 반환하면 함수 안하면 프로시저라고도 하는데 JS에서는 값을 반환한다.

return 을 하던가 undefined를 반환하는 방법.

new를 통해  호출하면 명시적 return 이 없어도 인스턴스 객체로 취급한다.

```jsx
// 함수 선언
function foo(){
	return 0;
}// 여기에 ; 없는게 맞다=> 왜?

// 함수 정의문(표현식), 익명함수
const bar = function (){

}

// iife
(function(){

})()

// 화살표 함수, arrow 함수

const bar = (a) => {
	
}

const x = {
	y:5
};

x.name = 10;

function foo(){
	this.fds = 10; // 동적 바인딩
	// constructer, prototype
}

const y = new foo(); // 인스턴스 객체

if(y instanceof foo){
 // TS를 사용하는 신뢰성으로 이용
}
// y가 foo 함수가 생성한 객체

class bar {
	constructor(){
		this.name = 10;
	}
}
console.log(new bar()) // bar { name: 10, constructor: Object:bar}
```

함수하나 줄테니 대신 호출해줘 = 콜백함수

함수를 대신 리턴하는 함수 1급함수  HOC 입력도 컴포넌트 출력도 컴포넌트

모든 자바스크립트 코드는 하나는 식, 문으로 나눌 수 있다. 실행하면 실행의 결과가 값으로 마무리 되면 식, 실행했는데 값이 안나오면 문(if, while문) ⇒ 마지막에 세미콜론이 있냐 없냐, 세미콜론은 식의 마무리, 문의 마무리는 

명시적인것과 암묵적인 것의 차이 ⇒ 암묵적인 것은 전부가 동의해야하는데 쉽지 않아 명시적인것이 좋다.

JS 첫글자가 대문자면 new로 호출,  class로 만들면 new로만 호출

---

쉬는시간 후

```jsx
const person = {
	name: '김민태',
	getName(){
		return this.name;
	}
}

console.log(person.getName());

const man = person.getName;

console.log(man()) // error 호출자가 없음. 호출자가 확인이 안되면 전역객체가 된다. 
```

함수한테 함수를 주는 ⇒ 위임하는 콜백함수

괄호호출, call, apply로 js에서 함수를 호출하는 방법.

call, apply, bind를 이해해야함 아니면 면접 광탈

```jsx
// 클로져 : 값을 보호할 때 많이 사용함.
// 클로져 이게 다임!

function foo(x){
	return (){
		return x
	}
}

const f = foo(10);

console.log(f())

// 2

const person = {
	age: 10
} 
person.age = 500;
// 애를 막을 수 없다..

const makePerson(){
	let age = 10;
	return {
		getAge(){
			return age;
		},
		// setAge는 방어 코드
		setAge(x){
			age = x > 1 && x < 130 ? x: age;
		}
	}
}

let p = makePerson();

console.log(p.getAge()) //  age를 보호할 수 있음
```

> 오류 메시지 쫙 정리해봐라 그리 오래 걸리지 않고 한번 해 두면 큰 도움이 됨.

## 비동기 어려움

왜 어렵냐? 인간에 두뇌가 생각을 동기적으로 하기 때문에 어렵다. 똑똑한 친구들은 어려워? 그러면 안어렵게 만들어 보자. ⇒ 비동기를 동기처럼 보이게 만듬

```jsx
// 1. 콜백 헬

setTimeout(function(x){
	console.log('앗싸')
	setTimeout(function(y){
		console.log('웃싸');
	}, 200
}

// 2. Promise => 그지 같다 => 타이핑이 많다.

const p1 = new Promise((resolve, reject)=> {
	setTimeout(()=>{
		resolve('응답1')
	}, 1000)

	resolve(); // 성공
	reject();	 // 실패
})

const p2 = new Promise((resolve, reject)=> {
	setTimeout(()=>{
		resolve('응답2')
	}, 1000)
})

p1.then(function (){ // 성공

}).catch(function(){ // 실패

}
p1.then(p2)
	.then(function(r){
		console.log(r);
	})
	.catch(function (){});

// 3. 비동기 함수

const delay = ms => new Promise(resolve=> setTimeout(resolve, ms)

async function main(){
	console.log('1')
	// 3초동안 멈추는 함수
	await	delay(3000)
	console.log('2')
}

main();

```

---

redux 직접 만들기

// component는 redux의 상태 객체를 직접적으로 바꾸지 못한다.

js 모든 객체는 참조형이다. 

## 질문

1. 4번째줄 ; 찍으면 왜 틀린가 ⇒ 문이기 때문에 ; 을 찍지 않는다.
2. 신입 개발자에게 필요한 cs 지식 : 자료구조, 운영체제(싱글스레드, 메모리, 운영체제가 어떻게 관리하는 지 등이 OS 지식임)
3. 코테를 잘 보기 위해서 어떤 것을 해야하나? ⇒ 알고리즘을 열심히 하자. 어떤 회사는 중요하게 안보기도 함. 회사마다 케바케이다.
4. 요즘은 FE 개발자가 많이 부족한 상황이다.

## Reference

민태님 개발 블로그

[https://medium.com/ibare-story/e252506f8525](https://medium.com/ibare-story/e252506f8525)

[https://medium.com/ibare-story/프로그래밍-단순한-기능-기능의-결합-의미의-부여-1d4ab9d59415](https://medium.com/ibare-story/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EB%8B%A8%EC%88%9C%ED%95%9C-%EA%B8%B0%EB%8A%A5-%EA%B8%B0%EB%8A%A5%EC%9D%98-%EA%B2%B0%ED%95%A9-%EC%9D%98%EB%AF%B8%EC%9D%98-%EB%B6%80%EC%97%AC-1d4ab9d59415)

자바스크립트 기본 : [https://fastcampus-js-bootcamp.herokuapp.com/](https://fastcampus-js-bootcamp.herokuapp.com/)
