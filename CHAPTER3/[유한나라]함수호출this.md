# 함수로써 호출했을때 this

함수를 호출했을 때 this가 가리키는 것은 2가지이다.

- 브라우저 환경일 때 : Window
- Node.js 환경일 때 : global

```js
var func = function(x){
    console.log(this, x)
};
func(1);    // Window
```


위를 보았을 때 함수 내부에서 this가 가리키는 값도 Window라고 알 수 있다.

