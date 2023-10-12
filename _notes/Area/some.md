`some()` 함수는 JavaScript의 배열 메서드 중 하나로, 배열의 요소 중 어떤 요소가 주어진 함수의 테스트를 통과하는지 테스트합니다. 반환 값은 불리언(Boolean) 타입으로, 배열의 어떤 요소가 주어진 함수의 조건을 만족하면 `true`를 반환하고, 아니면 `false`를 반환합니다.

```javascript
arr.some(callback(element[, index[, array]])[, thisArg])
```


ex1) 짝수가 존재하는지 확인
```javascript
const numbers = [1, 3, 5, 7, 9];
const hasEvenNumber = numbers.some(num => num % 2 === 0);
console.log(hasEvenNumber);  // false
```

ex2) 배열에 특정 값을 포함하는지 확인하기
```javascript
const fruits = ['apple', 'banana', 'mango', 'cherry'];
const hasMango = fruits.some(fruit => fruit === 'mango');
console.log(hasMango);  // true
```
