Functions  
  
Dart는 진정한 객체 지향 언어이므로 함수도 객체이며 타입이 Function입니다. 이는 함수를 변수에 할당하거나 다른 함수에 인수로 전달할 수 있음을 의미합니다.  
```  
// 하나의 표현식만 포함하는 함수의 경우 아래와 같이 단축 구문을 사용할 수 있습니다.  
String sayHello(String name) => "Hello ${name} nice to meet you.";  
  
num plus(num a, num b) => a + b;  
  
void main() {  
print(sayHello("sugar"));  
}  
```  
https://dart.dev/guides/language/language-tour#functions

Named parameters  
  
Named parameters는 명시적으로 required로 표시되지 않는 한 선택 사항입니다. 기본값을 제공하지 않거나 Named parameters를 필수로 표시하지 않으면 해당 유형은 기본값이 null이 되므로 null을 허용해야 합니다.  
```  
String sayHello(  
{required String name, required int age, required String country}) {  
return "${name} / ${age} / ${country}";  
}  
  
void main() {  
print(sayHello(name: "sugar", age: 10, country: "Korea"));  
}  
```  
https://dart.dev/guides/language/language-tour#parameters

Dart에서 [] 은 optional, positional parameter를 명시할 때 사용된다.  
name, age는 필수값이고 []를 통해 country를 optional값으로 지정해줄 수 있다.  
  
```  
String sayHello(String name, int age, [String? country = ""]) {  
return 'Hello ${name}, You are ${age} from the ${country}';  
}  
  
void main() {  
var result = sayHello("sugar", 10);  
print(result);  
}  
```

?? 연산자를 이용하면 왼쪽 값이 null인지 체크해서 null이 아니면 왼쪽 값을 리턴하고 null이면 오른쪽 값을 리턴한다.  
```  
String capitalizeName(String? name) {  
return name?.toUpperCase() ?? "";  
}  
```  
  
??= 연산자를 이용하면 변수 안에 값이 null일 때를 체크해서 값을 할당해줄 수 있다.  
```  
void main() {  
String? name;  
name ??= "sugar";  
name = null;  
name ??= "js";  
print(name); // js  
}  
```