`call`과 `apply`는 Javascript 함수에서 제공하는 함수를 호출하는데 사용되는 메서드이다.

그리고 둘 다 함수를 호출할 때 `this` 값을 지정할 수 있게 해줍니다.
### call

`call` 메서드는 첫 번째 인자로 `this` 값으로 사용될 객체를 받고, 그 이후의 인자들은 호출할 함수의 파라미터로 전달됩니다.

```javascript
function greet(greeting, punctuation) {
  console.log(greeting + ', ' + this.name + punctuation);
}

const person = {
  name: 'Alice'
};

greet.call(person, 'Hello', '!'); // 출력: "Hello, Alice!"

```

위 예제에서 `greet` 함수는 `call` 메서드를 사용해 호출되며, `this` 값은 `person` 객체로 지정됩니다. 따라서 함수 내에서 `this.name`은 `Alice`를 참조합니다.

### apply

`apply` 메서드는 `call`과 비슷하지만, 함수에 전달될 인자들을 배열로 받습니다. 첫 번째 인자는 `this` 값으로 사용될 객체입니다.

```js
function greet(greeting, punctuation) {
  console.log(greeting + ', ' + this.name + punctuation);
}

const person = {
  name: 'Alice'
};

greet.apply(person, ['Hello', '!']); // 출력: "Hello, Alice!"

```

`apply`를 사용할 때, 함수의 인자들은 배열의 요소로 전달됩니다. 이는 가변 인자를 가진 함수를 다룰 때 특히 유용합니다.

### call vs apply

두 메서드의 주요 차이점은 함수의 인자를 어떻게 전달하는지에 있습니다:

- `call`은 인자들을 개별적으로 전달합니다.
- `apply`는 인자들을 배열로 전달합니다.

기능적으로는 두 메서드는 동일합니다. 어느 것을 사용할지는 주로 인자들이 어떤 형태로 주어져 있는지에 따라 결정됩니다. 배열 형태로 인자들이 주어지면 `apply`를, 그렇지 않으면 `call`을 사용하면 됩니다.