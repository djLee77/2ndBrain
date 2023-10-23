자바스크립트 호이스팅은 인터프리터가 코드를 실행하기 전에 함수, 변수, 클래스 또는 임포트의 선언문을 해당 범위의 맨 위로 이동시키는 과정을 말한다.

1. 변수가 선언된 줄 이전에 해당 범위에서 변수 값을 사용할 수 있는 경우 ("값 호이스팅")
2. 변수가 선언된 줄 이전에 해당 범위의 변수를 참조할 수 있지만 [`ReferenceError`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/ReferenceError)를 던지지 않고 값이 항상 [`정의되지 않음`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/undefined)인 경우입니다. ("선언 호이스팅")
3. 변수를 선언하면 변수가 선언된 줄 앞의 범위에서 동작이 변경됩니다.
4. 선언의 부작용은 선언이 포함된 나머지 코드를 평가하기 전에 발생합니다