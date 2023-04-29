1. 제너레이터란?
	1.  제너레이터(Generator) 함수는 이터러블을 생성하는 함수
2. 생김새
	1.  function* 키워드로 선언한다. 그리고 하나 이상의 yield 문을 포함한다.
	2. function* counter() { console.log('Point 1'); yield 1; // 첫번째 next 메소드 호출 시 여기까지 실행된다. console.log('Point 2'); yield 2; // 두번째 next 메소드 호출 시 여기까지 실행된다. console.log('Point 3'); yield 3; // 세번째 next 메소드 호출 시 여기까지 실행된다. console.log('Point 4'); // 네번째 next 메소드 호출 시 여기까지 실행된다. }
3. 그래서 어디에 써요?
	1. 함수 내부에서 바로 비동기 처리를 동기 처리 처럼 구현할 수 있다.
	2. const g = (function* () { 
	3. let user;
	4. //  비동기 처리 함수가 결과를 반환한다.
	5. // 비동기 처리의 순서가 보장된다. 
	6. user = yield getUser(g, 'jeresig'); 
	7. console.log(user); // John Resig 
	8. user = yield getUser(g, 'ahejlsberg'); console.log(user); // Anders Hejlsberg 
	9. user = yield getUser(g, 'ungmo2'); 
	10. console.log(user); 
	11. // Ungmo Lee 
	12. }());
