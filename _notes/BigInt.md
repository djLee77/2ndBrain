BigInt 타입은 임의 정밀도로 정수를 나타낼 수 있는 JavaScript 숫자 원시 값입니다. BigInt로 Number의 안전한 정수 제한(`Number.MAX SAFE INTEGER`)을 넘어서는 큰 정수도 안전하게 저장하고 연산할 수 있습니다.

BigInt는 정수 끝에 `n`을 추가하거나 `BigInt()`함수를 호출해 생성할 수 있습니다.

다음 예제는 `Number.Max SAFE INTEGER`를 증가시키면, 예상된 값을 반환하는 것을 보여줍니다.

```Javascript
// BigInt
const x = BigInt(Number.MAX_SAFE_INTEGER); // 9007199254740991n
x + 1n === x + 2n; // 9007199254740992n는 9007199254740993n과 같지 않아 false입니다.

// Number
Number.MAX_SAFE_INTEGER + 1 === Number.MAX_SAFE_INTEGER + 2; // 둘 다 9007199254740992 이기 때문에 true입니다.
```
BigInt는 소수를 나타낼 수 없지만, 큰 정수를 더 정확하게 나타낼 수 있기 때문에, BigInt 값은 숫자보다 항상 더 정확하거나 덜 정확하지 않습니다. 어떤 타입도 다른 타입을 수반하지 않으며, 서로 대체할 수 없습니다. 
`TypeError`는 BigInt 값이 산술 표현식의 일반 숫자와 혼합되거나 서로 암시적으로 변환되는 경우 발생합니다.
