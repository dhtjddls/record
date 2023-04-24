morgan이란?
morgan은 nodeJS 에서 사용되는 로그 관리를 위한 미들웨어 입니다. 
매번 return status().json({message})에서 벗어나 깔끔하고 편리한 로깅을 할용해 봅시다!

### 기본적인 사용법
- 기본적인 사용법은 매우 간단합니다
	1. npm i morgan
	2. app.js 혹은 엔드포인트 파일에 require 해준 후, 미들웨어 사용을 위해 app.use(morgan('옵션 명')) 을 입력하면 끝! 
	3. 옵션명에는 기본적으로 dev(개발 전용 로그), combined(긴 로그), common(보통), short(짧은 로그), tiny(최소한의 로그) 등이 있습니다. 개발을 할 때는 주로 dev를 사용합니다!

```
var express = require('express')

var morgan = require('morgan')

var app = express()

app.use(morgan('combined'))

app.get('/', function (req, res) {

  res.send('hello, world!')

})
```

추가적인 사용법
- 기본적으로 morgan 함수는 morgan(format, options) 라는 두 매개변수를 가집니다.
- format에는 앞서 우리가 이야기한 기본적은 옵션명들이 들어갑니다. 

- **combined**
-   배포환경에서 사용
-   불특정 다수가 접속하기 때문에 IP를 로그에 남겨줌

```
:remote-addr - :remote-user [:date[clf]] ":method :url HTTP/:http-version" :status :res[content-length] ":referrer" ":user-agent"
```

**common**

```
:remote-addr - :remote-user [:date[clf]] ":method :url HTTP/:http-version" :status :res[content-length]
```

**dev**

-   개발용을 위해 response에 따라 색상이 입혀진 축약된 로그를 출력.
-   :status값이 빨간색이면 서버 에러코드, 노란색이면 클라이언트 에러 코드, 청록색은 리다이렉션 코드, 그외 코드는 컬러가 없다.

```
:method :url :status :response-time ms - :res[content-length]
```

**short**

-   기본 설정보다 짧은 로그를 출력하고, 응답 시간을 포함.

```
:remote-addr :remote-user :method :url HTTP/:http-version :status :res[content-length] - :response-time ms
```

**tiny**

-   최소화된 로그를 출력

```
:method :url :status :res[content-length] - :response-time ms
```


- options에는 immediate 과 skip이 있습니다.
	- immediate
	- 응답 대신 요청 시 로그 라인을 작성합니다. 즉, 서버가 다운되더라도 요청은 기록되지만 _응답의 데이터(예: 응답 코드, 콘텐츠 길이 등)는 기록될 수 없습니다_ .
	- skip
	- 로깅의 스킵여부를 결정하기 위한 함수입니다.
	- 기본값은 false. 이 함수는 "skip(req, res)" 형식으로 호출됩니다.
```
morgan('combined', {
  skip: function (req, res) { return res.statusCode < 400 }
})
```

기록된 로그들을 파일로 저장해두고 싶다면?

한개의 파일에 저장하기
```
// create a write stream (in append mode)

var accessLogStream = fs.createWriteStream(path.join(__dirname, 'access.log'), { flags: 'a' })

// setup the logger

app.use(morgan('combined', { stream: accessLogStream }))
```

날자 별로 저장하기
```
var accessLogStream = rfs.createStream('access.log', {

  interval: '1d', // rotate daily

  path: path.join(__dirname, 'log')

})

// setup the logger

app.use(morgan('combined', { stream: accessLogStream }))

```

참고:  https://www.npmjs.com/package/morgan, https://inpa.tistory.com/entry/EXPRESS-%F0%9F%93%9A-morgan-%EB%AF%B8%EB%93%A4%EC%9B%A8%EC%96%B4

