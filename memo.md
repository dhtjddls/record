- AIP -> API Imporvement Proposals
- -> API 디자인 Best 예시 문서 google aip

원하는 기능 추가

  github 컨벤션
	develop 컨벤션
	대용량 데이터
  2일 정도 -> Nest 공부 
  - 1차 스코프
  - 조회랑 검색 
  1. CI/CD 
     -> 1. 테스트 -> 빌드 -> 배포
     -> event(push, pr, merge) -> 준비 해놓은 스크립트(파이프 라인)를 실행한다.
  2. Nest.js, TS
  3. Test Code

  - 2차 스코프 
1. 검색 -> like %wantFind% -> 성능 저하가 나온다.
2. 검색에 한해서 검색엔진을 따로 쓴다 -> elasticsearch, 그 검색을 로깅하고 실시간 모니터링할거다-> ELK
3. 싱글 스레드니까, 손이 부족하니까 손을 늘리면 -> 속도가 빨라질거다.
4. http/1.1 보다 http/2 적용시 속도가 더 빠를 것이다.
5. Test를 포함한 검증 절차를 가진 CI/CD는 코드 리팩토링 및 코드 변경에 긍정적인 영향을 미친다고 하던데 진짠가?