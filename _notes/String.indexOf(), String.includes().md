indexOf : > string.**indexOf**(searchvalue, position)
- indexOf 함수는, 문자열(string)에서 특정 문자열(searchvalue)을 찾고,   
    검색된 문자열이 '첫번째'로 나타나는 [위치] index를 리턴합니다.

1. [String.indexOf()] : 문자열에 특정 문자열이 포함되어 있는지 확인
```javascript
const str = 'Hello, World, Javascript';

if(str.indexOf('Hello') != -1){
	console.log("exist Hello")
}
```
 포함되어 있으면 1, 포함되어 있지 않으면 -1을 반환한.

2. [String.includes()] : 문자열에 특정 문자열이 포함되어 있는지 확인
```javascript
const str = 'Hello, World, Javascript';

if(str.includes('Hello') != -1){
	console.log("exist Hello")
}
```
 [true, false]로 반환한다.