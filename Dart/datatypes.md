dark에는 대표적으로 다음과 같은 타입이 있다.  
void main() {  
String name = "tom";  
bool isPlay = true;  
int age = 10;  
double money = 52.55;  
num x = 12;  
num y = 1.2;  
}
`중요한 점은 이 모든게 object라는 것이다.`  
만약 IDE를 사용하고 있다면 컨트롤 + 클릭(mac인 경우 cmd + 클릭)을 통해 그 자료형에 들어가보면 class인 것을 확인할 수 있다.
int, double => num을 상속받았다!


List를 사용하는 2가지 방법  
```  
void main() {  
List numbers = [1, 2, 3];  
var number2 = [4, 5, 6];  
}  
```  
  
List는 collection if와 collection for를 지원한다.  
collection if는 List를 만들 때, if를 통해 존재할 수도 안 할 수도 있는 요소를 가지고 만들 수 있다.  
```  
void main() {  
var giveMeFive = true;  
var item = [  
1,  
2,  
3,  
if (giveMeFive) 10, // giveMeFive가 true이면 10을 넣음  
];  
print(item);  
}  
```  
https://dart.dev/guides/language/language-tour#collection-operators


Collection For  
  
Dart는 조건문(if) 및 반복(for)을 사용하여 컬렉션을 구축하는 데 사용할 수 있는 컬렉션 if 및 컬렉션 for도 제공합니다.  
```  
void main() {  
var oldFriends = ["nico", "lynn"];  
var newFriends = [  
"tom",  
"jon",  
for (var friend in oldFriends) "❤️ $friend"  
];  
  
print(newFriends); // [tom, jon, ❤️ nico, ❤️ lynn]  
}  
```  
https://dart.dev/guides/language/language-tour#collection-operators

Maps  
  
일반적으로 맵은 key와 value를 연결하는 객체입니다. 키와 값 모두 모든 유형의 객체가 될 수 있습니다. 각 키는 한 번만 발생하지만 동일한 값을 여러 번 사용할 수 있습니다.  
```  
var gifts = {  
// Key: Value  
'first': 'partridge',  
'second': 'turtledoves',  
'fifth': 'golden rings'  
};  
  
// Map 생성자를 사용하여 동일한 객체를 만들 수 있습니다.  
var gifts2 = Map();  
gifts2['first'] = 'partridge';  
gifts2['second'] = 'turtledoves';  
gifts2['fifth'] = 'golden rings';  
```  
https://dart.dev/guides/language/language-tour#maps

Sets  
  
Set에 속한 모든 아이템들이 유니크해야될 때 사용한다.  
유니크할 필요가 없다면 List를 사용하면 된다.  
```  
var halogens = {'fluorine', 'chlorine', 'bromine', 'iodine', 'astatine'};  
```  
https://dart.dev/guides/language/language-tour#sets

