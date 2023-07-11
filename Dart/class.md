dart에서 property를 선언할 때는 타입을 사용해서 정의한다.  
```dart  
class Player {  
final String name = 'jisoung';  
final int age = 17;  
void sayName(){  
// class method안에서는 this를 쓰지 않는 것을 권장한다.  
print("Hi my name is $name")  
}  
}  
  
void main(){  
// new를 꼭 붙이지 않아도 된다.  
var player =Player();  
}  
```

dart에서 생성자(constructor) 함수는 클래스 이름과 같아야 한다.  
  
```dart  
class Player {  
// 이럴 때 late를 사용한다.  
late final String name;  
late final int age;  
// 클래스 이름과 같아야한다!  
Player(String name){  
this.name = name;  
}  
}  
  
void main(){  
// Player 클래스의 인스턴스 생성!  
var player = Player("jisoung", 1500);  
```  
  
위의 생성자 함수는 다음과 같이 줄일 수 있다.  
```dart  
// 생략  
Player(this.name, this.age);  
```  
첫 번째 인자는 this.name으로 두 번째 인자는 this.age로 갈 것이다.

클래스가 거대해질 경우 위와 같이 생성자 함수를 만드는 것은 비효율적일 것이다.  
예를 들어보자  
```dart  
class Team {  
// property
final String name;  
int age;  
String description;  

// constructor
Team(this.name, this.age, this.description);  
}  
  
void main(){  
// 헉 너무 많은 인자를 받아야 해서 햇갈린다.  
// 거기다 각 인자의 의미를 알 수가 없다.  
var myTeam = Team("jisoung", 17, "Happy coding is end coding");  
```  
  
이 문제를 해결하려면 너무 간단하다.  
첫 번째는 중괄호({})를 이용하는 것이다.  
  
```dart  
class Team {  
final String name;  
int age;  
String description;  
  // 선택적 파라미터 적용
Team({this.name, this.age, this.description});  
}  
  
void main(){  
// 한 눈에 볼 수 있다.  
var player = Player(  
name: "jisoung",  
age: 17,  
description: "Happy coding is end coding"  
}  
}  
```  
두 번째는 name parameter를 사용하는 것이다.  
```dart  
// 생략  
Player(name:"jisoung", age: 17, description: "Happy coding is end coding");  
```  
하지만 여기에는 큰 문제가 있다.  
변수가 null일 수도 있기 때문에 우리는 이걸 required를 이용하거나 기본 값을 줘서 처리해 줘야한다. 우리는 required를 사용할 것이다.  
  
```dart  
// 생략  
Team({  
required this.name,  
required this.age,  
required this.description,  
});,  
```  
훨씬 좋아졌다.

만약 생성자(constructor) 함수를 여러개 만들고 싶다면 어떨까?  
  
```dart  
// 생략  
Player.createBluePlayer({  
required String name,  
required int age,  
}) : this.age = age,  
	 this.name = name,  
	 this.team = 'blue',  
	 this.xp = 0;  
```  
콜론(:)을 사용하면 특별한 생성자 함수를 만들 수 있다.  
콜론을 넣음으로써 dart에게 여기서 객체를 초기화하라고 명령할 수 있다.  
기존 생성자 코드와 비교해보자  
  
```dart  
// 첫 번째 case  
class Player {  
late final String name;  
Player({  
required this.name  
});  
}  
  
void main(){  
var player = Player(  
name: "jisoung",  
);  
}  
```  
```dart  
// 두 번째 case  
Player({this.name, this.age, this.description});  
```  
```dart  
// 세 번째 case  
class Player {  
final String name;  
Player.createUser({  
required this.name  
}): this.name = name;  
}  
  
void main(){  
var player = Player.createUser(  
name: "jisoung",  
);  
}  
```

예제를 보자  
```dart  
// 생략  
void main(){  
var jisoung = Player(name: "jisoung", age: 17, description: "Happy code is end coding");  
jisoung.name = "nico";  
jisoung = 20;  
jisoung.description = "Best Project is End Project";  
}  
```  
위를 보면 반복되는 부분이 있다. dart에서는 이걸 간단하게 ..으로 해결할 수 있다.  
```dart  
// 생략  
void main(){  
var jisoung = Player(name: "jisoung", age: 17, description: "Happy code is end coding");  
...name = "nico"  
..age = 20  
..description = "Best Project is End Project";  
}  
```  
각 '..'들은 jisoung을 가리킨다. 매우 유용한 operator이다.  
앞에 class가 있다면 그 클래스를 가리킨다.

enum은 우리가 실수하지 않도록 도와주는 타입이다.  
dart에서 enum type을 만드는 법은 다음과 같다  
```dart  
enum Team {  
red,  
blue,  
}  
class Player {  
String name;  
int age;  
Team team;  
  
Player({  
required this.name,  
required this.age,  
required this.team,  
});  
}  
  
void main(){  
var jisoung = Player(name: "jisoung", age: 17, team: Team.red);  
var sushi = jisoung  
..name = "sushi"  
..age = 12  
..team = Team.blue;  
```

추상화 클래스는 다른 클래스들이 직접 구현 해야하는 메소드들을 모아놓은 일종의 `청사진`이라 보면 된다.  
추상 클래스에서는 기능을 구현하지 않는다.  
```dart  
abstract class Human {  
void walk();  
}  
```  
extends를 이용해 상속, 확장을 할 수 있다.  
```dart  
abstract class Human {  
void walk();  
}  
class Player extends Human {  
// 생략  
void walk(){  
print("working!");  
}  
}  
```

상속을 하고 super를 이용해 부모 클래스의 생성자를 호출할 수 있다.  
```dart  
class Human {  
final String name;  
Human(this.name); // 호출 받는다.  
void sayHello(){  
print("Hello! $name");  
}  
}  
  
class Player extends Human {  
Player({  
required this.team,  
required String name  
}) : super(name: name);  
// Human의 생성자 함수를 호출한다.  
}  
```  

==@override==를 이용해 부모 클래스의 객체를 받아올 수 있다.  
```dart  
// 생략  
==@override==  
void sayHello(){  
super.sayHello();  
}
```

## Mixins  
Mixin은 생성자가 없는 클래스를 의미한다.  
Mixin 클래스는 상속을 할 때 extends를 하지 않고 with 를 사용한다.  
Mixin의 핵심은 여러 클래스에 재사용이 가능하다는 점이다.  
```dart  
class Tall {  
final double tall = "190.00"  
}  
  
class Human with Tail {  
// 생략  
print(tall) // "190.00"
}  
```  
extends와 차이점은 extend를 하게 되면 확장한 그 클래스는 부모 클래스가 되지만 with는 부모의 인스턴스 관계가 된다. 단순하게 mixin 내부의 프로퍼티를 갖고 오는 거라고 생각하면 쉽다.