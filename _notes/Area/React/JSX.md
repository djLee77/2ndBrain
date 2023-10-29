1.JSX란?
JSX (Javascript XML)는 [[Javascript]]에 XML을 추가한 확장 문법이다.
JSX는 리액트로 프로젝트를 개발할 때 사용되므로 공식적인 자바스크립트 문법은 아니다.
브라우저는 JSX 문법을 이해하지 못하기 때문에 브라우저에서 실행하기 전에 [[Babel]]을 사용하여 일반 자바스크립트 형태의 코드로 변환된다. 

JSX는 하나의 파일에 자바스크립트와 HTML을 동시에 작성하여 편리하다.

EX)
```
// 실제 작성할 JSX 예시
function App() {
	return (
      <h1>Hello, Daejun!</h1>
    );
}

// 위와 같이 작성하면, 바벨이 다음과 같이 자바스크립트로 해석하여 준다.
function App() {
	return React.createElement("h1", null, "Hello, Daejun!");
}
```

2.JSX 문법


> [!NOTE] > 1. 반드시 부모 요소 하나가 감싸는 형태여야 한다
> 
[[Virtual DOM]] 에서 컴포넌트 변화를 감지할 때 효율적으로 비교할 수 있도록 컴포넌트 내부는 하나의 [[DOM]] 트리 구조로 이루어져야 한다는 규칙이 있기 떄문이다.

EX) 에러 케이스
```
function App(){
return(
	<div>Hello</div>
	<div>Daejun</div>
	)
}
```


> [!NOTE] 2. 자바스크립트 표현식

 JSX 안에서도 자바스크립트 표현식을 사용할 수 있다. 자바스크립트 표현식을 작성하려면 JSX내부에서 코드를 {}로 감싸주면 된다.


> [!NOTE] 3. if문(for문) 대신 삼항 연산자(조건부 연산자) 사용
> > 

 if문과 for문은 JavaScript 표현식이 아니기 때문에 JSX 내부 자바스크립트 현식에는 사용할 수 없다.  
 그렇기 때문에 조건부에 따라 다른 렌더링 시 JSX 주변 코드에서 if문을 사용하거나, {}안에서 삼항연사자를 사용해야 한다.

EX) 방법 1. 외부에서 사용
```
function App() {
let desc = "";
const loginYn = 'Y';
  if(loginYn === 'Y') {
    desc = <div>Daejun 입니다. </div>;
  }else{
    desc = <div>비회원 입니다. </div>;
  }
  return(
    {desc}
  )
}
```

EX) 방법 2. 삼항 연산자 사용
```
function App() {
  const loginYn = 'Y';
  return (
    <>
      <div>
        {loginYn === 'Y' ? (
          <div>Daejun 입니다. </div>
        ):(
          <div>비회원 입니다. </div>
        )}
      </div>
    </>
  );
}
```

EX) 방법 3. 즉시 실행 함수 사용
```
function App(){
  const loginYn = 'Y';
  return (
    <>
      {
        (() => {
          if(loginYn === "Y"){
            return(<div>Daejun 입니다. </div>);
          }else{
            return(<div>비회원 입니다. </div>);
          }
        })()
      }
    </>
  )
}
```


> [!NOTE] 4. [[React DOM]]은 HTML 어트리뷰트 이름 대신 camelCase를 사용한다.
 
 JSX 스타일링 - JSX에서 자바스크립트 문법을 쓰려면 {}를 써야 하기 때문에, 스타일을 적용할 때에도 객체 형태로 넣어 주어야 한다.
 카멜케이스를 작성해야 한다. ex) font-size => fontSize

```
function App() { 
  const style = { 
    backgroundColor: 'green',
    fontSize: '12px' 
  } 
  return ( 
    <div style={style}>Hello, Daejun</div> 
  );
}
```

