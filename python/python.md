# Django

### Django로 개발하는 Todo-list 웹사이트
- 구름IDE로 개발하는 첫 장고 프로젝트.
- 앞으로 장고를 이용한 웹 개발의 초석.
- 구현 기능부분도 다루지만 개발 단계에 대해 이해하기 쉽게 만들 예정.
- django version: 3.06

- 개발순서 : 프로젝트 생성 -> settings.py 수정 -> 모델 계획 및 구현 -> view.py 작성 후 첫 화면 렌더 ->

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
`python manage.py makemigrations`<br/>
`python manage.py migrate`

- models.py를 수정하면 터미널에서 꼭 makemigrations과 migrate를 해줘야 한다.
- 처음에 자꾸 migrate가 안돼서 이거 땜에 한 시간 삽질했다.
- 알아보니 makemigrations와 migrate 순서대로 둘 다 해줘야 했다. (git commit과 git push같은 느낌인듯.)
- 이러니 migrations폴더에 계속해서 뭐가 쌓이던데 괜찮은건지 모르겠다...

## 모델 확인하기
```python
from django.contrib import admin

from .models import TodoList, TodoList_files, TodoList_images

admin.site.register(TodoList)
admin.site.register(TodoList_images)
admin.site.register(TodoList_files)
```

- 설계한 모델이 잘 되는지 확인하는 과정이다.
- 추가한 클래스를 불러와 `admin.site.register(CLASS_NAME)`을 통해 admin이 사용할 수 있게끔 하는것 같다.
- 모델을 확인하면서 알아낸 점인데, models.py의 `__str__(self)` 메소드는 admin주소(웹 사이트 주소 뒤에 /admin)로 들어갔을 때 표시되는 TodoList의 Title인 것 같다.
- 추가적으로 `python manage.py createsuperuser`를 통해 관리자 계정을 생성해주면 끝이다.

## admin.py 수정하기
```python
from django.contrib import admin 
from .models import TodoList, TodoList_files, TodoList_images 

class TodoList_fileInline(admin.StackedInline):
    model = TodoList_files 
    
class TodoList_imageInline(admin.StackedInline):
    model = TodoList_images

class TodoListAdmin(admin.ModelAdmin):
    inlines = [TodoList_fileInline, TodoList_imageInline]
    list_display = ('name', 'description', 'date_created', 'date_deadline', 'remaining_days')
    list_filter = ['date_created']
    
admin.site.register(TodoList, TodoListAdmin)
```

- admin 페이지에서 좀 더 알아보기 쉽게 만들기위해 admin.py를 수정한다.
- file, image를 inline으로 바꿔서 TodoList 추가하는 화면에 나오게끔 하는 내용이다.
- 위 두 class는 대충 StackedInline로 바꿔서 model로 리턴하는 것 같다.
- 그렇게 받은 model을 `class TodoListAdmin(admin.ModelAdmin)`의 inlines에 배열로 넣어 페이지에서 확인할 수 있다.
- list_dispay는 table에 맞는 이름대로 todo list 선택 페이지의 table title을 바꿔준다. (대충 보기 편해진다는 뜻.)
- list_filter는 admin 페이지의 왼쪽 중앙에 필터가 생긴다.
- 데이터가 있는 상태에서 admin을 수정해서 그런지, model을 어쩌다 건들였는지 `no such table`에러가 떠서 두 시간 넘게 삽질했다... db.sqlite3 파일을 지우고 다시 migrations, migrate를 하니 되는 것 같다.

## view.py 작성하기
```python
from django.shortcuts import render
from .models import TodoList

def home(request):
    todolists = TodoList.objects
    return render(request, "home.html", {'todolists': todolists})
```

- 데이터베이스를 화면에 뿌려주기 위해 view.py를 작성한다.
- `from .models import TodoList`를 통해 모델에서 값을 가져올 테이블을 import 한다.
- home 메소드를 만들어 todolists에 TodoList.objects, 즉 모든 테이블 정보를 오브젝트 형태로 넣는다.
- 이를 home.html파일에 todolists라는 이름으로 넘겨 render한다.

## tamplate (home.html) 작성하기
```html
{% for todolist in todolists.all %}
	<h1>할일 제목: {{ todolist.name }}</h1>
	<p>생성 날짜: {{ todolist.date_created }}</p>
	<p>데드라인 날짜: {{ todolist.date_deadline }}</p>
	<p>남은 일수: {{ todolist.remaining_days }}</p>
{% endfor %}
```

- todolists로 받은 정보를 html로 작성해 화면에 뿌려준다.
- 추가적으로 urls.py의 urlpatterns에 `path('', views.home, name='home'),`를 추가해준다. (기본 ' '경로에 만들어둔 home 메소드를 연결한다는 뜻.)

## 정적 파일 불러오기
```python
STATIC_URL = '/static/'

STATICFILES_DIRS = (
    os.path.join(BASE_DIR, 'static'),
) 
```

- 정적인 파일(css, image 등)을 사용하기 위해 settings.py에 위 코드를 수정해준다.
- 앞으로 정적인 파일의 경로는 static폴더를 기준으로 한다는 뜻.
- 정적인 파일을 사용할 html에 맨 위에 `{% load static %}`을 추가해줘야한다.

---
[참고자료(장고쟁이)](https://djangojeng-e.github.io/2020/05/19/TodoList-4%ED%8E%B8-%EB%AA%A8%EB%8D%B8-%ED%99%95%EC%9D%B8%ED%95%98%EA%B8%B0/)
