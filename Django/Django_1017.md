# Django
## 221017 REST API
### 목표
* REST API 사용


## HTTP
* Hyper Text Transfer Protocol
* resource를 가져올 수 있는 protocol
  * 리소스 : HTTP 요청의 대상
* 클라이언트-서버 프로토콜
* request 요청 : 클라이언트에서 요청
* response 응답 : 서버에서 응답
* **Stateless 무상태**
  * 연결에서 연속적으로 수행되는 요청 사이에 링크가 없음
  * 응답을 끝내고 연결을 끊으면, 상태 정보 유지x
  * 쿠키와 세션으로 서버 상태를 요청과 연결
  * ex) 장바구니

### HTTP Request Methods
* GET
  * READ
  * 서버에 리소스의 표현을 요청
  * 조회에서만 사용
* POST
  * CREATE
  * 데이터를 지정된 리소스에 제출
  * 서버의 상태 변경
* PUT
  * UPDATE
  * 리소스 수정
* DELETE
  * DELETE
  * 리소스 삭제

### HTTP response status codes
1. Informational responses : 100-199
2. Successful responses : 200-299
3. Redirection messages : 300-399
4. Client error responses : 400-499
5. Server error responses : 500-599

## URI
* Uniform Resource Identifier 통합 자원 식별자
* 하나의 리소스를 가리키는 문자열
* 리소스 식별에 사용
  * URL 웹주소 경로 : 위치로 식별
  * URN 이름 : 이름으로 식별

## URL
* Uniform Resource Locator 통합 자원 위치
* 리소스의 주소

### URL 구조
### Scheme (or Protocol)
* 브라우저가 리소스를 요청하는데 사용하는 프로토콜
* https

### Authority
* :// 으로 authority 구분
* domain과 port로 구성
* 둘은 : 으로 구분

### Domain Name
* 요청 중인 웹 서버
* IP주소로 사용하기 불편해서 domain name 사용
* 직접적인 IP주소도 사용 가능
* ex) google.com 은 142.251.42.142

### Port
* 웹 서버의 리소스에 접근하는데 사용되는 Gate
* HTTP와 HTTPS는 생략 가능
  * HTTP - 80
  * HTTPS - 443
* Django는 8000이 기본 포트

### Path
* 웹 서버의 리소스 경로
* 추상화된 형태의 구조 표현

### Parameters
* 웹 서버에 제공하는 추가적인 데이터
* & 으로 구분
* key-value 목록
* 서버는 리소스를 응답하기 전에 파라미터를 사용하여 추가 작업 수행

### Anchor
* 리소스의 다른 부분에 대한 앵커
* #(부분식별자)으로 구분
* #이후 부분은 서버에 전송x
* ex) 현재 페이지에서 특정 위치(스크롤)로 이동

### URN
* Uniform Resource Name 통합 자원 이름
* 위치에 영향x, 이름으로 자원 식별
* 웹에서는 대부분 URL 사용
* ex) ISBN 국제표준 도서번호

## API
* Application Programming Interface
* 애플리케이션과 프로그래밍 언어로 소통
* API로 복잡한 코드를 추상화하여 쉽게 사용

## REST
* Representational State Transfer
* API server 개발을 위한 SW 설계 방법론
* 소프트웨어 아키텍쳐 디자인 제약 모음
* REST 원리를 따르는 시스템을 RESTful하다 라고 함
* 자원을 정의하고 자원에 대한 주소를 지정하는 전반적인 방법 서술

## 주소를 지정하는 방법
1. 자원 식별 - URL
2. 자원에 대한 행위 - HTTP Methods
3. 자원 표현 - JSON

## JSON
* JavaScript 표기법을 따른 문자열
* key-value 형태의 구조
* 현재 API에서 가장 많이 사용하는 데이터 타입
* 사람에게 직관적, 기계가 파싱(해석, 분석)하기 쉬움

***


## RESTful하다?? (면접 필수)
* aws 문서
* https://aws.amazon.com/ko/what-is/restful-api/
* 지켰을 때 오는 장점


## HTTP response status code
* data를 주고받기, http 응답코드 반환

## Serialization
* 직렬화
* 데이터 구조나 객체 상태를 검퓨터 환경에 저장하고,
* 나중에 재구성 할 수 있는 포맷으로 변환하는 과정
* 어떤 환경에서도 나중에 다시 쉽게 사용할 수 있는 포맷으로 변환하는 과정
* json이 보편적인 변환 포맷으로 사용

## JSON

## 유효성 검사
* 사용자가 넘기는 data는 