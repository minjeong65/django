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

* django-mathfilters 설치
  * mathfilters 앱 등록(settings.py)
  * {% load mathfilters %}

* from django.core.paginator import **Paginator** : 페이징을 위한 클래스

* `Paginator` ( *object_list* , *per_page* , *orphans=0* , *allow_empty_first_page=True* )

  * 필수 인수 - object_list : 페이징할 객체, per_page : 한 페이지에 보여줄 목록 개수

* page = request.GET.get('page','1') 

* 페이징 객체 속성

  * | 항목                 | 설명                                |
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
    | end_index            | 현재 페이지의 끝 인덱스(1부터 시작) |

</br>

* 페이징 기능

  * | 페이징 기능               | 코드                                                         |
    | :------------------------ | :----------------------------------------------------------- |
    | 이전 페이지가 있는지 체크 | `{% if question_list.has_previous %}`                        |
    | 이전 페이지 번호          | `{{ question_list.previous_page_number }}`                   |
    | 다음 페이지가 있는지 체크 | `{% if question_list.has_next %}`                            |
    | 다음 페이지 번호          | `{{ question_list.next_page_number }}`                       |
    | 페이지 리스트 루프        | `{% for page_number in question_list.paginator.page_range %}` |
    | 현재 페이지와 같은지 체크 | `{% if page_number == question_list.number %}`               |

</br>

* active 기능
  * 현재 페이지를 표시하기 위해 활성화 기능 추가
  * class="page-item {% if blist.number == i %}active{% endif %}"



**ERROR**

* UnboundLocalError: local variable 'b' referenced before assignment
  * 모델에 없는 값을 사용하려고 하기 때문

