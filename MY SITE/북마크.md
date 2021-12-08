# 북마크 CRUD

### [ SITE ]

#### Create

* site name과 url을 입력받아 dropdown 버튼으로 생성
* dropdown - go / modify / delete
  * 각 버튼에 링크를 걸어서 생기는 밑줄을 지우려면  a태그에 style="text-decoration : none"를 넣어줌

**ERROR**

* integrityerror - NOT NULL constraint failed: book_book.site_name
  * book을 site_name없이 생성하려고 해서 오류가 남
  * create 창으로 넘어가서 site_name과 site_url을 입력하고 생성 버튼을 누르면 새로운 북마크가 생성되어야 하는데, 이 값이 계속 null인 상태여서 에러가 났다. 이유인즉슨, create.html에서 POST로 입력을 받을 때 input 태그에 name을 지정해 주는데, 이때의 name과 views.py의 create 함수에서 get에 사용한 이름을 같게 해야하는데,name을 input이 아닌 span태그에 잘못 넣어서 계속 입력 값을 얻어오지 못해 Null인 상태였던 것이다.

</br>

#### UPDATE

* html 파일에서 객체를 통해서 값을 사용할 땐  model에 작성한 변수명을 사용할 것
  *  update.py에서 값을 이용할 때 model에 작성한 변수명과 동일하게 작성해야 하는데, views의 update 함수에서 임의로 정한 변수명을 사용해서 값이 전달되지 않는다고 생각했음

</br>

#### DELETE

* dropdown의 delete버튼을 누르면 해당 북마크를 삭제

* 삭제하기 전 확인 메시지를 띄움

</br>

### [READING LIST]

#### CREATE

* URL을 입력받으면 해당 포스트의 타이틀을 크롤링해서 Card의 제목으로 설정하고 url은 Card의 내용으로 설정함
  * 일정 글자수가 넘으면 생략하고 '...'을 붙임
* 해당 포스트의 이미지를 가지고  Card의 상단에 포스트 이미지를 붙이려고 했지만 각 포스트마다 이미지가 들어있는 태그가 달라서 패스
  * 여유 있으면 각 경우를 따져서 크롤링 하도록 할 예정
  * 원본 이미지를 가져오는 코드 필요
  * 일정한 비율로 resizing하는 부분 필요

</br>

**페이지 제목 크롤링**

```python
from bs4 import BeautifulSoupImage
import requests

url = request.POST.get('read_url')
res = requests.get(url)
soup = BeautifulSoup(res.text, "lxml")
title = soup.select("title")[0].text
```

</br>

**이미지 크롤링**

```python
from bs4 import BeautifulSoup
from PIL import Image
import requests


res=requests.get(f"<url>")
soup = BeautifulSoup(res.text, "html.parser")
soup = soup.find("figure")
route = soup.select("img")[0].get("src")
res = requests.get(route)
f=open(f"<folder>/<title>.png","wb")
f.write(res.content)
f.close()

#image resizing
img = Image.open('image/a.png')
img_resize = img.resize((500, 300))
img_resize.save("<folder>/<title>.png")
```

</br>

#### DELETE

* UPDATE는 따로 구현하지 않고 DELETE만 구현함

