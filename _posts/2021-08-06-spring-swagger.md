---
title: "Spring boot + Swagger 적용하기"
date: 2021-08-06 12:00:00 +0900
categories: spring
comments: true
---

## Swagger
  개발자가 REST API 서비스를 설계, 빌드, 문서화할 수 있도록 하는 프로젝트
 - Controller에 명시된 어노테이션을 해석하여 API문서를 자동으로 만들어준다.
 - [접근 방법] 서버주소/swagger-ui.html

#### pom.xml에 dependency 추가하기

```xml
    <dependency>
        <groupId>io.springfox</groupId>
        <artifactId>springfox-swagger-ui</artifactId>
        <version>2.9.2</version>
    </dependency>

    <dependency>
        <groupId>io.springfox</groupId>
        <artifactId>springfox-swagger2</artifactId>
        <version>2.9.2</version>
    </dependency>
```

#### Config 파일 추가
* .apis(RequestHandlerSelectors.basePackage("com.test.controller")) 와 같이 특정 패키지 하위의 모든 URL 리스트를 추출
* .paths(PathSelectors.ant("/v1/api/**")) 와 같이 특정 url패턴만 필터링하여 API문서 생성

```java  
    @Configuration
    @EnableSwagger2
    public class SwaggerConfiguration {

        private ApiInfo apiInfo() {
            return new ApiInfoBuilder()
                    .title("문서제목")
                    .build();
        }

        @Bean
        public Docket api() {
            return new Docket(DocumentationType.SWAGGER_2)
                    .apiInfo(this.apiInfo())
                    .select()
                    .apis(RequestHandlerSelectors.any())
                    .paths(PathSelectors.ant("/v1/api/**"))
                    .build();
        }
    }
```