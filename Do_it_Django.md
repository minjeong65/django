# DO IT Django

### **부트스트랩**

 mb-2 : 공백주는 법

* m : margin / p : padding
* t : top / b : bottom / l : left / r : right / x : (x축) l , r / y : (y축) t , b
* 숫자 : 공백크기



 btn-sm : 버튼 크기

* lg / sm / xs / default

### URL과 뷰

* 장고의 기본적인 흐름 : 브라우저에 로컬 서버로 페이지를 요청하면 urls.py에서 URL 매핑을 통해 views.py의 함수를 호출하고, 호출된 결과를 브라우저에 전달



### 모델

* 장고는 기본적으로 SQLite를 사용

  * SQLite는 주로 소규모 프로젝트에서 사용

* 모델을 이용하여 SQL 쿼리문 없이 데이터를 처리할 수 있음 => ORM 사용

  * ORM (Object Relational Mapping) : 데이터베이스 테이블을 모델화하여 사용

* migrate : 각 앱들이 사용하는 데이터 테이블을 생성하는 과정

  * makemigrations : migrate를 하기 전에 데이터를 올리는 과정

  

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



### **Paginator**

from django.core.paginator

페이지 당 몇 개의 글을 보여줄지 지정



### get_object_or_404

get_object_or_404(모델명, pk)

* 예외처리 구문

* pk : primary key(객체 구분자)
* 모델에서 객체를 불러올 때 pk에 해당하는 객체가 있으면 불러오고 없으면 에러 페이지를 호출



### from .. import *

* views.py 파일 분리 과정
* ' . ' 현재 디렉토리의 것을 import하는 것,  '..'는 현재보다 하위 디렉토리의 것을 import 하는 것



### GET/ POST

HTTP 프로토콜의 데이터 전송 메서드

GET 특징:

* URL 뒤에 파라미터를 붙여서 데이터 전송
* URL 길이 제한이 있어 데이터 전송양이 제한되어 있음
* 사용자에게 URL이 노출되므로 보안적으로 안전하지 않음

POST 특징:

* BODY영역에 데이터를 숨겨서 보내므로 GET방식 보다 안전함
* 길이 제한이 없어 대용량 데이터 전송도 가능



### 에러

[makemigrations]

You are trying to change the nullable field 'author' on answer to non-nullable without a default; we can't do that (the database needs something to populate existing rows).

* 모델에 필드를 추가/수정했을 때 발생

* 필드를 추가했을 경우 원래 저장되어있던 객체들의 새로운 필드에는 어떤 조치를 취해야 하는지 물어보는 메세지

* 필드의 속성에 null=True 를 추가해주거나 필드의 default 값을 설정해주면 됨



### 앵커(anchor) 태그

현재 웹페이지에서 다른 웹페이지로 이동하거나 현재 페이지에서 특정 부분으로 스크롤 이동할 때 사용



### 마크다운

* 설치 : pip install markdown

* 필터 등록 : pybo_filter.py

  * ```python
    import markdown  
    django.utils.safestring import mark_safe
    
    @register.filter()
    def mark(value):
        extensions = ["nl2br", "fenced_code"]
        return mark_safe(markdown.markdown(value, extensions=extensions))
    ```

* 적용 : question_detail.html

  * ```python
    {% load pybo_filter %}
    
    <div class="card-text">{{ question.content|mark }}</div>
    #(...생략...)
    <div class="card-text">{{ answer.content|mark }}</div>
    ```




### AWS 라이트세일

* 아마존에서 운영하는 웹 서비스에 특화된 클라우드 서비스
* 서버 생성
* 한 달 뒤 서버 삭제 필수!



### Git

커밋 과정

* git init : git을 사용할 수 있도록 .git이 만들어짐 (숨김파일)
* .gitignore 생성 : 깃으로 관리하지 않을 대상을 기술하여 생성
* git add : 모든 파일을 추가하려면 *을 사용
* git commit : 커밋
  * -m : 커밋의 메시지를 입력하는 옵션
* git remote add origin : 깃허브 연결 - 로컬저장소와 원격저장소를 연결하는 것
* git push : 저장소에 올리기
* git pull : 이전에 올렸던 코드를 업데이트하거나 새로 커밋한 것을 내려받음





