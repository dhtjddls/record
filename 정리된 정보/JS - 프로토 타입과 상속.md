
문제제기: JS 객체에 대하여 공부하던 중, Pass-by-reference 참조에 의한 전달에 대하여 알게 되었고, 
그 예시로 
해당 값들을 해당 객체 내에서 직접 설정하지 않다 다른 객체에서 참조하여 지정할 시,
값을 복사하여 해당 객체의 고유 값으로 저장하는 것이 아니라 메모리에 저장되어 있는 그 값을 동시에 참조하고 있기 때문에 
둘 중 한 곳에서 해당 값을 변경하면 둘 모두에서 변경되는 이러한 경우를 알게 되었다.

```
var a = {}, b = {}, c = {}; // a, b, c는 각각 다른 빈 객체를 참조 
console.log(a === b, a === c, b === c); // false false false 
a = b = c = {}; // a, b, c는 모두 같은 빈 객체를 참조 
console.log(a === b, a === c, b === c); // true true true
// a를 바꾸면 b, c 모두 바뀜
```

하지만 여기서 의문점이 생기는데, 그렇다면 객체간의 상속을 통해 구현 할 때에, 하위 객체에서의 변경사항이 상위객체에게도 영향을 미치게 되는 큰 문제가 발생하지 않을까? 라는 의문점이 생겨서 JS의 프로토 타입과 상속에 대해 알아보게 되었다. 

알아본 결과, 모든 객체는 생성시 프로토타입이라는 자신의 부모 객체 부터 원형 객체 까지 연결되어 있는 유전자와 같은 객체와 함께 생성됩니다. 이 프로토 타입 객체는 유전자처럼 상위의 프로토 타입 객체들과 연결(체이닝) 되어 있는데 이것을 프로토타입 체이닝이라고 합니다. 
의문점의 결론은 일단 프로토 타입과는 큰 관련은 없었던 것으로 보인다. 객체 참조로 인한 다른 객체에서의 변경 문제는 객체의 assign 함수로 객체의 내부 내용들을 복사하여 새로운 객체를 생성해 참조를 피하거나, freeze 함수를 통해불변 객체로 만들거나, immutable 패키지를 사용한다면 방지 가능하다.

글로만 설명이 어려우시다면 
https://www.youtube.com/watch?v=wUgmzvExL_E
해당 동영상을 추천드립니다!