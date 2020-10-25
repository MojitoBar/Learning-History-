# Django

### Django로 개발하는 Todo-list 웹사이트
- 구름IDE로 개발하는 첫 장고 프로젝트.
- 앞으로 장고를 이용한 웹 개발의 초석.
- 구현 기능부분도 다루지만 개발 단계에 대해 이해하기 쉽게 만들 예정.
- django version: 3.06

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
---
[참고자료(장고쟁이)](https://djangojeng-e.github.io/2020/05/19/TodoList-4%ED%8E%B8-%EB%AA%A8%EB%8D%B8-%ED%99%95%EC%9D%B8%ED%95%98%EA%B8%B0/)
