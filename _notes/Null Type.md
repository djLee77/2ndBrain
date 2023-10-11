null이라는 하나의 값만 가질 수 잇음

`undefined`와 달리 객체가 없음을 나타내는 특별한 값이다.

예를 들면, 어떤 변수가 객체를 가리키길 원하나 현재는 어떤 객체도 가리키지 않을 때 'null' 값을 할당할 수 있습니다.

```javascript
let user = null; //현재 user는 아무 객체도 가리키지 않음.

let info = {
	name : "이대준",
	age : 24,
	sex : male,
}

user = info;
```

JavaScript의 `typeof` 연산자는 값의 타입을 문자열로 반환합니다. 그러나, `null` 값에 대해 `typeof` 연산자를 사용하면, 예상과 다르게 `"object"`라는 결과가 반환됩니다.

```javascript
console.log(typeof null);  // "object"
```

이것은 JavaScript의 오래된 버그로 알려져 있으나, 이를 수정하면 많은 기존 코드가 깨질 수 있기 때문에 이 버그는 그대로 유지되고 있습니다