요번에 경험한 node환경에서 multer와 aws s3를 활용한 멀티미디어 파일 업로드에 관한 내용을 기록하려고 합니다.

기본적인 순서
1. aws에서 s3라는 멀티미디어 파일 저장용 bucket, 바구니를 만들어 줍니다. (s3에 등록 시 url로 접근 가능! 매우 유용!)
2. clinet - server 간에 multer를 통해 폼데이터를 주고 받을 때, 클라이언트에서 보낸 파일을 s3에 등록한 후, 접근 가능한 url만 서버에 보내주어 관리하기!
![[node-s3-multer.png]]


각각의 과정은 게시글을 참고하세요!
1. aws s3 생성
   https://bamdule.tistory.com/177
2. multer, multer-s3, aws-sdk를 통한 미들웨어 생성
   https://jane-aeiou.tistory.com/85,
   https://github.com/junkyo974/hanghae_toyproject/blob/main/modules/s3.js
   해당 글들을 참고하여 middleware 작성