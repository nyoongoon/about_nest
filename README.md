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

