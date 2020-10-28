# Django

### Django로 개발하는 Todo-list 웹사이트
- 구름IDE로 개발하는 첫 장고 프로젝트.
- 앞으로 장고를 이용한 웹 개발의 초석.
- 구현 기능부분도 다루지만 개발 단계에 대해 이해하기 쉽게 만들 예정.
- django version: 3.06

- 개발순서 : 프로젝트 생성 -> settings.py 수정 -> 모델 계획 및 구현 ->

## 프로젝트와 앱 생성하기
`django-admin startproject PROJECT_NAME .`
- 터미널에서 위와 같은 명령으로 PROJECT_NAME 이라는 이름의 장고 프로젝트를 생성한다.

`python manage.py startapp APP_NAME`
- 터미널에서 위와 같은 명령으로 APP_NAME 이라는 이름의 앱을 생성한다.
- 프로젝트 안에 앱을 생성하는 느낌이다.
- 하나의 프로젝트에 여러개의 앱이 생성되기는 하나, 굳이 그래야하는 이유를 아직 모르겠다.

## settings.py 수정하기
```python
INSTALLED_APPS = [
  ...,
  'APP_NAME',
]

LANGUAGE_CODE = ko-kr'
TIME_ZONE = 'Asia/Seoul'
```
- `PROJECT_NAME/settings.py` 파일에 `INSTALLED_APPS` 안에, `APP_NAME` 을 추가해 준다. (이래야 장고에서 인식이 가능하다고 한다.)
- 아래에서 `LANGUAGE_CODE`와 `TIME_ZONE`을 각각 `ko-kr`와 `Asiz/Seoul`로 수정해준다. 아마 웹 내에 언어코드와 시간을 설정해주는 것 같다.


## 모델 계획하기
- 이제 Todo-list의 모델을 설계해보자.

|TodoList||TodoList_images||TodoList_files||
|---|---|---|---|---|---|
|필드명|데이터 타입|필드명|데이터 타입|필드명|데이터 타입|
|name|CharField|todo|ForeignKey|todo|ForeignKey|
|description|TextField|image|ImageField|file|FileField|
|date_created|DateField()|
|date_deadline|DateField()|
- 위 표와 같이 3개의 테이블을 만들건데, 마치 데이터베이스 설계하는 것과 비슷하다 느꼈다. (실제로 DB설계임.)
- 장고에서는 기본적으로 SQlite 데이터베이스를 제공한다. 따라서 SQlite 설계 작업이라 보면 될듯 싶다.
- 하나의 `TodoList`는 여러개의 이미지와 파일을 가질 수 있다.
- `TodoList_images`와 `TodoList_files`는 하나의 `TodoList`에 `ForeignKey`로 연결된다.

## models.py 작성하기
```python
from django.db import models
from datetime import date
import datetime

class TodoList(models.Model):
    name = models.CharField(max_length=40, verbose_name="할일제목")
    description = models.TextField(max_length=200, verbose_name="할일세부사항")
    date_created = models.DateField(auto_now_add=False, verbose_name="생성날짜")
    date_deadline = models.DateField(verbose_name="데드라인")
    
    def remaining_days(self):
        delta = self.date_deadline - date.today()
        days = delta.days
        return days
   
    def __str__(self):
        return f'{self.name} | {self.description} | {self.date_created} | {self.date_deadline}'

class TodoList_images(models.Model):
    todo = models.ForeignKey(TodoList, on_delete=models.CASCADE)
    image = models.ImageField(upload_to='todo/images/%Y/%m', blank=True)

class TodoList_files(models.Model):
    todo = models.ForeignKey(TodoList, on_delete=models.CASCADE)
    files = models.FileField(upload_to='todo/files/%Y/%m', blank=True)
```

- 모델을 계획했던대로 3개의 표를 각각 3개의 클래스로 선언한다.
- `from django.db import models`를 통해 python으로 SQlite를 작성하는 듯 하다. (자세한건 잘 모르겠고 일단 넘어가자.)
- 대충 class가 표와 대칭되고 변수가 표의 요소와 대칭되는 것 같다.
- class안에 메소드는 뭐하는 놈인지는 알겠지만, 어떻게 쓰는지는 아직 모르겠다.

## makemigrations와 migrate
`python manage.py makemigrations`
`python manage.py migrate`

- models.py를 수정하면 터미널에서 꼭 makemigrations과 migrate를 해줘야 한다.
- 처음에 자꾸 migrate가 안돼서 이거 땜에 한 시간 삽질했다.
- 알아보니 makemigrations와 migrate 순서대로 둘 다 해줘야 했다. (git commit과 git push같은 느낌인듯.)

---
[참고자료(장고쟁이)](https://djangojeng-e.github.io/2020/05/19/TodoList-4%ED%8E%B8-%EB%AA%A8%EB%8D%B8-%ED%99%95%EC%9D%B8%ED%95%98%EA%B8%B0/)
