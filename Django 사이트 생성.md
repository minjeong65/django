# Project 1 - Django 사이트 생성

* 가상환경 설치

  > python -m venv my

* 장고프로젝트 설치

  > 가상환경 진입 : c:\my\Scripts\activate
  > pip install django
  > django-admin startproject config .

* 앱설치

  > python manage.py startapp test01

* 서버구동

  > python manage.py runserver


  ※ 로켓발사확인!!!
* Reponse 원리

  > 요청발생 > config 에 있는 urls.py > urls.py 에는 views.py 로 연결 > views.py 의 함수에서 처리!! (request 를 받아서 response 를 반환해줘야함)

