JavaScript의 this는 **함수의 호출 방식**에 따라서 this에 바인딩 할 객체가 동적으로 결정됩니다.

1. 전역공간일 때
2. 함수호출
3. 메서드 호출
4. 생성자 함수 호출
5. apply / call / bind 호출



# 전역에서 this를 사용했을 때

브라우저 상인 전역 공간에서의 this는 항상 전역 객체인 Window를 참조한다.(node상에서는 global)
