JavaScript에서 객체의 "특성(attribute)"은 대체로 객체의 메타 정보와 관련이 있습니다. 예를 들면, 속성은 객체의 프로퍼티가 변경 가능한지, 열거 가능한지, 설정 가능한지 등의 정보를 담고 있습니다.

객체의 각 프로퍼티에는 아래와 같은 특성(attribute)들이 있습니다:

1. **[[Value]]**: 프로퍼티의 실제 값입니다.
2. **[[Writable]]**: 이 속성이 `true`일 경우, 해당 프로퍼티의 값은 수정될 수 있습니다.
3. **[[Enumerable]]**: 이 속성이 `true`일 경우, 해당 프로퍼티는 for...in 루프나 Object.keys() 메서드에 의해 열거될 수 있습니다.
4. **[[Configurable]]**: 이 속성이 `true`일 경우, 해당 프로퍼티는 삭제될 수 있고, 속성의 값들도 수정될 수 있습니다.
5. **[[Get]]**: 특정 프로퍼티에 getter 함수가 있다면 이 속성에 저장됩니다.
6. **[[Set]]**: 특정 프로퍼티에 setter 함수가 있다면 이 속성에 저장됩니다.

```Javascript
let obj = {
    myProperty: "Hello"
};

let descriptor = Object.getOwnPropertyDescriptor(obj, 'myProperty');
console.log(descriptor);
// {
//    value: 'Hello',
//    writable: true,
//    enumerable: true,
//    configurable: true
// }

```