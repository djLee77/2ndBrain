**즉시 실행 함수 표현식(Immediately Invoked Function Expression, IIFE)** 은 함수를 정의한 즉시 호출하는 JavaScript 패턴입니다. IIFE는 전역 범위에서 변수를 보호하거나 코드의 다른 부분과 충돌을 방지하기 위해 사용되곤 했습니다.

```javascript
(function () {
  console.log('This will run immediately upon definition.');
}());
```

IIFE를 사용하는 주요 이유는:

1. **변수 범위 제한**: IIFE 내부의 변수들은 외부 범위에서 접근할 수 없습니다. 이로 인해 변수 충돌의 가능성이 줄어듭니다.
2. **즉시 실행**: 함수를 정의하자마자 즉시 실행하므로 별도의 함수 호출이 필요 없습니다.

IIFE를 사용할 때 괄호로 묶는 이유:

1. **가독성**: IIFE는 단일 유닛으로 간주되므로 괄호로 둘러싸는 것이 이를 명확하게 표현합니다.
2. **구문 오류 방지**: JavaScript는 함수 선언 다음에 바로 괄호가 오는 것을 허용하지 않습니다. 그렇기 때문에 함수 표현식을 괄호로 둘러싸면 IIFE를 제대로 작동하게 만들 수 있습니다.