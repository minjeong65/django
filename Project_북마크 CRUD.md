# 북마크 CRUD

### Create

* site name과 url을 입력받아 dropdown 버튼으로 생성
* dropdown - go / modify / delete
  * 각 버튼에 링크를 걸어서 생기는 밑줄을 지우려면  a태그에 style="text-decoration : none"를 넣어줌

**ERROR**

* integrityerror - NOT NULL constraint failed: book_book.site_name
  * book을 site_name없이 생성하려고 해서 오류가 남
  * create 창으로 넘어가서 site_name과 site_url을 입력하고 생성 버튼을 누르면 새로운 북마크가 생성되어야 하는데, 이 값이 계속 null인 상태여서 에러가 났다. 이유인즉슨, create.html에서 POST로 입력을 받을 때 input 태그에 name을 지정해 주는데, 이때의 name과 views.py의 create 함수에서 get에 사용한 이름을 같게 해야하는데,name을 input이 아닌 span태그에 잘못 넣어서 계속 입력 값을 얻어오지 못해 Null인 상태였던 것이다.

</br>

### UPDATE





</br>

### DELETE

* dropdown의 delete버튼을 누르면 해당 북마크를 삭제

* 삭제하기 전 확인 메시지를 띄움




**문제**

* 모달이 안뜸
  * 

