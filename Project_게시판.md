# 게시판

### models, views

* models : subject, writer, content, photo

* index : 메인 화면
* detail : 선택한 게시글 
* create : 새 글 작성 
* update : 글 수정 ( 작성자만 가능 )
* delete : 해당 글 삭제 ( 작성자만 가능 )

</br>

### CREATE

* Write버튼
  * 로그인 상태일 경우 create 페이지로 이동
  * 로그인 상태가 아닌 경우 로그인 페이지로 이동
* 이미지 첨부
  * create / update.html
    * < input type="file" **name = "photo" **class="form-control" id="inputGroupFile04" aria-describedby="inputGroupFileAddon04" aria-label="Upload" >
  * detail.html 
    * < img src = "{{ **b.getphoto** }}" >
      * context = { 'b': b }

</br>

**ERROR**

* no such column : board_board.photo
  * model을 자주 바꿔서 makemigrations / migrate를 하는 과정에서 데이터베이스가 꼬여서 생긴 에러
  * 해당 앱의 migrations의 init 파일을 제외한 모든 파일 제거, db.sqlite3 제거 후 migration 다시 실행
  * db를 제거하므로 이전의 user와 데이터가 모두 사라짐을 유의

</br>

### UPDATE

* user가 작성자인 경우 user의 글 수정
* 기존 값들을 유지한 채 수정
  * < input > : value에 값 지정
  * < textarea > : disabled 설정하고 태그 밖에 값 지정

</br>

### DELETE

* user가 작성자인 경우 user의 글 삭제
* 실수를 방지하기 위해 modal 생성

</br>

### PAGINATION

**from django.core.paginator import Paginator** 

* 페이징을 위한 클래스

</br>

**Paginator ( *object_list* , *per_page* , *orphans=0* , *allow_empty_first_page=True* )**

* 필수 인수 
  * object_list : 페이징할 객체
  * per_page : 한 페이지에 보여줄 목록 개수
* 선택 사항
  * orphans : 마지막 페이지에 목록 수가 적을 때 이전 페이지에 같이 넣을 수 있도록 하는 기준 개수
    * default : 0 => 페이지가 결합되지 않음, 마지막 페이지에 한 개 이상의 개체가 있음
  * allow_empty_first_page=True : 첫 페이지를 비우도록 할 것인지
    * False와 object_list가 비어 있으면 EmptyPage 오류 발생

</br>

**페이지 GET**

* page = request.GET.get('page','1')
  *  GET 방식으로 호출된 URL에서 page값을 가져올 때 사용
  *  page값 없이 호출된 경우에는 디폴트로 1이라는 값을 설정

</br>

**페이지 리턴**

* Paginator.get_page(*number*) : 1부터 인덱싱하여 페이지 개체를 반환하는 동시에 범위를 벗어난 잘못된 페이지 번호를 처리
  * 페이지가 숫자가 아닐 경우 첫 번째 페이지 반환. 페이지 번호가 음수이거나 페이지 수보다 크면 마지막 페이지 반환
  * Paginator(..., allow_empty_first_page=False)를 지정했을 때 object_list가 비어 있는 경우에만 EmptyPage 예외를 발생시킴
* Paginator.page(*number*) : 1부터 인덱싱하여 페이지 개체를 반환. 
  * int()로 정수 변환할 수 없는 경우 PageNotAnInteger를 발생시킴
  * 지정된 페이지 번호가 없는 경우 InvalidPage를 발생시킴

</br>

**페이징 객체 속성**

| 항목                 | 설명                                |
| :------------------- | :---------------------------------- |
| paginator.count      | 전체 게시물 개수                    |
| paginator.per_page   | 페이지당 보여줄 게시물 개수         |
| paginator.page_range | 페이지 범위                         |
| number               | 현재 페이지 번호                    |
| previous_page_number | 이전 페이지 번호                    |
| next_page_number     | 다음 페이지 번호                    |
| has_previous         | 이전 페이지 유무                    |
| has_next             | 다음 페이지 유무                    |
| start_index          | 현재 페이지 시작 인덱스(1부터 시작) |
| end_index            | 현재 페이지 끝 인덱스               |

</br>

**페이징 기능**

| 페이징 기능               | 코드                                                         |
| :------------------------ | :----------------------------------------------------------- |
| 이전 페이지가 있는지 체크 | `{% if question_list.has_previous %}`                        |
| 이전 페이지 번호          | `{{ question_list.previous_page_number }}`                   |
| 다음 페이지가 있는지 체크 | `{% if question_list.has_next %}`                            |
| 다음 페이지 번호          | `{{ question_list.next_page_number }}`                       |
| 페이지 리스트 루프        | `{% for page_number in question_list.paginator.page_range %}` |
| 현재 페이지와 같은지 체크 | `{% if page_number == question_list.number %}`               |

</br>

**active 기능**

* 현재 페이지를 표시하기 위해 활성화 기능 추가
* class="page-item {% if blist.number == i %}active{% endif %}"

</br>

**mathfilters**

* 한 화면에 페이지 바 표시 제한을 위한 연산 필터
* install pip django-mathfilters
* mathfilters 앱 등록(settings.py)
* {% load mathfilters %}
* 연산
  * **sub** – 뺄셈
  * **mul** – 곱셈
  * **div** – 나눗셈
  * **intdiv** – 몫 연산
  * **abs** – 절댓값
  * **mod** – 나머지 연산
  * **addition** – 덧셈

* 예시

  ```
  <li>8 + 3 = {{ 8|add:3 }}</li>
  
  <li>13 - 17 = {{ 13|sub:17 }}</li>
  ```

</br>

**현재 페이지 양쪽으로 페이지 번호 두 개씩 뜨도록 구현(잠시 미룸)**

</br>

**ERROR**

* UnboundLocalError: local variable 'b' referenced before assignment
  * 모델에 없는 값을 사용하려고 하기 때문

