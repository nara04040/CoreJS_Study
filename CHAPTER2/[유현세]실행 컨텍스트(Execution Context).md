### **실행 컨텍스트(Execution Context)란**

함수를 실행할 때 필요한 조건, 환경정보를 담은 객체이다.

### **콜 스택(call stack)이란**

현재 어떤 함수가 동작중인지, 다음에 어떤 함수가 호출될 예정인지 등을 제어하는 자료구조이다.

이 콜 스택(call stack)에 실행 컨텍스트가 어떤 순서로 쌓이는지 아래 코드를 참고해 보자.

```
var a = 1;                   // 전역 컨텍스트
function outer() {           // outer 컨텍스트
  console.log(a);            // 3
  
  function inner() {         // inner 컨텍스트
    console.log(a);          // undefined
    var a = 3;
  }
  
  inner();
  
  console.log(a);            // 1
}
outer();
console.log(a);              // 1
```

위와 같이 코드를 구성했을 때 실행 컨텍스트의 스택은 다음과 같은 순서로 실행된다.

1\. 프로그램 실행: \[전역컨텍스트\]

2\. outer 실행: \[전역컨텍스트, outer\]

3\. inner 실행: \[전역컨텍스트, outer, inner\]

4\. inner 종료: \[전역컨텍스트, outer\]

5\. outer 종료: \[전역컨텍스트\]

[##_Image|kage@bZzLPd/btrWtd2Ikdh/93mb0Tfu0JLQo7fgELJBQk/img.jpg|CDM|1.3|{"originWidth":1217,"originHeight":590,"style":"alignCenter","width":573,"height":278,"caption":"콜스택 구조","filename":"IMG_147D7538138D-1.jpeg"}_##]

### **실행컨텍스트의 내부 환경**

실행컨텍스트 내부는 다음과 같이 구성되어 있다.

[##_Image|kage@qrmSU/btrWopKCBH2/5FdPD2c5x0KMVOzfX69ask/img.jpg|CDM|1.3|{"originWidth":826,"originHeight":498,"style":"alignCenter","width":566,"height":341,"caption":"활성화된 실행 컨텍스트의 수집 정보","filename":"IMG_11354DE4F665-1.jpeg"}_##]

Variable Environment와 Lexical Environment를 쉽게 구분할 수 있는 방법은 Variable Environment는 오직 식별자 정보를 수집하는 용도로만 쓰이고 Lexical Environment는 각 식별자에 담긴 데이터를 추적하는 용도로 쓰인다. 다시 정리하면

**Variable Environment**: 최초에 식별정보를 가지고 있지만 그 값은 변하지 않는다.

**Lexical Environment**: 실행 컨텍스트의 실행 내용에 따라서 변수 값이 바뀔 때, 변경사항을 계속 트랙킹 한다.

### **Lexical Environment**

Lexical Environment는 어떤 실행 컨텍스트A에 대한 환경정보가 담겨있는 사전이라고 생각하면 쉽다. (ex. 내부식별자 a: 현재 값은 undefined / 내부식별자 b: 현재 값은 20)

**다시 말해 Lexical Environment는 실행컨텍스트를 구성하는 환경 정보들을 모아 사전처럼 구성한 객체이다.**

Lexical Environment는 다음과 같은 정보들로 이루어져 있다.

  **environmentRecord(환경기록)**: 현재문맥의 식별자(hoisting)

  **outerEnvironmentReference**(외부환경 참조): 외부 식별자(scope chain)

다음글을 통해 environmentRecord와 hoisting에 대해서 공부해 보자.

---

Ref. 

코어 자바스크립트 - 정재남