[`String`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String) 타입은 텍스트 데이터를 나타내며, [UTF-16 코드 단위 수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String#utf-16_characters_unicode_code_points_and_grapheme_clusters)를 나타내는 16비트 부호 없는 정수 값의 나열로 인코딩됩니다. String의 각 요소는 String 내부의 위치를 차지합니다. 첫 번째 요소는 인덱스 `0`에, 다음 요소는 인덱스 `1`에 있습니다. String의 [길이](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/length)는 UTF-16 코드 단위의 수이며, 실제 유니코드 문자 수와 일치하지 않을 수 있습니다. 자세한 내용은 [`String`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String#utf-16_characters_unicode_code_points_and_grapheme_clusters) 페이지를 참조하세요.

JavaScript String은 변경할 수 없습니다. 즉, String이 생성되면 수정할 수 없습니다. String 메서드는 현재 String의 내용을 기반으로 새 String을 만듭니다. 예를 들면, 다음과 같습니다.

- [`substring()`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/substring)을 사용해 원래 String의 하위 String을 만들 수 있습니다.
- 연결 연산자(`+`) 또는 [`concat()`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/concat)를 사용하여 두 문자열을 연결합니다.

#### "문자열의 타입화"를 조심하라

문자열을 사용해 복잡한 데이터를 표현하는 것이 매력적으로 보일지도 모르고, 단기적으로는 다음과 같은 장점이 있습니다.

- 연결 연산자를 통해 복잡한 문자열을 쉽게 만들 수 있습니다.
- 문자열은 디버깅이 쉽습니다. (출력 내용이 항상 문자열의 값과 동일)
- 문자열은 많은 API([입력 칸 (en-US)](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement "Currently only available in English (US)"), [로컬 스토리지](https://developer.mozilla.org/ko/docs/Web/API/Web_Storage_API) 값, `responseText`와 함께 사용하는 [`XMLHttpRequest`](https://developer.mozilla.org/ko/docs/Web/API/XMLHttpRequest) 등등)의 공통 분모이며 문자열로만 작업하고 싶을 수 있습니다.

규칙을 통해, 어떤 자료구조라도 문자열로 표현할 수 있습니다. 그러나 그게 좋은 방법은 아닙니다. 예를 들어, 구분자를 사용하면 (물론 JavaScript 배열이 더 적합하겠지만) 문자열로 리스트를 흉내낼 수도 있을 것입니다. 그러나 구분자를 리스트의 요소로 사용하는 순간 리스트가 망가지고 맙니다. 이제 구분자를 구분하기 위해 이스케이프 문자를 선택하고, 등등... 이 모든 것이 각자의 규칙을 필요로 하고 불필요한 유지보수 부담이 발생합니다.

문자열은 텍스트 데이터에만 사용하세요. 복잡한 데이터를 표현해야 할 땐 문자열을 구문 분석하고 적합한 추상화를 사용하세요.

### JavaScript에서 문자열(String)은 iterable한 객체로 간주됩니다. 

따라서 spread 연산자를 사용하여 문자열의 각 문자(character)를 개별 요소로 하는 배열을 생성할 수 있습니다.

때문에 JavaScript에서는 문자열(string)을 배열처럼 인덱스를 사용해서 각 문자에 접근할 수 있습니다. 따라서, 문자열에 대해서도 인덱스를 통한 접근이 가능합니다.

예를 들어, 문자열 `'123'`이 있을 때, `'123'[0]`은 `'1'`을 반환하고, `'123'[1]`은 `'2'`를 반환합니다.

추가적으로 new Set(string), ...string 등 iterable한 객체들에 적용 가능한 것들을 모두 적용할 수 있습니다.



wrapper 객체 내장함수

[[String.indexOf(), String.includes()]] -문자열 포함여부 확인하는 법

string.startsWith( 탐색할 문자열, index );

```javascript
const str = "Tom is thinking";
const name = "Tom";
console.log(str.startsWith(name)); // true
```

string.endsWith(탐색할 문자열);