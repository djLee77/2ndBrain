`undefined` 라는 하나의 값만 가질 수 있다.

개념적으로, `undefined` 는 값이 없음을 의미하고, [[Null Type]]은 객체가 없음을 의미합니다. (typeof null === "object"에 대한 변명이 될 수 있습니다.) 일반적으로 값이 없는 경우 언어의 기본값은 undefiend입니다.

- 반환 값이 없는 return 문은 암시적으로 undefined를 반환합니다.
- 존재하지 않는 객체 속성에 접근 (obj.iDontExist)하면 undefined가 반환됩니다.
- 초기화(let x;)가 없는 변수 선언은 변수를 undefined로 암시적으로 초기화합니다.
- Array.prototype.find() 및 Map.prototype.get() 와 같은 대부분의 메서드는, 요소를 찾을 수 없을 때 undefined를 반환합니다.