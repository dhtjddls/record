
1. Java에서 this는 인스턴스 자신을 가리키는 참조 변수지만 JS에서는 함수 호출 방식에 따라서 this가 가르키는 대상이 달라진다(왜..왜!!!)
2. 기본적인 함수 호출시 무조건 전역 객체에 바인딩 된다 this -> window or global
   객체 바로 아래에 있는 메서드 빼고 나머지 내부 함수들은 다 전역에 바인딩 된다. 콜백도 
   (예외는 없다 ㄱ-)
3. 메서드로 호출되는 건 해당 생성 객체에 바인딩된다.
4. new를 붙인 생성자 함수 호출시 해당 함수의 생성 객체에 바인딩 된다 (이래야지..원래는..ㅠ)
5. 해서 new가 없으면 전역에 바인딩되는 위험성을 회피하기 위해서 함수 내부에 if(!(this instanceof arguments.callee)) -> 요런 if문을 넣어서 처리해 준다. (-> 없으면 new로 해서 만들어줘!)
6. 이런 전역에 바인딩 되버리는 애들을 명시적으로 상위 객체로 바인딩하는 방법도 있다. ->
   apply, call, bind
	 - apply(바인딩할것, [바인딩 될것]) 2번째 인자 array
	 - call(바인딩할것, 바인딩될것) 2번째 인자 not array
	 - bint(this) 는 this가 바인딩 된 새로운 함수를 반환한다. ->해서 새로 실행시켜줘야함.