객체란 Javascript만이 가지고 있는 특징의 기초를 이루는 자료형으로 많은 기능을 내장하고 있다.

```javascript
var result = {name: "soyoon"}
```

중괄호 '{}'안에 key : value 형식으로 프로퍼티를 저장한다. 프로퍼티란 객체에 속한 데이터를 뜻한다.

객체 속성 값을 읽는 방법은 점 표기범([[dot notation]])과 대괄호 표기법([[bracket notation]])이 있다.

	대괄호 표기법
```javascript
javascript
let obj = {
  fruit : "favorite fruit",
  "favorite fruit" : {
  apple : "first",
  peach : "second",
  banana : "third"
  }
};

// 속성 추가
obj["stock"] = 100;
console.log(obj["stock"]);//  100

// 속성 값 변경
obj["fruit"] = "soyoon";
console.log(obj["fruit"]); //  "soyoon"

console.log(obj);

/*  favorite fruit: {
    apple: "first",
    banana: "third",
    peach: "second"
  },
  fruit: "soyoon",
  stock: 100
}
*/
```

	점 표기법
```javascript
javascript
let obj = {
  fruit : "favorite fruit",
  "favorite fruit" : {
  apple : "first",
  peach : "second",
  banana : "third"
  }
};

// 속성 추가
obj.stock = 100;
console.log(obj.stock);  //  100

// 속성 값 변경
obj.fruit = "soyoon";
console.log(obj.fruit);  //  "soyoon"

console.log(obj);

/*  favorite fruit: {
    apple: "first",
    banana: "third",
    peach: "second"
  },
  fruit: "soyoon",
  stock: 100
}
*/
```

> [!NOTE] 
> **dot notation 은 key값이 동적으로 변할 때 사용에 한계**가 있으며,  
숫자로 시작할 수 없고, 변수를 포함할 수 없음.  
**bracket notation 은 key값이 변수일 때 주로 사용**하며  
숫자, 변수, 공백 모두 사용할 수 있음.

[[Object-foreach]] - Object를 이용한 foreach문

