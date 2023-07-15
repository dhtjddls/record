Git 이란?
- 분산 버전 관리 시스템으로, 파일의 변경 사항을 추적하고 여러 사용자들 간의 파일에 대한 작업을 조율하는데 사용된다.
간단한 Git 명령어
- git init : git 생성하기
- git clone git_path : 코드가져오기
- git checkout branch_name : 브랜치 선택하기
- git checkout -t remote_path/branch_name : 원격 브랜치 선택하기
- git branch branch_name : 브랜치 생성하기
- git branch -r : 원격 브랜치 목록보기
- git branch -a : 로컬 브랜치 목록보기
- git branch -m branch_name change_branch_name : 브랜치 이름 바꾸기
- git branch -d branch_name : 브랜치 삭제하기
- git push remote_name — delete branch_name : 원격 브랜치 삭제하기 
  ( git push origin — delete gh-pages )
- git add file_path : 수정한 코드 선택하기 ( git add * )
- git commit -m “commit_description” : 선택한 코드 설명 적기 ( git commit -m “내용”)
- git push romote_name branch_name : add하고 commit한 코드 git server에 보내기 (git push origin master)
- git pull : git서버에서 최신 코드 받아와 merge 하기
- git fetch : git서버에서 최신 코드 받아오기
- git reset — hard HEAD^ : commit한 이전 코드 취소하기
- git reset — soft HEAD^ : 코드는 살리고 commit만 취소하기
- git reset — merge : merge 취소하기
- git reset — hard HEAD && git pull : git 코드 강제로 모두 받아오기
- git config — global user.name “user_name ” : git 계정Name 변경하기
- git config — global user.email “user_email” : git 계정Mail변경하기
- git stash / git stash save “description” : 작업코드 임시저장하고 브랜치 바꾸기
- git stash pop : 마지막으로 임시저장한 작업코드 가져오기

Git branch 전략
- Git Flow
	- gitflow에는 5가지 브랜치가 존재
	- **master** : 기준이 되는 브랜치로 제품을 배포하는 브랜치
	- **develop** : 개발 브랜치로 개발자들이 이 브랜치를 기준으로 각자 작업한 기능들을 Merge
	- **feature** : 단위 기능을 개발하는 브랜치로 기능 개발이 완료되면 develop 브랜치에 Merge
	- **release** : 배포를 위해 master 브랜치로 보내기 전에 먼저 QA(품질검사)를 하기위한 브랜치
	- **hotfix** : master 브랜치로 배포를 했는데 버그가 생겼을 떄 긴급 수정하는 브랜치
![[Pasted image 20230712172354.png]]

- **gitflow 과정**  (참고: [우아한형제들 기술블로그 (우린 Git-flow를 사용하고 있어요)](https://techblog.woowahan.com/2553/))
1. master 브랜치에서 develop 브랜치를 분기합니다.
2. 개발자들은 develop 브랜치에 자유롭게 커밋을 합니다.
3. 기능 구현이 있는 경우 develop 브랜치에서 feature-* 브랜치를 분기합니다.
4. 배포를 준비하기 위해 develop 브랜치에서 release-* 브랜치를 분기합니다.
5. 테스트를 진행하면서 발생하는 버그 수정은 release-* 브랜치에 직접 반영합니다.
6. 테스트가 완료되면 release 브랜치를 master와 develop에 merge합니다.

- Github Flow
	- Git-flow가 Github에서 사용하기에는 복잡하다고 나온 브랜치 전략이다.
	- hotfix 브랜치나 feature 브랜치를 구분하지 않는다. 다만 우선순위가 다를 뿐
	- 수시로 배포가 일어나며, CI와 배포가 자동화되어있는 프로젝트에 유용
	![[Pasted image 20230712172020.png]]

- gitlab flow
	- 복잡한 Gitflow와 너무 간단한 Github의 절충안
	- master 브랜치는 production 브랜치
	- production브랜치는 master 이상 권한만 push 가능
	- developer 권한 사용자는 master 브랜치에서 신규 브랜치를 추가
	- 신규 브랜치에서 소스를 commit 하고 push
	- merge request를 생성하여 master 브랜치로 merge 요청
	- master 권한 사용자는 developer 사용자와 함께 리뷰 진행 후 master 브랜치로 merge
	- 테스트가 필요하다면 master에서 procution 브랜치로 merge하기 전에 pre-production 브랜치에서 테스트
	![[Pasted image 20230712172205.png]]

참고자료: https://velog.io/@kw2577/Git-branch-%EC%A0%84%EB%9E%B5