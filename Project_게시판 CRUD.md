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


