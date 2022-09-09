### django form
* 사용자가 입력한 데이터가 우리가 원하는 형식이 맞는지 <u>**유효성 검증**</u>이 필요
* form : 
* 유효성 검사 도구 중 하나
* 유효성 검사를 단순화 및 자동화하여 생산성 향상
* 외부의 악의적 공격 및 데이터 손상에 대한 방어 수단
* django :
1. 렌더링을 위한 데이터 준비 및 재구성
2. 데이터에 대한 HTML forms 생성
3. 클라이언트로부터 받은 데이터 수신 및 처리

### form class
* 앱폴더에서 form.py에 ArticleForm 클래스 선언
* forms.Form 상속을 받아 클래스 선언
* views.py 에서 클래스 활용하여 인스턴스 생성 및 사용

#### form rendering option
* as_p
  * 각 단락을 \<p>태그로 감싸기
* as_ul
  * 각 단락을 \<li>태그로 감싸기
* as_table
  * 각 단락을 \<tr>태그로 감싸기

### widgets
* form fields
  * 입력에 대한 유효성 검사
  * 템플릿에서 사용
* widgets
  * html input 요소 렌더링 및 출력 처리
  * form fields에 할당
  * 렌더링만 처리할 뿐, 유효성 검사와는 관계x

### 작성 예시
* form field 공식문서 확인
  * https://docs.djangoproject.com/en/4.1/ref/forms/fields/
* built-in 위젯 공식문서 확인
  * https://docs.djangoproject.com/en/3.2/ref/forms/widgets/
* coding style guide
  * 위젯 등을 사용할 때, 스타일 가이드 확인하고 가이드에 맞게 작성 추천
  * https://docs.djangoproject.com/en/dev/internals/contributing/writing-code/coding-style/

### ModelForm
* 어떤 모델을 기반으로 form을 작성할지 Meta 클래스에 작성

#### Meta 클래스
* ModelForm의 정보를 작성
* model 속성에서 models.py에서 선언한 클래스를 참조!!! (호출이 아님!!!)
  * 클래스의 인스턴스가 되는 것이 아니라,
  * 클래스의 참조 값을 받음
  * <u>**필요한 시점에**</u> 사용하기 위해서,
  * 클래스의 필드나 속성을 내부적으로 참조하기 위해서,
  * 예시와 같이 작성
* '__all\_\_' 으로 모든 필드 포함 가능
* exclude로 특정 필드 제외 가능
# 예시사진
* metadate는 보통 데이터를 표현하기 위한 데이터를 의미

#### save 메서드

### Form vs ModelForm
* Form
  * 사용자로부터 받는 데이터가 DB에 영향을 주지 않고(저장x 수정x 등등), 
  * 단순하게 데이터로써 사용되는 경우에 사용
  * ex) 로그인할 때, 사용자 정보 확인에 사용만 하고 저장x
* ModelForm
  * 사용자로부터 받는 데이터가 DB에 영향을 주는 경우 사용
  * ex) 회원가입할 때
  * 데이터 유효 검사 후, save() 호출하여 DB에 저장

### Handling HTTP requests (중요!!)

### view decorators

#### allowed http methods

### substituting a custorm User model

#### 인증과 권한

#### custom user model
* custom user model로 대체
* built-in user model의 기본 인증 요구사항이 적절하지 않은 경우,
* AUTH_USER_MODEL을 override 해서 사용

### custom user model로 대체하기
* 공식문서 순서대로 진행!
1. AbstractUser 상속받아 커스텀 User 클래스 작성
2. settings.py에 AUTH_USER_MODEL 저장
3. accounts 앱의 admin.py에 커스텀 User 모델 등록

#### 중간에 user model을 수정하려고 한다면
* 권장x, 프로젝트 처음 시작할 때 설정해야함
* 그래도 해야된다면 DB 초기화 후 진행

### DB 초기화 방법
1. migrations파일 삭제
   * 번호가 붙은 파일만 삭제 ex) 0001
   * migrations 폴더 및 __init\_\_.py는 삭제x
2. db.sqlite3
3. migrations 진행
   * makemigrations
   * migrate

### HTTP Cookies
### HTTP
* Hyper Text Transfer Protocol
* 요청
  * 클라이언트(브라우저)가 서버에 요청
* 응답
  * 서버가 클라이언트(브라우저)로 응답

#### 특징
1. 비 연결 지향
2. 무상태

### Cookie

### login()

### logout(request)
* HTTP request 객체를 인자로 받고, 반환 값이 없음
* 로그인 안되어있을 때, 오류 x
* 현재 요청에 대한 session data를 DB에서 삭제
* 클라이언트의 쿠키에서 session id를 삭제
* session을 삭제하여 다른 사람이 동일한 웹 브라우저로, 이전 사용자의 session data에 접근하는 것을 방지