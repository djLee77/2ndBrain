
`Map`객체는 키-값 쌍의 집합이다.

```javascript
const map1 = new Map();

map1.set('a', 1);
map1.set('b', 2);
map1.set('c', 3);

console.log(map1.get('a'));
// Expected output: 1

map1.set('a', 97);

console.log(map1.get('a'));
// Expected output: 97

console.log(map1.size);
// Expected output: 3

map1.delete('b');

console.log(map1.size);
// Expected output: 2

```

Map의 Key type은 String만 가능한 Object와 다르게 모든게 가능하다.
심지어 functions, objects까지도 key로 사용 가능

Map.has(key) 함수는 key로 되어있는 요소가 존재하는지 확인

Map.foreach() 사용법
```javascript
function logMapElements(value, key, map) {
  console.log(`map.get('${key}') = ${value}`);
}
new Map([
  ["foo", 3],
  ["bar", {}],
  ["baz", undefined],
]).forEach(logMapElements);
// Logs:
// "map.get('foo') = 3"
// "map.get('bar') = [object Object]"
// "map.get('baz') = undefined"

```

위를 익명함수로 `Map.foreach((value, key, map) => {})` 와 같이 간단하게 사용할 수 있다.