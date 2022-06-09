# about_nest
nestjs에 대해서 알게 된 정보를 기록하는 저장소입니다.



# 3강
## nest.js vs express
- nest는 express를 사용하고 있음.  

### 라우터 문제
- 3강 10:20 에서 
``` javascript
app.use("/api", apiRouter); // /api로 시작하지 않으면 index.html로 넘기는 코드인듯
app.get("*",(req,res,next)=>{
	res.sendFile(path.join(__dirname, "public", "index.html"));
});
```

# 6강 - 컨트롤러 기본
### 모듈
- 메인에서 처음으로 가는 곳이 모듈. 
- express는 app.js에서 라우터를 많이 붙였는데, 네스트는 모듈 위주의 설계.
- @Get() // @Post를 통해서 IoC
- 모듈을 직접 구성해야한다는 점에서 스프링보다 IoC가 약함. 

### 서비스
- 비즈니스 로직
- 서비스는 요청과 응답에 대해서는 모른다. (req,res)가 없어야함 !
- -> req, res 없으면 좋으점 모킹(req,res) 필요 없는 디버깅 가능.
``` javscript
{code: SUCCESS, data: data} //의 모양으로 알아서 데이터 return
```
- return res.json(data);하지 않고 return data; 해도 알아서 역직렬화 해줌

# 7강 ConfigModule 사용하기(dotenv 진화판)
- express의 미들웨어 vs nest
- nest는 모듈 시스템이라 .env 등을 갖다 쓰려고 해도 모듈로 만들어서 다시 연결하는 작업을 해야함. -> 기존 라이브러리 미리 모듈로 감싸놓은 패키지를 사용하는게 편함. 
```javascript
@Module({
  imports: [ConfigModule], //설정 없는 경우 모듈만  
  imports: [ConfigModule.forRoot()], //설정 있는 경우 모듈뒤에 함수가 붙음 
```
- (.env)ConfigService를 사용하여 -> Service클래스에서 주입을 해주어 사용하는 것이 좋다. 
```javascript
@Module({
  imports: [ConfigModule.forRoot({isGlobal:true, load:[getEnv]})], 
  // const getEnv = async ()=>{} //비동기함수로 사용 가능해짐
```

# 8강 loggerMiddleware로 morgan처럼 로깅하기
- 요청이 들어왔을때 콘솔 출력 해쥼
- cf)  next(); // 미들웨어 쓸 떄 항상 next()를 써야 다음으로 넘어감
