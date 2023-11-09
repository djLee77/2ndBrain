```js
class CoffeeMachine {

  #waterLimit = 200;

  #checkWater(value) {
    if (value < 0) throw new Error("물의 양은 음수가 될 수 없습니다.");

    if (value > this.#waterLimit) throw new Error("물이 용량을 초과합니다.");
  }
}

let coffeeMachine = new CoffeeMachine();

// 클래스 외부에서 private에 접근할 수 없음
coffeeMachine.#checkWater(); // Error
coffeeMachine.#waterLimit = 1000; // Error
```

`#`은 자바스크립트에서 지원하는 문법으로, private 필드를 의미합니다. private 필드는 클래스 외부나 자손 클래스에서 접근할 수 없습니다.

오직 같은 클래스 내의 다른 메서드에서만 접근이 가능하고, 다른 클래스에서 private 필드를 다루기 위해서는 getter setter를 사용해야 합니다.