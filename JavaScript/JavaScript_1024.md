# JavaScript
## 221024 JavaScript 기초
### 목표
* JavaScript 기초 문법 정리


## browser APIs
* 데이터 제공, 오디오 재생 등 수행

## DOM Document Object Model
* 문서 객체 모델
* 프로그래밍 언어가 DOM 구조에 접근할 수 있는 방법 제공
* HTML 문서를 구조화 하여 각 요소를 객체로 취급
* 문서를 논리 트리로 표현
* DOM 메서드를 사용하여 프로그래밍적으로 트리에 접근
* 웹 페이지의 객체 지향 표현, javascript 같은 스크립트 언어로 DOM 수정

### Window object
* 가장 최상위 객체
* DOM을 표현하는 창

### document object


### DOM 조작
* DOM 조작 순서
1. 선택 
2. 조작
* **항상 <u>선택 후 조작</u> 순서에 유의!!!**

### 선택 메서드
* document.querySelector(selector)
  * 제공한 선택자와 일치하는 element 한 개 선택
  * 제공한 css selector를 만족하는 **첫 번째 element 객체 반환**
* document.querySelectorAll(selector)
  * 제공한 선택자와 일치하는 여러 element 선택
  * 매칭 할 하나 이상의 셀렉터를 포함하는 유효한 css selector 인자 받음
  * 제공한 css selecor를 만족하는 **nodelist 반환**

### nodelist
* index로만 접근 가능
* forEach 메서드 등 배열 메서드 사용 가능
* nodelist는 기본적으로 라이브 컬렉션
  * 변경사항을 신시간으로 반영o
* 하지만 querySelectorAll()에 의해 반환되는 nodelist는 정적 컬렉션
  * DOM의 변경사항을 실시간을 반영x
  * 특정 변수에 캐시 가능
  * 순회 중 값이 변하지 않아 변수 값 사용 가능

### 조작 메서드
* document.createElement(tagName)
  * 작성한 tagName의 html요소를 생성하여 반환
* Node.innerText
  * Node 객체와 그 자손의 텍스트 컨텐츠 DOMString 표현
  * 태그와 태그 사이의 내용 부분 raw text
* Node.appendChild()
  * 한 Node를 특정 부모 Node의 자식 NodeList 중 마지막 자식으로 삽입
  * 한번에 하나의 Node만 추가 가능
  * 추가된 Node 객체 반환
  * 주어진 Node가 이미 존재하는 다른 Node를 참조한다면, 현재 위치에서 새로운 위치로 이동
* Node.removeChild()
  * Dom에서 자식 Node 삭제
  * 삭제된 Node 반환
* Element.getAttribute(attributeName)
  * 해당 요소의 지정된 값(문자열) 반환
  * attributeName은 얻고자 하는 속성의 이름
* Element.setAttribute(name, value)
  * 지정된 요소의 값을 설정
  * 속성이 이미 존재하면, 속성 값 갱신
  * 속성이 존재 하지않으면, 지정된 이름과 값으로 속성 추가

### Element.classList
* 엘리먼트의 클래스 목록에 접근
* 사용할 수 있는 메서드 확인
* https://developer.mozilla.org/ko/docs/Web/API/Element/classList
* toggle(String [, force])
  * 클래스 값을 토글
  * 하나의 인수만 있을 때 : 
    * 클래스가 존재하면, 클래스 제거 후 false 반환
    * 존재하지 않으면, 클래스 추가 후 true 반환
  * 두번째 인수가 있을 때 :
    * 두번째 인수가 true 이면, 클래스 추가
    * 두번째 인수가 false 이면, 클래스 제거

## Event
* 프로그래밍하고 있는 시스템에서 일어나는 사건 acction, 발생 occurrence
* 각 이벤트에 대해 조작할 수 있도록 특정 시점을 시스템이 알려주는 것
* ex) 마우스 클릭, 키보드 입력, 브라우저 열고 닫기, 데이터 제출, 텍스트 복사 등등
  
## Event object
* 네트워크 활동
* 사용자와의 상호작용
* 같은 사건의 발생을 알리는 객체
* Event 발생
  * 사용자의 행동으로 발생
  * 특정 메서드를 호출하여 프로그래밍 적으로 만들어낼 수 있음
* DOM 요소는 Event를 **수신**
* 받은 Event를 **처리**
  * 이벤트 처리기 Event handler인 addEventListener() 를 다양한 html요소에 **<u>부착</u>**해서 처리

### Event handler
* addEventListener()
* EventTarget.addEventListener(type, listener)
* 대상 (EventTarget)에 특정 이벤트 (type)가 발생하면 할 일(listener)을 등록
* 지정한 Event가 대상에 전달될 때마다 호출할 함수를 설정
* Event를 지원하는 모든 객체를 대상을 지정 가능
* type
  * 반응 할 Event 유형을 나타내는 대소문자 구분 문자열
  * input, click, submit 등등   
  * mdn 참고
  * https://developer.mozilla.org/ko/docs/Web/Events
* listener
  * 지정된 타입의 Event를 수신할 객체
  * JavaScript fnction 객체 (콜백함수) 로 작성
  * 콜백 함수는 발생한 Event의 데이터를 가진 Event 객체를 유일한 매개변수로 받음

## Event 취소
* event.preventDefault()
* Event의 기본 동작을 중단
* HTML 요소의 기본 동작을 작동하지 않게 막음

## lodash
* JavaScript 유틸리티 라이브러리
* 자료구조를 다룰 때 편리한 유틸리티 함수 제공
* ex) reverse, sortBy, range, random

## this
* 어떠한 object를 가리키는 키워드
* python의 self와 같음
* 인스턴스 자기자신을 가리킴
* 함수가 호출될 때 this를 암묵적으로 전달 받음
* 하지만 동작방식은 다름
* **함수 호출 방식**에 따라 this에 바인딩 되는 객체가 달라짐
* 함수를 선언할 때x
* 함수를 호출할 때, 어떻게 호출 되었는지에 따라 동적으로 this 결정

### 전역 문맥에서의 this
* 브라우저의 전역 객체인 window 가리킴
* 전역 객체는 모든 객체의 유일한 최상위 객체

### 함수 문맥에서의 this
* this의 값은 함수를 호출한 방법에 의해 결정
* 단순 호출
  * 전역 객체를 가리킴
  * 브라우저 : window
  * Node.js : global
* Method : 객체의 메서드
  * 해당 객체와 바인딩
* Nested : 함수안의 콜백 함수
  * 콜백 함수로 단순 호출해버리면 전역 객체를 가리키게 됨
  * 그래서 **<u>화살표 함수</u>**로 호출
  * 화살표 함수에서 this는 자신을 감싼 정적 범위 의미
  * 즉, 자동으로 한 단계 상위 범위의 객체를 바인딩
```javascript

```

### 화살표 함수에서의 this
* Lexical scope
* 호출 위치와 상관없이 **상위 스코프**를 가리킴
* 함수를 **어디에 선언했는지에 따라 결정**
* static scope라고도 함
* 일반적인 프로그래밍 언어 방식
* **함수 내의 콜백 함수의 경우, <u>화살표 함수 사용 권장</u>**