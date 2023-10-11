[[원시값]]

Type|typeof return value|Object wrapper
:---|:---:|---:
[[Null Type]] Type|`"object"`|N/A
[[Undefined Type]] Type|`"undefined"`|N/A
[[Boolean]] Type|`"boolean"`|`Boolean`
[[Number]] Type|`"number"`|`Number`
[[BigInt]] Type|`"bigint"`|`BigInt`
[[String]] Type|`"string"`|`String`
[[Symbol]] Type|`"symbol"`|`Symbol`

객체
---------
1. 컴퓨터 과학에서의 객체([[Object]]) 란 참조할 수 있는 메모리 상의 값을 말합니다. JavaScript에서 객체는 유일한 변경 가능한 값입니다. Functions는 사실 callable이라는 추가 기능이 있는 객체이기도 합니다.

2. 프로퍼티 - Javascript에서의 객체는 프로퍼티의 컬렉션으로 볼 수 있습니다. 객체 레터럴 구문을 사용해 제한적으로 속성을 초기화할 수 있고, 그 후에 속성을 추가하거나 제거할 수도 있습니다. 객체 속성은 키-값 쌍과 동일합니다. 프로퍼티 값으로는 다른 객체를 포함해 모든 타입을 사용할 수 있으므로 복잡한 자료구조의 구축이 가능합니다. KEY로는 [[String]]타입 또는 [[Symbol]]타입이 될 수 있습니다.

4. 객체 속성에는 [[데이터 속성]]과 [[접근자 속성]] 두 종류가 있습니다. 각각의 속성에는 다시 `attribute`들이 존재합니다. `attribute`([[객체의 attribute]])은 JavaScript 엔진 내부에서는 접근되지만, `Object.defineProperty)` 를 통해 설정하거나, `Object.getOwnPropertyDescriptor()`를 통해 읽을 수 있습니다. - [[Object.defineProperty()]]란?

Key 컬렉션
-------------------
- [[Map]] 이란

- [[Set]]  이란


