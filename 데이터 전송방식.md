# 데이터 전송방식

### * GET : URL 을 통해서 데이터 전달 

  >   ?  :  데이터 전송부분 시작점
  >   & :  데이터들을 연결
  >   민감한 데이터 전송(보안취약), 많은 양의 데이터 전송(URL 길이 제한) 에 부적절

### * POST : HTTP 패킷에 숨겨서 전달

  > method : 어떤 방식으로 전달할 것이냐
  > action : 어디에 전달할 것이냐

**form 태그**

1. form 태그 안에 있는 정보만 전달

> <form> 여기 안에만 전달 </form>

2. name 속성을 갖지 않는 정보는 전달하지 않음

3. method는 form 태그의 default 값

> method  :  GET
> action  :  현재
