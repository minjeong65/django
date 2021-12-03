# MVT

### MVT 

* 장고의 기본 디자인 패턴
* model(데이터베이스) / view(로직) / template(출력화면)

* 처리과정
  1. 클라이언트로부터 요청을 받으면 URLconf(URL - 뷰 매핑)를 이용하여 URL을 분석한다.
  2. URL 분석 결과를 통해 해당 URL에 대한 처리를 담당할 뷰를 결정한다.
  3. 뷰는 자신의 로직을 실행하면서 만일 데이터 베이스 처리가 필요하면 모델을 통해 처리하고 그 결과를 반환받는다.
  4. 뷰는 자신의 로직 처리가 끝나면 템플릿을 사용하여 클라이언트에 전송할 HTML 파일을 생성한다.
  5. 뷰는 최종 결과로 HTML 파일을 클라이언트에게 보내 응답한다.



![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpdQ3m%2FbtqwhTpC3gU%2FvXB2IGfXViX7cGFQgXjlR1%2Fimg.png)

참고 : https://butter-shower.tistory.com/49

</br>

### Model

사용할 데이터에 대한 정의를 담고있는 클래스

</br>

### View

웹 요청을 받아서 데이터 베이스 접속 등 해당 어플리케이션의 로직에 맞는 처리를 하고, 그 결과 데이터를 HTML로 변환하기 위하여 템플릿 처리를 한 후에 최종 HTML로 된 응답 데이터를 웹 클라이언트로 반환하는 역할

* 함수 또는 클래스의 메소드로 작성
* 첫번째 인자로 HttpRequest 객체를 받고 필요한 처리를 한 후에 최종적으로 HttpResponse 객체를 반환함

</br>

### Template

최종 응답에 사용할 *.html 파일을 작성하면, 장고는 이를 해석해서 최종 HTML 텍스트 응답을 생성하고, 이를 클라이언트에게 보냄

* 템플릿 파일을 찾을 때는 TEMPLATE_DIRS 및 INSTALLED_APPS에서 지정된 앱의 디렉토리를 검색
  * settings.py에 정의

