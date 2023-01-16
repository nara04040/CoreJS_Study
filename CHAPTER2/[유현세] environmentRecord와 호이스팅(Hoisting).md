[\>\[Javascript\] 실행 컨텍스트](https://luka-frontend.tistory.com/39)

 [\[Javascript\] 실행 컨텍스트(Execution Context)

실행 컨텍스트(Execution Context)란 함수를 실행할 때 필요한 조건, 환경정보를 담은 객체이다. 콜 스택(call stack)이란 현재 어떤 함수가 동작중인지, 다음에 어떤 함수가 호출될 예정인지 등을 제어

luka-frontend.tistory.com](https://luka-frontend.tistory.com/39)

environmentRecord는 현재 문맥의 식별자 정보(이름, 함수선언, 변수명)가 수집된다. 실행 컨텍스트가 최초 실행될 때 가장 먼저 하는 일이다. 이것을 다른 말로 **"호이스팅(Hoisting)"**이라고 한다.

**호이스팅(Hoisting)**은 식별자 정보를 실행 컨텍스트의 맨 위로 끌어올린다. 아래 예시 코드를 참고하자.

```
//호이스팅 전
console.log(a());
console.log(b());
console.log(c());

function a() {
  return 'a';
}
let b = function bb() {
  return 'bb';
}
let c = function() {
  return 'c';
}

//호이스팅 후
function a() {
  return 'a';
}
let b;
let c;
console.log(a());
console.log(b());
console.log(c());


b = function bb() {
  return 'bb';
}
c = function() {
  return 'c';
}
```

호이스팅이 완료된 위의 끌어올려진 내용 전체가 **environmentRecord**이다.

실행 컨텍스트가 실행되는 순간에 제일 먼저 하는 일이 바로 **호이스팅(hoisting)**이다.

_중요한 점은, 자바스크립트 엔진이 실제로 변수를 끌어올리지는 않지만, 편의상 끌어올리는 것으로 간주하는 것이다._

한 가지만 더 예를 들어보자

```
function a(x) {
  console.log(x);
  let x;
  console.log(x);
  let x = 2;
  console.log(x);
}
a(1);
```

위 코드는 다음과 같이 볼 수 있다.

```
function a() {
  let x = 1; // 추가된 부분
  console.log(x);
  let x;
  console.log(x);
  let x = 2;
  console.log(x);
}
a()
```

이 상태에서 호이스팅(Hoisting)을 처리해 보겠다.

```
function a() {
  let x;
  let x;
  let x;
  
  x = 1;
  console.log(x); // 1
  console.log(x); // 1
  x = 2;
  console.log(x); // 2
}
a();
```

다음으로는 함수 선언의 호이스팅(Hoisting)을 예를 들어보자.

```
function a() {
  console.log(b);
  let b = 'bbb';
  console.log(b);
  function b() {}
  console.log(b);
}
a();
```

위 코드의 호이스팅이 마친 상태의 코드는 아래와 같다.

```
function a() {
  let b; //변수는 선언부만 끌어올린다.
  function b() {} // 함수 선언은 전체를 끌어올린다.
  
  console.log(b); //b 함수 출력
  b = 'bbb';
  console.log(b); // 'bbb'
  console.log(b); // 'bbb'
}
a();
```

+++ 추가적으로 위의 호이스팅이 끝난 상태에서의 함수 선언문은 함수명으로 선언한 변수에 함수를 할당한 것처럼 여길 수 있어 아래와 같이 표기할 수도 있다.

```
function a() {
  let b
  let b = function b() {} // 바뀐 부분
  
  console.log(b); //b 함수 출력
  b = 'bbb';
  console.log(b); // 'bbb'
  console.log(b); // 'bbb'
}
a();
```

다음으로는 outerEnvironmenetReference와 스코프에 대해서 알아보도록 하자.

---

Ref. 

[코어 자바스크립트](http://www.yes24.com/Product/Goods/78586788) - 정재남