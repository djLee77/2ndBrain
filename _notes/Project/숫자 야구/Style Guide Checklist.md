### 2. References

- [ ] 2. var의 사용을 피하고 되도록 const사용, 값을 바꿔야하다면 let을 사용해라. 

---
### 3. Objects

- [ ] 3-1. Object를 만들 떄는 literal 문법을 사용할 것

```javascript
//bad
const item = new Object();

//good
const item = {};
```

- [ ] 3-2. 동적인 이름의 속성을 추가할 때는 아래와 같이할 것
```javascript
function getKey(k) {
  return `a key named ${k}`;
}

//bad
const obj = {
  id: 5,
  name: 'San Francisco',
};

obj[getKey('enabled')] = true;

//good
const obj = {
  id: 5,
  name: 'San Francisco',
  [getKey('enabled')]: true,
};
```

- [ ] 3-3. 함수를 객체의 속성으로 추가할 때
```javascript
//bad
const atom = {
  value: 1,

  addValue: function (value) {
    return atom.value + value;
  },
};

//good
const atom = {
  value: 1,

  addValue(value) {
    return atom.value + value;
  },
};
```

- [ ] 3-4. 객체의 key와 value의 변수명이 동일할 때는 아래와 같이 작성할 것
```javascript
const lukeSkywalker = 'Luke Skywalker';

//bad
const obj = {
  lukeSkywalker: lukeSkywalker,
};

//good
const obj = {
  lukeSkywalker,
};
```

- [ ] 3-5. 객체를 선언할 때, value의 type에 따라 그룹화할 것
```javascript
const anakinSkywalker = 'Anakin Skywalker';
const lukeSkywalker = 'Luke Skywalker';

//bad
const obj = {
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  lukeSkywalker,
  episodeThree: 3,
  mayTheFourth: 4,
  anakinSkywalker,
};

//good
const obj = {
  lukeSkywalker,
  anakinSkywalker,
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  episodeThree: 3,
  mayTheFourth: 4,
};
```

- [ ] 3-6. key는 유효하지 않은 식별자일 경우만 ''를 사용할 것
```javascript
// bad
const bad = {
  'foo': 3,
  'bar': 4,
  'data-blah': 5,
};

// good
const good = {
  foo: 3,
  bar: 4,
  'data-blah': 5,
};
```

- [ ] 3-7. 객체의 프로토타입 메소드를 직접 호출하지 말 것
	이유 1 : 특정 객체가 'hasOwnPropert'라는 속성을 직접 가지고 있을 수 있기 때문
	이유 2 : `Object.creat(null)`을  통해 생성된 객체는 프로토타입이 없기 때문에 `hasOwnPropert`와 같은 메소드를 호출할 수 없다.
```javascript
// bad
console.log(obj.hasOwnProperty(key));

// good
console.log(Object.prototype.hasOwnProperty.call(obj, key));

// better
const has = Object.prototype.hasOwnProperty; // cache the lookup once, in module scope.
console.log(has.call(obj, key));

// best
console.log(Object.hasOwn(obj, key)); // only supported in browsers that support ES2022

/* or */
import has from 'has'; // https://www.npmjs.com/package/has
console.log(has(obj, key));
/* or */
console.log(Object.hasOwn(obj, key)); // https://www.npmjs.com/package/object.hasown
```

- [ ] 3-8. 객체를 얕게 복사할때는 assign 대신 스프레드 구문을 사용할 것
```javascript
// very bad
const original = { a: 1, b: 2 };
const copy = Object.assign(original, { c: 3 }); // 이렇게 생성하면
delete copy.a; // 이렇게 복사된 객체를 수정하게되면 원본 객체에도 수정이 반영되버린다.

// bad
const original = { a: 1, b: 2 };
const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }
//이렇게 하면 얕게 복사는 되지만 코드 가독성이 떨어진다.

// good
const original = { a: 1, b: 2 };
const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
```

---

### 4. Arrays

- [ ] 4-1. 배열을 선언할 때 literal 문법을 사용한다.
```javascript
// bad
const items = new Array();

// good
const items = [];
```

- [ ] 4-2. 배열에 값을 추가할 때는 push() 사용
```javascript
const someStack = [];

// bad
someStack[someStack.length] = 'abracadabra';

// good
someStack.push('abracadabra');
```

- [ ] 4-3. 배열을 복사할 때 spread 연산을 사용
```javascript
// bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i < len; i += 1) {
  itemsCopy[i] = items[i];
}

// good
const itemsCopy = [...items];
```

- [ ] 4-4. iterable object 를 배열로 변환할 때도 from()대신 spread를 사용
```javascript
const foo = document.querySelectorAll('.foo');

// good
const nodes = Array.from(foo);

// best
const nodes = [...foo];
```

- [ ] 4-5. 객체의 배열같은 부분을 배열로 전환할때는 `Array.from`을 사용
```javascript
const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 };

// bad
const arr = Array.prototype.slice.call(arrLike);

// good
const arr = Array.from(arrLike);

// result
['foo', 'bar', 'baz']
```

- [ ] 4-6. `mapping`으로 새로운 배열을 생성할 때 `Array.from`을 대신 사용
	`mapping`을 사용하게 되면 중간에 중간 배열을 한번 생성하기 때문
```javascript
const foo = {1, 2, 3};
const bar = num => num * 2;

// bad
const baz1 = [...foo].map(bar); // => [2, 4, 6]

// good
const baz2 = Array.from(foo, bar); // => [2, 4, 6]

```

- [ ] 4-7. 배열의 메소드 콜백에서 반드시 return값을 갖도록 해라.
```javascript
// good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;
});

// good - 화살표 함수는 결과를 바로 반환한다.
[1, 2, 3].map((x) => x + 1);

// bad - no returned value means `acc` becomes undefined after the first iteration
[[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
  const flatten = acc.concat(item);
});

// good
[[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
  const flatten = acc.concat(item);
  return flatten;
});

// bad
inbox.filter((msg) => {
  const { subject, author } = msg;
  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  } else {
    return false;
  }
});

// good
inbox.filter((msg) => {
  const { subject, author } = msg;
  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  }

  return false;
});
```

- [ ] 4-8. 아래와 같이 줄바꿈을 가독성이 좋게 사용
```javascript
// bad
const arr = [
  [0, 1], [2, 3], [4, 5],
];

const objectInArray = [{
  id: 1,
}, {
  id: 2,
}];

const numberInArray = [
  1, 2,
];

// good
const arr = [[0, 1], [2, 3], [4, 5]];

const objectInArray = [
  {
    id: 1,
  },
  {
    id: 2,
  },
];

const numberInArray = [
  1,
  2,
];
```

---

### 5. Destructuring(구조 분해)

- [ ] 5-1. 아래와 같이 구조분해를 통해 속성에 접근할 것
```javascript
// bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;

  return `${firstName} ${lastName}`;
}

// good
function getFullName(user) {
  const { firstName, lastName } = user;
  return `${firstName} ${lastName}`;
}

// best
function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`;
}


const user = {
  firstName: "John",
  lastName: "Doe"
};

console.log(getFullName(user));  // "John Doe" 라는 결과가 출력됩니다.

```

- [ ] 5-2. 배열 destructuring을 사용
```javascript
const arr = [1, 2, 3, 4];

// bad
const first = arr[0];
const second = arr[1];

// good
const [first, second] = arr;
```

- [ ] 5-3. 여러값을 return 할 때는 배열 destructuring 대신, 객체 destructuring을 사용
```javascript
// bad
function processInput(input) {
  // then a miracle occurs
  return [left, right, top, bottom];
}

// the caller needs to think about the order of return data
const [left, __, top] = processInput(input);

// good
function processInput(input) {
  // then a miracle occurs
  return { left, right, top, bottom };
}

// the caller selects only the data they need
const { left, top } = processInput(input);
```

---

### 6. Strings

- [ ] 6-1.  `''`을 사용할 것
```javascript
// bad
const name = "Capt. Janeway";

// bad - template literals should contain interpolation or newlines
const name = `Capt. Janeway`;

// good
const name = 'Capt. Janeway';
```
- [ ] 6-2. 여러줄로 나눠 작성하지 말기
```javascript
// bad
const errorMessage = 'This is a super long error that was thrown because \
of Batman. When you stop to think about how Batman had anything to do \
with this, you would get nowhere \
fast.';

// bad
const errorMessage = 'This is a super long error that was thrown because ' +
  'of Batman. When you stop to think about how Batman had anything to do ' +
  'with this, you would get nowhere fast.';

// good
const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
```

- [ ] 6-3. Template String \`\`  사용
```javascript
// bad
function sayHi(name) {
  return 'How are you, ' + name + '?';
}

// bad
function sayHi(name) {
  return ['How are you, ', name, '?'].join();
}

// bad
function sayHi(name) {
  return `How are you, ${ name }?`;
}

// good
function sayHi(name) {
  return `How are you, ${name}?`;
}
```

- [ ] 6-4. eval() 사용 금지

- [ ] 6-5. 불필요한 이스케이프 금지
```javascript
// bad
const foo = '\'this\' \i\s \"quoted\"';

// good
const foo = '\'this\' is "quoted"';
const foo = `my name is '${name}'`;
```

---

### 7. function

- [ ] 7-1.. 함수 선언 대신 명명된 함수 이름 표현 사용 ([[함수를 정의하는 법]] 참고)
	메소드에는 해당하지 않는 규칙이다. ([[함수와 메소드의 차이]] 참고)
```javascript
// bad
function foo() {
  // ...
}

// bad
const foo = function () {
  // ...
};

// good
// lexical name distinguished from the variable-referenced invocation(s)
const short = function longUniqueMoreDescriptiveLexicalFoo() {
  // ...
};
```

- [ ] 7-2. [[IIFE(즉시 실행 함수 표현식)]]은 괄호로 감싼다.
```js
// immediately-invoked function expression (IIFE)
(function () {
  console.log('Welcome to the Internet. Please follow me.');
}());
```

- [ ] 7-3. `if`, `for` 문과 같은 곳의 블록 안에서 함수를 정의하지 마시오.
```js
for (var i = 0; i < 10; i++) {
    funcs[i] = function() {
        return i;
    };
}
```

- [ ] 7-4. ECMA-262는 블록을 명령문의 목록으로 정의합니다. 그러나 함수 선언은 명령문이 아닙니다. 이것은 함수 선언이 블록 내에서 예상대로 작동하지 않을 수 있음을 의미합니다.
```javascript
// bad
if (currentUser) {
  function test() {
    console.log('Nope.');
  }
}

// good
let test;
if (currentUser) {
  test = () => {
    console.log('Yup.');
  };
}
```

- [ ] 7-5. 매개 변수명에 arguments 사용금지. (모든 함수는 arguments라는 지역 객체에 접근이 가능하) 
```js
// bad
function foo(name, options, arguments) {
  // ...
}

// good
function foo(name, options, args) {
  // ...
}
```

- [ ] 7-6. 매개변수에 입력한 여러개의 인자들을 메소드 내에서 배열로 다루는법
```js
// bad
function concatenateAll() {
  const args = Array.prototype.slice.call(arguments);
  return args.join('');
}

// good
function concatenateAll(...args) {
  return args.join('');
}
```

- [ ] 