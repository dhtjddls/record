
swagger와 swagger-autogen

1. swagger 란? 
	- 우리가 만든 restful api들의 명세를 도와주는 도구입니다.
	- 내가 만든 api들을 서로 공유하고, 확인할 수 있기 때문에 협업시 생산성 증가에 도움을 줄 수 있습니다.
2. swagger-autogen
	- swagger가 api 명세를 도와주지만, 명세를 직접해야 함은 변하지 않습니다. 그러나 
	  swagger-autogen은 내 프로젝트 파일의 내용을 읽어 기본적인 뼈대를 자동생성해주는 편리한 도구입니다. 

사용법
1. 필요한 패키지 다운받기
   ```
   npm i swagger-ui-express swagger-autogen
``
2. app.js에 해당 모듈을 선언해주고, 사용하겠다고 적어줍시다.
```
// 1번째 파라미터 url은 우리가 만든 api 명세를 확인하는 페이지의 url입니다. 마음대로 정의하셔도 됩니다!

app.use("/swagger", swaggerUi.serve, swaggerUi.setup(swaggerFile));
```

3. 원하는 위치에 swagger.js 파일을 하나 만들어 주시고 아래 코드를 작성해 주세요.
 ```
// autogen 패키지 불러오기 및 실행
const swaggerAutogen = require("swagger-autogen")();
// 기본 설명 설정 알맞게 채워주세요
const doc = {
  info: {
    title: "My API",
    description: "Description",
  },
  host: "localhost:3000",
  schemes: ["http"],
};

const outputFile = "./swagger-output.json";
const endpointsFiles = [
  "./app.js" //저희 최종 실행 파일인 app.js
];

swaggerAutogen(outputFile, endpointsFiles, doc);

```

4. 이렇게 작성이 완료되었다면, 해당 파일을 node 명령어로 실행해주세요
```
node ./swagger.js // swagger.js가 있는 파일 경로를 지정해줘야 겠죠? 요기선 프로젝트파일 최상단에 위치해있어서 ./swagger.js입니다.
```

5. 서버를 실행해주고 2번에서 지정해준 url로 접속해서 확인하실 수 있습니다. (ex localhost:3000/swagger)
6. 자동생성된 api 명세의 다른 설명들을 추가하기 위해서는 실행시 새로 생성된 swagger-output.json에서 직접 변경해주시면 됩니다! 