useEffect(()=> {
	console.log('[[렌더링]] 될 때 마다 실행.');
})

useEffect(()=> {
	console.log('[[마운트]] 될 때만 실행.');
}, []);

useEffect(() => {
	console.log('value값이 업데이트 될 때마다 실행');
}, [value])


useEffect이 배열이고 배열에 원소를 추가하고 싶을 때는 로직에서 새로운 배열을 생성하고 생성된 배열에 값을 추가한 다음, 생성된 배열을 set해주는 방식으로 사용해야 한다.