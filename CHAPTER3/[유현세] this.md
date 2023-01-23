### **this의 값은 함수를 호출한 방법에 의해 결정된다.**

[##_Image|kage@ynZFF/btrWCIW49OE/EbYKFPlVDiHaq0sDvp6ZyK/img.jpg|CDM|1.3|{"originWidth":826,"originHeight":498,"style":"alignCenter","width":672,"height":405,"filename":"IMG_11354DE4F665-1.jpeg"}_##]

ThisBinding은 실행컨텍스트가 실행되는 순간에 this를 바인딩한다라는 뜻이다. 따라서 this의 값은 함수를 호출될 때 함께 결정된다.

**_바인딩: 구성 요소의 실제 값 또는 프로퍼티를 결정짓는 행위_**

호출하는 방식은 다음과 같이 분류된다.

1.  전역공간에서: window / global
2.  함수 호출시: window / global
3.  메서드 호출시: 메서드 호출 주체(메서드명 앞)
4.  callback 호출 시: 기본적으로는 함수내부에서와 동일
5.  생성자 함수 호출시: 인스턴스 

**\*arrow function은 this를 바인딩하지 않는다.**

### **1\. 전역 공간에서의 this**

전역 공간에서는 전역 컨텍스트를 생성하는 주체가 전역 객체이기 때문에 this는 이 전역 객체를 가리키게 된다. 브라우저 환경에서의 전역객체는 window, Node.js 환경에서는 global이다.

```js
//전역 공간(브라우저)
console.log(this) // {alert: f(),...}
console.log(this === window) // true

//전역 공간(Node.js)
console.log(this) // {process: {title: 'node',...}}
console.log(this === global) // true
```

전역변수를 선언하면 자바스크립트 엔진은 이를 전역객체의 프로퍼티로도 할당한다.

```js
// 전역 공간(브라우저)
const a = 1;
console.log(a); // 1
console.log(window.a); // 1
console.log(this.a); // 1
```

### **2\. 함수로서 호출할 때 함수 내부에서의 this**

조금 이상하긴 하지만 함수를 호출하는 순간에 실행해주는 주체가 전역 공간이기 때문에 호출한 대상이 전역 객체가 된다.

```js
function a() {
 console.log(this);
}
a(); // Window {...}
```

하지만 아래와 같은 예외적인? 이해할 수 없는 경우도 존재한다.

```js
function b() {
  function c() {
    console.log(this);
  }
  c(); // Window {...}
}
b(); // Window {...}
```

b 함수 내부에서의 this는 전역 객체라고 쳐도 c함수는 b함수라고 봐야 할 것 같은 상황인데도 위와 같이 전역 객체가 나온다.

이런 버그 같은 문제들 때문에 ES6에서는 아예 this를 바인딩하지 않는 arrow function이 나왔다.

### **3\. 메서드로서 호출할 때 메서드 내부에서의 this**

메서드로서 호출했을 때의 this는 메서드를 호출한 주체가 된다.(점 앞을 보면 된다)

```js
const car = {
  name: 'MINI',
  getName: function() {
    console.log(this);
  }
}

car.getName() // {name: 'MINI', getName: f}
```

원래는 함수인데 '어떤 객체'와 관련된 동작을 하게 되면 그때는 메서드라고 부른다. 여기서의 '어떤 객체'가 바로 점 앞이 되는 것이다.

### **4\. 콜백 함수 호출 시  그 함수 내부에서의 this**

콜백함수 호출 시 내부에서의 this 값은 '무조건 이거다'라고 정의할 수 없다. 콜백 함수의 제어권을 가지는 함수나 메서드가 콜백 함수에서의 this를 무엇으로 할지 결정한다. 

```js
// 1번 예제
setTimeOut(
  funtion() { 
    console.log(this);
  }, 300
); // Window{...}

// 2번 예제
document.body.innerHTML += `<button id="a">클릭</button>`;
document.body.querySelector("#a")
  .addEventListener('click', function (e) {
    console.log(this); // <button id="a">클릭</button>
  });
```

### **5\. 생성자 함수 호출 시  생성자 함수 내부에서의 this**

new 명령어와 함께 생성자 함수를 호출하면 해당 함수가 생성자로서 동작하게 된다. 그리고 어떤 함수가 생성자 함수로서 호출된 경우 내부에서의 this는 곧 새로 만들 구체적인 인스턴스 자신이 된다.

```js
function person(n,a) {
  this.name = n;
  this.age = a;
}

const newRoy = new person('luka', 30);
const roy = person('rooney', 40);

console.log(newRoy); // person {name: 'luka', age: 30}
console.log(window.name, window.age); // rooney 40
```

---

### **명시적으로 this를 바인딩하는 방법**

#### **1\. call 메서드**

call 메서드는 메서드의 호출 주체인 함수를 즉시 실행하도록 하는 명령이다.

```js
const func = function(a, b, c) {
  console.log(this, a, b, c);
};

func(1, 2, 3); // Window{...} 1 2 3
func.call({ x: 1 }, 4, 5, 6); // { x: 1 } 4 5 6
```

#### **2\. apply 메서드**

apply 메서드는 call 메서드와 기능적으로는 완전히 동일하지만 두 번째 인자는 배열로 받아, 그 배열의 요소들을 호출할 함수의 매개변수로 지정한다.

```js
const func = function(a, b, c) {
  console.log(this, a, b, c);
};

func(1, 2, 3); // Window{...} 1 2 3
func.call({ x: 1 }, [4, 5, 6]); // { x: 1 } 4 5 6
```

#### **3\. bind 메서드**

bind 메서드는 ES5에 추가된 기능으로, call과 비슷하지만 즉시 호출하지는 않고 넘겨받은 this 및 인수들을 바탕으로 새로운 함수를 반환하기만 하는 메서드이다. 다시 새로운 함수를 호출할 때 인수를 넘기면 그 인수들은 기존 bind 메서드를 호출할 때 전달했던 인수들의 뒤에 이어서 등록된다.

```js
const func = function(a, b, c, d) {
  console.log(this, a, b, c, d);
};
func(1, 2, 3, 4); // Window{...} 1 2 3 4

const bindFunc = func.bind({ x : 1 });
bindFunc(5, 6, 7, 8); // { x : 1 } 5 6 7 8
```

---

ref.

**코어자바스크립트 - 정재남**

[##_Image|kage@dBf97C/btrWZW7Ash7/aX1UfBZJpqCXXbKwJCGYk1/img.jpg|CDM|1.3|{"originWidth":850,"originHeight":478,"style":"alignLeft","width":299}_##]