# 게시판 CRUD

### models, views

* models : subject, writer, content

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

</br>

### UPDATE

* user가 작성자인 경우 user의 글 수정

* 기존 값들을 유지한 채 수정

</br>

### DELETE

* user가 작성자인 경우 user의 글 삭제

