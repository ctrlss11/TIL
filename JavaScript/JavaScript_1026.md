# JavaScript
## 221026 JavaScript 기초
### 목표
* JavaScript에서의 비동기 처리


## Synchronous 동기
* 모든 일을 순서대로 하나씩 처리
* 이전 작업이 끝나야 다음 작업 시작
* 웹에서의 요청과 응답을 동기식으로 처리하면
* 요청을 보내고 응답이 올때까지 대기, 응답 후 다음 로직 처리

## Asynchronous 비동기
* 작업을 시작한 후 결과를 기다리지 않고 다음 작업 처리
* 병렬 작업
* 웹에서의 요청과 응답을 비동기식으로 처리하면
* 응답이 빨리오는 작업부터 처리

### 비동기를 사용하는 이유
* 사용자 경험 때문
* 동기로 처리하면 데이터를 모두 불러온 뒤에 다음 로직 처리
* 이는 프로그램이 멈춘 듯한 사용자 경험을 만들게 됨
* 비동기로 처리하면, 응답이 오는 순서대로 처리하게 됨

## JavaScript의 비동기 처리
* javaScript는 single thread 언어
* thread 작업을 수행하는 주체
  * multie-thread : 작업을 수행하는 주체가 여러개
  * single-thread : 작업을 수행하는 주체가 한개
* single thread라서 하나의 작업을 요청한 순서대로 처리할 수 밖에 없음
* 따라서 비동기 처리를 할 수 있도록 도와주는 환경 필요

### Runtime 런타임
* 특정 언어가 동작할 수 있는 환경
* JavaScript에서 비동기 처리는 Browser나 Node 환경에서 처리
* Browser 환경 구성
  1. JavaScript Engine의 Call Stack
  2. Web API
  3. Task Queue
  4. Event Loop

## 비동기 처리 동작
1. 모든 작업은 Call Stack 으로 들어가 LIFO로 처리
2. 오래 걸리는 작업이 Call Stack으로 들어오면 Web API로 보내 별도 처리
3. Web API에서 처리가 끝난 작업은 Task Queue 에 순서대로 들어감 (대기열)
4. Event Loop가 Call Stack이 비어있는지 계속 체크
5. Call Stack의 처리가 끝나 비게 되면, Task Queue 의 작업들을 FIFO로 Call Stack으로 보냄
* JavaScript는 single thread 언어로 한 번에 하나의 작업을 수행하는 동기적 처리
* 브라우저 환경에서는 비동기 처리가 가능
* Web API에서 처리된 작업이 Task Queue를 거쳐 Event Loop에 의해 Call Stack으로 들어와 순차적으로 실행

## Axios
* JavaScript의 HTTP 웹 통신을 위한 라이브러리
* 비동기 통신 기능 제공
* node 환경 : npm
* browser 환경 : cdn
* Django REST API로 요청을 보내고 데이터를 받아온 후 처리
* vs Python의 request는 동기 처리
* Axios Docs
* https://axios-http.com/kr/docs/intro
* 요청 Config
* https://axios-http.com/kr/docs/req_config

### Axios 구조
* get, post 등의 method로 요청
* then : 요청에 성공하면 실행할 로직
* catch : 요청에 실패하면 수행할 로직
```javascript
axios({
  url: 'url 주소'
  method: 'get',    // default는 GET
  params: {         // querystringparameter 사용시
    ID: 12345
  },
//   data: {            // PUT, POST, PATCH, DELETE 에서만 사용
//     title: '제목',
//     content: '내용',
//   },
})
  .then()
  .then()
  .catch()
```

### 비동기 처리 단점
* 작업이 완료되는 순서에 따라 처리하기에
* 코드의 실행 순서가 불명확해져 실행 결과를 예측하면서 코드를 작성하기 어려워짐
* 콜백 함수를 사용하여 해결!!

## Callback Function 콜백 함수
* 다른 함수의 인자로 전달되는 함수
* 동기, 비동기 상관없이 사용 가능

### Ashnchronous Callbakc 비동기 콜백
* 시간이 걸리는 비동기 작업 완료 후 실행할 작업을 명시할 목적으로 사용하는 함수
* 비동기 처리를 위해서 콜백 함수의 형태 필요
* **특정한 조건이나 행동에 의해 호출 되도록 작성 가능**
* **비동기 처리를 순차적으로 동작 가능**

### Callback Hell 콜백 지옥
* 비동기 처리를 위한 콜백을 작성할 때 발생하는 문제
* **너무 많은 비동기 작업이 연쇄적으로 들어와서 순서대로 처리할 때 문제 발생**
* 코드의 가독성이 떨어짐
* 유지 보수가 어려움
* 코드의 형태가 피르미드 같아 파멸의 피라미드 라고도 부름
```javascript
work1(function () {
  work2(result1, function (result2) {
    work3(result2, function (result3) {
        ...
    })
  })
})
```

## Promise 프로미스
* 비동기 작업의 완료 또는 실패를 나타내는 객체
* 작업이 끝나면 실행 한다는 약속
* 비동기 처리의 순서 보장
* Callback Hell 문제를 해결하기 위해 사용
* Axios 라이브러리 : Promise 기반의 클라이언트
* .then(callback)
  * 요청한 작업이 성공하면 callback 실행
  * 이전 작업의 성공 결과를 인자로 전달
* .catch(callback)
  * then()이 하나라도 실패하면 callback 실행
  * 이전 작업의 실패 객체를 인자로 전달
* axios로 처리한 비동기 로직이 항상 promise 객체를 반환
* 따라서 **<u>chaining</u>** 가능
  * 한 작업을 쪼개서 작은 여러 기능으로 chaining하게 작성 가능
  * 실행 중간에 디버깅 필요하다면 catch 작성
```javascript
work1()
  .then((result1) => {
    return result2
  })
  .then((result2) => {
    return result3
  })
  .catch((error) => {
    return error1
  })
```