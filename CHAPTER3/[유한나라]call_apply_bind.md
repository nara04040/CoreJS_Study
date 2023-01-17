## Function.prototype.call(thisArg[, arg1[, arg2[, ...]]])

call 메서드는 호출 주체인 함수를 즉시 실행하는 명령이다.

call 메서드의 첫 인자를 this로 바인딩한다. 이후의 인자들은 호출할 함수의 매개변수로 한다.

<br>

```js
var func = function (a,b,c){
    console.log(this,a,b,c);
};

func(1,2,3);    // Window , 1 2 3
func.call({x:1}, 4, 5, 6)   // {x : 1} 4 5 6
```

객체를 메서드를 그냥 호출한다면 this는 객체를 참조하지 않는다.

하지만 call 메서드를 이용한다면 객체를 this를 지정할 수 있다.

```js
var obj = {
    a: 1,
    method: function (x,y) {
        console.log(this.a, x, y);
    }
};

obj.method(2,3);    // 1 2 3
obj.method.call({a:4}, 5, 6);   // 4 5 6
```

<br>
<br>

## Function.prototype.apply(thisArg[, argsArray])

apply 메서드는 call메서드와 기능적으로는 완전 동일하다.

하지만 call 메서드는 첫 인자를 제외한 나머지 모든 인자를 매개변수로 지정한다.

apply메서드는 두 번째 인자를 배열로 받아 배열의 요소를 호출할 함수의 매개변수로 지정한다.


<br>
<br>

## Function.prototype.bind(thisArg[, arg1[, arg2[, ...]]])

call과 비슷하지만 즉시 호출이 아닌 넘겨 받은 this, 인수들을 바탕으로 **새로운 함수를 반환하는 메서드이다.**

다시 새로운 함수를 호출할 때 인수를 넘긴다면 인수들은 bind메서드를 호출할 때 전달했 던 인수들의 뒤에 이어서 등록합니다.