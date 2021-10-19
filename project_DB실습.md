# MTV 모델에서 "M" 을 다뤄보자

### 1. ORM
※ ORM 에 대한 이해
원래 서버에서 DB 를 다루기 위해서는 Database 언어를 따로 다뤄야하지만,
이를 object-relation 의 Mapping 으로 처리하는 것!!
따라서, class 를 알아야한다!!

A Class 는 "A라면 가지고 있어야하는 속성과 특징을 변수와 함수 즉, 코드 집합으로 묶어놓은 집합" 이다!

> 객체1 = A( )  

위와 같은 방식으로 객체를 생성하며, 이 객체1을 "A Class 의 인스턴스다" 라고 표현하기도 한다!

A 라는 테이블에서 각각의 필드를 "A 테이블이라면 가지고 있어야하는 속성" 으로 바라보고,
A 테이블에 있는 데이터들을 각각 "A Class 의 인스턴스" 로 규정하고 코딩하면 된다!!



### 2. TABLE 만들기 (models.py 에 설정) 

* num, name 을 가지고 있는 Student 테이블을 만들자 

  ( => num, name 을 가지고 있는 Student Class 을 만들자)

  ```python
  class Student(models.Model):
  	num = IntegerField()
  	name = CharField(max_length=30)
  
  comment = TextField()
  ```

Table 을 이제 올려줘야한다!! (migration : 데이터모델을 바꾸는 것! 한마디로 DB 정보가 바뀌는것)



### 3. DB 등록하기

두 가지 핵심 명령어를 살펴보자

 - python manage.py makemigrations
   > settings.py 의 INSTALLED_APPS 에 있는 내용들을 점검하여 DB와 관련하여 변화가 일어났는지 체크
   > 변화가 있다면 DB 에 올릴 준비를 해주는 파일인 0001 과 같은 파일이 생성된다.
  > 따라서, 위 명령어에서 등록된 Table 을 DB 에 올리려면 settings.py 에 해당 App(st) 을 등록해주어야함.
  > 'st.apps.StConfig' 등록!

 - python manage.py migrate
   
   > makemigrations 가 있는 상태에서 실제로 DB 를 등록하는 명령어!!



### 4. 직접 데이터 추가하기

 - python manage.py shell
   
   가상환경을 토대로 python shell 실행 ( ※주의※  >>> 가 있는 곳이 shell )

   ```python
   from st.models import Student
   
   st1 = Student(num=100, name="han", comment="착함")
   st1.save()
   st2 = Student(num=200, name="kim", comment="모험심이 많음")
   st2.save()
   st3 = Student(num=300, name="kang", comment="오늘은 펜트하우스 마지막방송")
   st4.save()
   ```

> 위와 같이 테이블에 한 줄(이걸 레코드라고 하기도함) 추가하려면, Student 의 인스턴스 생성 후 save 해주면됨



### 5. 데이터 조회하기

```python
all_st = Student.objects.all()
```

 > Student 모든 데이터들을 가져옴! (Student 의 인스턴스들의 리스트반환)
 > 따라서 for 문을 돌리면 i 에는 Student 의 인스턴스가 들어감

```python
 for i in all_st:
 	print(i.num, i.name, i.comment)
 a = Student.objects.get(name="han")
```

 > 특정 인스턴스 검색 
 >  print(a.num, a.name, a.comment)



### 6. HTML 문서에 데이터를 넘겨보자!!

render 의 context 인자(Dictionary 형)에 실어주면 됨!!

```python
 def index(request):
     a = 10
     b = range(10)
     context = {
        'con1' : a,
 		'con2' : b
     }
	return render(request, "board/index.html", context)
```

index.html 에서 con1, con2 변수로 사용할 수 있음!!
데이터를 보냈으니 이 변수를 활용해서 HTML 문서에 나타낼 수 있어야하죠?

### 7. Template Tag : HTML 문서에서 python 구문을 사용할 수 있도록!

 - {%  %} : 구문(if, for)      =>  { % 는 꼭 붙여서 표기!!
 - {{  }} : 객체나 변수

※ 이 때, 주의할 점은 Template Tag 에서는 칸 띄우기 개념이 없는
HTML 문서에 표현된다. 따라서 종속문장의 구분이 없기 때문에 매 구문 마다
**{% endfor %} , {% endif %} **와 같은 마무리를 지어주지 않으면 안된다.

```html
if 1:            =>     	{% if 1 %}
   print(1)             		<h1> 1 </h1> 
   if 2:						{% if 2 %}
       print(2)						<h1> 2 </h1>   
else:							{% endif %}
   print(3) 				{% else %}
								<h1> 3 </h1>
							{% endif}
```

또한, for 문의 종속문장에서 주로 사용되는 표현(변수처럼 사용)에 대해서 정리해보자
forloop.counter : for 문 안의 현재반복 횟수를 저장 (start value : 1)
forloop.counter0 : for 문 안의 현재반복 횟수를 저장 (start value : 0)
forloop.first : 첫번째 반복에서만 True
forloop.last : 마지막 반복에서만 True
