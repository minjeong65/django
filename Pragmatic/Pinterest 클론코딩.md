# Pinterest 클론코딩

### --- MVT ---

**Model**

* django와 데이터데이스 간 통신을 하게 함

* 생성되는 객체를 데이터베이스에 등록해야하는데 쿼리문을 사용하지 않고 편리하게 등록할 수 있게 해줌

**View**

* 계산 부분

* user의 요청에 응답하기 위해 server가 하는 작업

**Template**

* 웹 사이트 외부 구현(User Interface)
* User의 요청에 서버가 응답하는 과정에서 요청값을 받아 화면에 보여줌
* 정적 언어인 html에 동적인 부분을 생성하게 해주는 작업

</br>

### --- Git ---

**.gitignore**

git으로 추적하지 않을 파일들을 정의한 파일

* db.sqlite3, .env 등

</br>

**commit**

< git bash >

> cd c/my/pragmatic 

파일이 있는 디렉토리로 이동

> git status

아직 추적되지 않은 파일을 보여줌

> git add .

추적되지 않은 모든 파일을 add함(커밋할 준비)

> git commit -m "메시지"

메시지에 부가 설명을 작성하여 커밋

</br>

### --- SECRET KEY ---

**SECRET KEY**

* SECRET_KEY는 주로 쿠키데이터 해시, 암호화 등 임시적인 일에 사용되고, 변경 시 로그인 세션 등의 데이터가 사라질 수 있음

* django의 보안과 관련된 것이므로 외부로 노출되면 안됨
*  50자의 랜덤 문자로 구성

**SECRET KEY 분리**

* 환경변수패턴 : SECRET_KEY의 값을 환경변수에 저장하여 참고
* **비밀파일패턴** : SECRET_KEY의 값을 별도 파일에 저장하여 참고
  * .env 파일을 생성하여 참고하도록 하고 해당 파일은 .gitignore에 추가함

</br>

### ---  ---
