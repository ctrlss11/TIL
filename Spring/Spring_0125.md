# Swagger 사용법 정리
## 230125 Swagger
### 목표
* swagger 사용방법 정리
* annotation 정리

## 개발환경
* Spring Boot
* gradle
* java 11
* swagger 3.0.0

## dependency 추가

```groovy
dependencies {
	implementation 'io.springfox:springfox-boot-starter:3.0.0'
	implementation 'io.springfox:springfox-swagger-ui:3.0.0'
}
```

## SwaggerConfig 추가

```java
@EnableSwagger2
public class swaggerConfig {

    @Bean
    public Docket api() {
        return new Docket(DocumentationType.OAS_30)
                .useDefaultResponseMessages(false)
                .select()
                .apis(RequestHandlerSelectors.basePackage("packageName"))
                .paths(PathSelectors.any())
                .build()
                .apiInfo(apiInfo());
    }

    private ApiInfo apiInfo() {
        return new ApiInfoBuilder()
                .title("API_NAME")
                .description("API_DESCRIPTION")
                .version("API_VERSION")
                .build();
    }

}
```

### .apis(RequestHandlerSelectors.basePackage("packageName"))
* Swagger를 적용할 클래스의 package명

### .paths(PathSelectors.any())
* 해당 package 하위의 모둔 url에 적용
* 특정 패턴의 url에만 적용하려면 작성

### .useDefaultResponseMessages()
* default response message 사용 안하려면 false

### ApiInfo apiInfo()
* 작성한 API의 제목, 버전, 설명 작성

## Swagger 기능
### @ApiOperation
* API 설명

```java
    @ApiOperation(
            value = "기프티콘 저장",
            notes = "기프티콘 상세 정보 저장 API",
            httpMethod = "POST")
```

### @ApilmplicitParam
* Request Parameter 설명
* 복수인 경우 @ApiImplicitParams 사용

```java
    @ApiImplicitParams({
        @ApiImplicitParam(
            name = "email",
            value = "계정 이메일",
            required = true,
            dataType = "string",
            paramType = "path",
            defaultValue = "None"),

        @ApiImplicitParam(
            name = "social",
            value = "소셜로그인 구분",
            required = true,
            dataType = "string",
            paramType = "path",
            defaultValue = "None"),
    })
```

* paramType
  * @RequestParam 이면 query
  * @PathVariable 이면 path

### @ApiResponse
* Response 설명
* 복수인 경우 @ApiResponses 사용

```java
    @ApiResponses({
        @ApiResponse(code = 200, message = "성공입니다."),
        @ApiResponse(code = 400, message = "접근이 올바르지 않습니다.")
    })
```

### @ApiParam
* DTO field 설명

```java
    @ApiParam(value = "바코드 넘버", required = true)
```

### @ApiModelProperty
* DTO field 예제 추가 및 설명

```java
    @ApiModelProperty(
        name = "barcode_num",
        value = "바코드 넘버",
        example = "1234-5678-9999"
    )
```

### @ApiIgnore
* Swagger UI 상 무시
* @ApiIgnore를 사용해서 @ApiImplicitParam으로 선언하지 않은 parameter 정보 무시 가능
```java
    public String getNotice(@ApiIgnore UserDTO userDTO) {
        return "notice";
    }
```
* return type 앞에 사용하여 특정 api만 무시 가능
```java
    public @ApiIgnore String getNotice(UserDTO userDTO) {
        return "notice";
    }
```