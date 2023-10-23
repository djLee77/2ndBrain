React Hooks는 React 16.8버전에 추가된 공식 **라이브러리**입니다.

[[Class Component(클래스형 컴포넌트)]]의 단점은 상태에 따라 그 결과 값이 의도치 않게 변한다는 것. 즉 예상치 못한 side effect가 발생할 수 있다는 것이다.

[[Function Component(함수형 컴포넌트)]]는 불변성을 갖고있지만, 클래스형 컴포넌트가 제공하는 state와 setState를 이용해 상태와 생명주기를 관리하는 강력한 기능들을 대체할 수 없었다.

이를 위해 함수형 컴포넌트에서도 클래스형 컴포넌트처럼 [[리렌더링]]하고 생명주기를 관리할 수 있도록 해주는 **React Hooks**가 나온 것이다.

* [[useEffect]]
* [[useState]]
* [[useRef]]
* 