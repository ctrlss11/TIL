# REST API 설계 / 네이밍 방법
## 230124 Spring
### 목표
* REST API 설계 개념 공부
* url 네이밍 규칙 권장사항 정리

## REST 란?
* Representational State Transfer
* 자원, 행위, 표현으로 구성
* Resource 자원 : URI
* Verb 행위 : HTTP Method
* Representations 표현

URI를 통해 자원(Resource)를 표시하고, HTTP Method를 기반으로 해당 자원의 행위를 규정하여 결과를 받는 것

---

## Resource 표현 방식
* document, collection, store, controller 으로 구분 가능

### document
* 1개의 객채 인스턴스를 나타냄
* collection 중의 하나로 표현
* / 를 통해 구분

```
http://api.example.com/device-management/managed-devices/{device-id}
http://api.example.com/user-management/users/{id}
http://api.example.com/user-management/users/admin
```

### collection
* 단일 resource(== document)들의 묶음
* 복수형 단어 사용

```
http://api.example.com/device-management/managed-devices
http://api.example.com/user-management/users
http://api.example.com/user-management/users/{id}/accounts
```

### store
* 처음 resource를 등록할 때 client가 전달한 key 사용
* 복수형 단어 사용

```
http://api.example.com/cart-management/users/{id}/carts
http://api.example.com/song-management/users/{id}/playlists
```

### controller
* 서버의 실행 가능한 function
* resource를 조작하는 것이 아닌 직접 function을 실행하는 행위를 나타냄
* 동사 사용 가능

```
http://api.example.com/cart-management/users/{id}/cart/checkout
http://api.example.com/song-management/users/{id}/playlist/play
```

---

## REST API 설계
### 1. 동사가 아닌 명사로 resource 표현
* 명사를 사용하여 resource의 속성 표현 가능

```
http://api.example.com/device-management/managed-devices
http://api.example.com/device-management/managed-devices/{device-id}
http://api.example.com/user-management/users/
http://api.example.com/user-management/users/{id}
```

### 2. 소문자 사용
* 주소에서 대소문자를 구분하기 때문에
* camelCase가 아닌 소문자로 사용

```
// Bad
http://restapi.example.com/users/postComments

// Good
http://restapi.example.com/users/post-comments
```

### 3. 언더바 _ 대신 하이픈 - 사용
* <u>**가급적 하이픈의 사용도 최소화**</u>
* 정확한 의미나 표현을 위해 불가피한 경우에만 사용

```
// Bad
http://restapi.example.com/users/post_comments

// Good
http://restapi.example.com/users/post-comments
```

### 4. URI 마지막에 / 사용 x
* / 를 통하여 계층을 구분
* 마지막에는 사용 x

### 5. 행위는 URI에 포함 x
* 행위는 HTTP Method를 사용하여 전달

```
// Bad
POST http://restapi.example.com/users/1/delete-post/1

// Good
DELETE http://restapi.example.com/users/1/posts/1
```

### 6. 파일 확장자는 URI에 포함 x
* request body 내용의 포멧은 accept header를 사용하여 나타내기

```
// Bad
http://restapi.example.com/users/photo.jpg

// Good
GET http://restapi.example.com/users/photo
HTTP/1.1 Host: restapi.example.com Accept: image/jpg
```

### 7. 가급적 자원의 명사를 사용, 컨트롤 자원을 의미하는 경우 예외적으로 동사 사용

```
// Bad
http://restapi.example.com/posts/duplicating

// Good
http://restapi.example.com/posts/duplicate
```

## 카카오 API 예시
https://developers.kakao.com/docs/latest/ko/reference/rest-api-reference