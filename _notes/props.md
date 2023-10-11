	Props란 무엇인가
props란 상위 컴포넌트가 하위 컴포넌트에 값을 전달할 때 사용하는 속성이다.

상위 컴포넌트가 하위 컴포넌트에 값을 전달하기 때문에 단방향 데이터 흐름을 갖는다.

부모 컴포넌트는 수정 가능하지만, 자식 컴포넌트는 읽기만 가능하다.

상위 컴포넌트 - App.js
```
 function App() {
	 return(
		 <div>
			 <Card 
			 person = {객체}
		     size = 90
		     color = "red"
		     />
		 </div>
	 )
 }
```

하위 컴포넌트 - Card.js
```
function Card(props){
	return(
		<div>
			{props.person}, {props.size}, {props.color}
		</div>
	)
}
```