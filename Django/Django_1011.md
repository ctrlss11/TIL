# Django
## 221011 Static / Media
### 목표
* Static file, Media file 사용

## Static files 정적 파일

## Media files
* 사용자가 웹에서 업로드하는 정적 파일
* user uploaded static file

### 웹 서버와 정적 파일
* 특정 위치 URL 에 있는 자원을 요청 HTTP request 받아서
* 응답 HTTP response 를 제공 serving 하는 것

## Django에서 정적파일 사용
1. settings.py 에서 INSTALLED_APPS 에 django.contrib.staticfiles 포함
2. seetings.py 에서 STATIC_URL 정의
3. 앱의 static 폴더에 정적 파일 위치
4. template 에서 static 템플릿 태그 사용, 정적 파일의 URL 만들기
```html
{% load static %}

<img src="{% static 'sample_img.jpg' %}" alt="sample image">
```

### django template tag
* {% load %}
  * load tag
  * 템플릿 태그와 필터를 로드
* {% static '경로' %}
  * static tag
  * STATIC_ROOT 에 저장된 정적 파일에 연결

### Static files 관련 settings
1. STATIC_ROOT
  * 배포 환경에서 Django의 모든 정적 파일을 다른 웹 서버가 제공하기 위해 사용
  * collectstatic이 배포를 위해 정적 파일을 수집하는 디렉토리의 절대 경로
  * 개발 과정에서 settings.py의 DEBUG = True 이면 작동 x
2. STATICFILES_DIRS
  * 기본경로 외에 추가적인 정적 파일 경로 목록을 정의하는 list
3. STATIC_URL
  * STATIC_ROOT 에 있는 정적 파일을 참조할 때 사용할 URL
  * 실제 파일이나 디렉토리가 아니고, URL로만 존재

### static file 가져오기
1. 기본 경로
2. 추가 경로

## Media files

### ImageField()
* 이미지 업로드에 사용하는 모델 필드
* FileField 를 상속받는 서브 클래스
  * FileField 의 모든 속성, 메서드 사용
  * 사용자가 업로드한 객체가 유효한 이미지인지 유효성 검사
* ImageField 인스턴스는 최대 길이 100자인 문자열로 DB에 생성
  * max_length 사용
* Pillow 라이브러리 설치

### FileField()
* 파일 업로드에 사용하는 모델 필드
* 선택인자
  * upload_to : 경로 지정
  * storage
```python
FileField(upload_to='', storage=None, max_length=100)
```

### Media files 사용
1. setting.py 에서 MEDIA_ROOT, MEDIA_URL 설정
2. upload_to 속성을 정의하여 MEDIA_ROOT의 하위 경로 지정

### Media files 관련 settings
1. MEDIA_ROOT
  * 사용자가 업로드 할 미디어 파일들을 저장할 디렉토리의 절대 경로
  * DB에는 파일의 경로를 저장
  * STATIC_ROOT와 반드시 다른 경로로 지정
2. MEDIA_URL
  * MEDIA_ROOT 에서 제공되는 미디어 파일을 처리하는 URL
  * 업로드 된 파일의 URL을 만들어 주는 역할
  * STATIC_URL과 반드시 다른 경로로 지정

### 개발 단계에서 사용자가 업로드한 미디어 파일 제공
* https://docs.djangoproject.com/en/4.1/howto/static-files/#serving-files-uploaded-by-a-user-during-development
* 사용자에게 제공하기 위해서는 업로드 된 파일의 URL이 필요
  * 업로드 된 파일의 URL : settings.MEDIA_URL
  * 위 URL을 통해 참조하는 파일의 실제 위치 : settings.MEDIA_ROOT

### ImageFIeld option
* blank
  * balnk=True 이면 빈 문자열이 저장
  * 유효성 검사에서 빈 문자열로 사용
* null
  * null=True 이면 빈 값을 DB에 NULL로 저장
* CharField, TextField와 같은 문자열 필드에는 null 옵션 사용을 지양
* 문자열에서의 데이터 없음에 대한 표현은 빈 문자열로 사용하는 것이 규칙
* NULL 과 빈 문자열 두 개를 사용하면, DB의 일관성 측면에서 문제

### 사용자 지정 업로드 경로
1. 문자열 값 경로 지정
2. 함수 호출

## Image Resizing
* 원본 이미지를 서버에 그대로 로드 하는 것은 부담이 있음
* 여러가지 방법이 있지만 그 중,
* 업로드 될 때 이미지 자체를 resizing 하는 방법
  * django-imagekit 설치 후 INSTALLED_APPS 에 등록

### django-imagekit
* 썸네일, 해상도, 사이즈, 색깔 등 조정
* django-imagekit 라이브러리 사용법 검색

### 썸네일 만들기
1. 원본 이미지 저장 x
2. 원본 이미지 저장 o

## QuerySet API
* Field lookups