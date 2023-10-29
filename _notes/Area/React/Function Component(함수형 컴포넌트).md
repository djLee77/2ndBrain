Function Component는 Class Component의 단점을 해결해주는 **불변성**이라는 특징이 있습니다.
함수형 컴포넌트는 의도치 안흔 변화를 방지할 수 있고, 그 내용을 바꾸기 위해서는 새로운 매개변수 값을 넣어서 다시 호출(리렌더링)해야 합니다.

따라서 `this`가 가지고 있는 값이 어떻게 변할지 모르는 Class Component와 달리, Functional Component에선 어떤 값이 불변하다는 확신을 가지고 구현할 수 있습니다.