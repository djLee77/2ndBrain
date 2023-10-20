* 콜백 함수는 다른 함수에 인수로 전달되는 함수이다.
* 이 기술을 사용하면 함수가 다른 함수를 호출할 수 있다.
* 콜백 함수는 다른 함수가 완료된 후에 실행될 수 있다.

예시
```javascript
function myDisplayer(some) {  
  document.getElementById("demo").innerHTML = some;  
}  
  
function myCalculator(num1, num2, myCallback) {  
  let sum = num1 + num2;  
  myCallback(sum);  
}  
  
myCalculator(5, 5, myDisplayer);
```
위 예시에서는 myDisplayer가 콜백 함수가 된다.

이렇게 되면 myCalculator의 코드들이 전부 실행된 뒤에 콜백 함수인 myCallback이 실행되도록 구현할 수 있다.