
bcrypt라는 암호화 해쉬 모듈과 bcryptjs라는 해쉬 모듈은 거의 같지만 
https://lahuman.github.io/bcrypt_bcryptjs/
해당 링크의 글을 통해 알게 된 점은 bcrpyt사용을 위해서는 os에 c++과 python 등이 설치되어야 한다. 물론 성능은 더 좋지만 js만 사용하는 우리 프로젝트에 bcryptjs가 더 적합하다고 생각했다.

1. 그래서 bcrypt가 뭔데?
	- bcrypt는 암호를 해시하는데 도움을 주는 라이브러리로 유저들의 비밀번호를 그대로 저장하는 것이 아니라 hash를 통해 암호화하여 보관할 수 있도록 도와준다.
2. 어떻게 쓰는데?
	1. npm i bcryptjs로 설치 require로 불러옵니다.
	- `npm install bcryptjs`
	  const  bcrypt  = require( ' bcryptjs ' ) ;
	2. hash로 변환해서 db에 저장해 줍니다.
	- var salt = bcrypt.genSaltSync(10);
	var hash = bcrypt.hashSync("password", salt);
	3. 변환한 pw를 입력값과 비교합니다.
	- bcrypt.compareSync("password", 'inputPassword');

3. 암호화는 뭐고 해시는 뭐야?
	- 암호화는 말 그대로 사람들이 바로 알아볼 수 없게 암호처럼 만들어 놓는 것을 말합니다.
	- 암호화에서 말하는 해시는 쉽게 말하면 정해진 길이의 랜덤한 값을 생성하는 것을 말한다. 이런 기법을 사용하여 암호화를 수행한다.
	- 그 중 bcrypt는 추가적으로 원래 데이터에 추가적으로 랜덤한 데이터를 더하여 암호화를 진행하여 더 강력한 암화를 제공하는데, 이 추가적인 램덤 데이터를 우리가 위에서 정의한 Salt라고 생각하면 된다.