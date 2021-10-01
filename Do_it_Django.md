# DO IT Django

### **부트스트랩**

 mb-2 : 공백주는 법

* m : margin / p : padding
* t : top / b : bottom / l : left / r : right / x : (x축) l , r / y : (y축) t , b
* 숫자 : 공백크기





 btn-sm : 버튼 크기

* lg / sm / xs / default





### **messages 모듈 (views.py)**

1회성 메시지 생성 : 1회 노출되고 사라짐



### **render**

render( request, template_name, context = None, content_type=None, status = None, using = None)

* request, template_name은 필수 인자
* redirect와 비교 : render는 템플릿을 불러오고, redirect는 URL로 이동함



### **path**

path( route, view, kwargs, name)

* route : URL 패턴 문자열
* view : 패턴을 찾으면 호출할 view함수
* name : URL에 이름을 지어주면 Django에서 명확하게 참조할 수 있음



### **새 기능 추가 패턴**

1. 템플릿에 추가 기능을 위한 링크나 버튼 추가
2. urls.py에 링크에 해당되는 URL 매핑을 작성
3. forms.py에 폼 작성(폼이 필요없으면 생략 가능)
4. views.py 에 URL 매핑에 추가한 함수 작성
5. 함수에 템플릿 작성

