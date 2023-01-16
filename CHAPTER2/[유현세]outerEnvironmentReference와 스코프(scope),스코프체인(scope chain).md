[\>\[Javascript\] environmentRecord와 호이스팅(Hoisting)](https://luka-frontend.tistory.com/40)

 [\[Javascript\] environmentRecord와 호이스팅(Hoisting)

\>\[Javascript\] 실행 컨텍스트 \[Javascript\] 실행 컨텍스트(Execution Context) 실행 컨텍스트(Execution Context)란 함수를 실행할 때 필요한 조건, 환경정보를 담은 객체이다. 콜 스택(call stack)이란 현재 어떤 함수

luka-frontend.tistory.com](https://luka-frontend.tistory.com/40)

**outerEnvironmentReference**란 현재 문맥의 관련 있는 외부 식별자 정보를 참조한다라고 보면 된다.



### 스코프(scope)란

스코프란 식별자에 대한 유효범위를 뜻한다. 어떤 경계 A의 외부에서 선언한 변수는 A의 외부뿐 아니라 A의 내부에서도 접근이 가능하지만, A의 내부에서 선언한 변수는 오직 A의 내부에서만 접근할 수 있다.

이러한 식별자의 유효범위를 바깥으로 차례로 검색해 나가는 것을 **스코프 체인(scope chain)**이라고 한다. 이를 가능하게 하는 것이 곧 **outerEnvironmentReference**이다.

[##_Image|kage@IJ8yA/btrWq9UiZ6K/TQE5RKyJPbV77FnkV0XgD1/img.jpg|CDM|1.3|{"originWidth":829,"originHeight":660,"style":"alignCenter","width":470,"height":374,"caption":"스코프 체인 예시"}_##]

위의 이미지로 예시를 들면

CODE의 outerEnvironmentReference를 통해 BLOCK의 LexicalEnvironment에 접근할 수 있다.

BLOCK의 outerEnvironmentReference를 통해 FUNCTION의 LexicalEnvironment에 접근할 수 있다.

FUNCTION의 outerEnvironmentReference를 통해 GLOBAL의 LexicalEnvironment에 접근할 수 있다.

BLOCK의 outerEnvironmentReference를 통해 CODE의 LexicalEnvironment에 접근할 수 없다.

즉 스코프(scope)는외부로는 나갈 수 있지만, 자기보다 더 안쪽으로는 들어갈 수가 없다. 이게 변수의 유효범위이다.

CODE 함수에서 선언한 변수의 유효범위는 CODE 함수 내부에만 국한이 된다.

---

Ref.

코어 자바스크립트 - 정재남