# 조회/정렬

### 데이터베이스

Django는 기본적으로 SQLite를 사용하도록 설정되어 있음

</br>

### select / option

* select : 드롭다운을 만드는 틀
* option : 드롭다운 요소
* 드롭다운의 내부 아이템을 누르면 get방식으로 url에 value값이 전달됨
* submit하기 위해서는 버튼을 생성하거나 속성으로 `onchange="this.form.submit()"`를 넣어줌

</br>

### 정렬 데이터

* 추천순(voter)

* 댓글순(reply)

* 최신순(ctime)

  ```django-python
  # 한국시간으로 설정
  LANGUAGE_CODE = 'ko-kr'
  TIME_ZONE = 'Asia/Seoul'
  ```

</br>

### 사용함수

* **`annotate`**  :  `Count`를 이용하여 새로운 필드를 만듦
* **`Count`** : 추천수, 댓글수를 세기 위해 사용
* **`order_by`** : 주어진 컬럼을 기준으로 정렬

</br>

<hr>

### 조회 데이터

* 제목(subject)
* 내용(content)
* 작성자(writer)
* 댓글 작성자(reply__replyer)

</br>

### 사용함수

* **`filter`** : 조건에 해당하는 값만 가져옴

  > Board.objects.filter(필드명=조건값)

  * 2개 이상의 필드가 사용될 때는 보통 and로 묶어줌

  * OR로 묶기 위해서는 Q()사용

    > from django.db.models import Q
    >
    > Board.objects.filter(Q(subject="제목")|Q(content = "내용"))

</br>

### 조회 관련 함수

**`all`** : 모든 데이터를 가져옴

> Board.objects.all()

</br>

**`exclude`** : 조건에 해당하는 값을 제외하고 가져옴

> Board.objects.exclude(필드명=조건값)

</br>

**`get`** : 조건에 해당하는 값을 가져옴

> Board.objects.get()

* 반드시 1개의 데이터만 인수로 넣을 수 있음
* 0개이거나 2개 이상은 에러 발생

</br>

**`first`** : 가장 첫번째 데이터를 가져옴

> Board.objects.first()

</br>

**`last`** : 가장 마지막 데이터를 가져옴

>  Board.objects.last()

</br>

**`index, slice`** : 인덱싱, 슬라이싱을 통해 데이터를 가져옴

* 음수는 사용 불가

> Board.objects[index]
>
> Board.objects[start:stop:step]

</br>

### Filter 조건 키워드

`__startswith / __istartwith` : 지정한 문자열로 시작하는 자료 검색 (대소문자 구분O / 구분X)

`__endswith / __iendswith` : 지정한 문자열로 끝나는 자료 검색 (대소문자 구분O / 구분X)

`__contains / __icontains` : 지정한 문자열을 포함하는 자료 검색 (대소문자 구분O / 구분X)

`__is null` : 해당 열의 값이 null인 자료 검색

`__in` : 주어진 리스트 안에 존재하는 자료 검색

</br>

**Error**

* no such column: board_board.ctime (혹은)
* django.db.utils.OperationalError: table board_board has no column named ctime
  * migrate을 새로 해도 테이블이 생성되지 않음
  * 해결 : SQLite 프로그램을 통해 직접 테이블 추가

