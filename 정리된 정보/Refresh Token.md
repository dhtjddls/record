- 문제 제기 : refresh token에 대한 질문을 꽤나 받았다. 혹시 이후에도 해당 내용에 대해 도움이 필요할지 모를 사람들을 위해 문서로 남겨두려한다.
- ![[Pasted image 20230515193724.png]]


1. Access token
	- refresh 토큰의 탄생 배경은 access token에 있다. 일반적으로 로그인이 성공했을 때 서버는 res의 헤더영역인 cookie에 유저의 간단한 정보가 포함된 암호화된 access token을 발급한다. 그리고 acess token이 존재하는 사용자에 한해서 유저 권한을 인가(유저 권한을 허가)한다.
	- 다만 이러한 토큰일 누군가에게 탈취당했을 때, 서버 측에서 마땅히 할 수 있는 조취가 없기 때문에 기본적으로 짧은 유효기간을 갖는다. 그리고 이러한 짧은 유효기간은 유저들의 불편을 유도할 뿐만 아니라 보안적으로도 미봉책이다.
2. refresh token
	- 그래서 등장한 것이 refresh token이다. refresh token은 access token과 다르게 긴 유효기간을 가지며, refresh token이 있다면, access token이 만료되었더라도 새로운 acess token으로 교체하여 발급 가능하다. aceess token의 한 한달짜리 인증서와 비슷하다. 
	- 때문에 acess token보다 더 높은 수준의 보안을 필요로 하기 때문에 refresh token은 안전한 저장소에 저장되며 보안 사항이 발생했을 때 바로 삭제하여 대처가 가능하다.
3. refresh token이 적용된 로그인과 인증흐름
	1. 로그인을 하면, 유효기간이 짧은 access token과 긴 refresh token을 모두 발급한다.
	2. 이 후 인증 정보를 체크할 때는 먼저 refresh token을 확인한다. 
		   refresh token이 만약 있다면 -> acess token만 재발급
		   없다면 -> refresh token이 없기 때문에 다시 로그인
	3. 로그아웃 시 혹은, refresh token의 유효기간이 만료 되었을 때는 db에 저장된 refresh token에 대한 정보를 삭제해준다.