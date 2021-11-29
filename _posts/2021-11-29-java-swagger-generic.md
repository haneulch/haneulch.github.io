---
title: "Swagger ApiResponse에 Generic type 사용하기"
date: 2021-11-29 12:00:00 +0900
categories: java
comments: true
---

 **예시 코드는 단순 참고용입니다.**
 
 **swagger 사용시 공통된 response 객체를 implementation에 선언할 경우 그 상세 내용이 예시에서 단순 object로 표현이 된다. 
object가 아닌 그 클래스의 내용을 전부 보여주고 싶다면 wrapper클래스를 사용하면 된다.**

 1. 공통 response 객체를 생성해서 코드와 함께 응답 데이터를 보내려고 구성

```java
    public class CommonResponse<T> {
        private String code;
        private String message;
        private T data;
    }
```

 2. Controller에서 Swagger를 사용해 response 양식을 보여주기 위한 설정
  - @ApiResponse의 implementation에 리턴될 클래스를 명시

```java
    public TestController {
        @Operation(
            summary = "test 예시", 
            description = "예시 데이터 입니다.",
            responses = {
                @ApiResponse(
                    responseCode = "200", 
                    description = "", 
                    content = @Content(schema = @Schema(implementation = CommonResponse.class))
                )
            }
        )
        public ResponseEntity<CommonResponse<Test>> test() {
            Test test = new Test();
            CommonResponse<Test> response = new CommonResponse<Test> ("SUCCESS", "성공", test);
            return new ResponseEntity<CommonResponse<Test>>(response, HttpStatus.OK);
        }
    }

    class Test {
        String data1;
        String data2;
    }
```

 3. 위와 같이 선언시 Response 데이터 예시에는 data가 단순 'object' 로만 보여 상세 내용을 알 수 없다.

 ```json
    {
        "code" : string,
        "message" : string,
        "data" : object
    }
 ```

  4. Wrapper 클래스 생성

```java
    public class TestWrapper extends CommonResponse<Test> {}
```

```java
    public TestController {
        @Operation(
            summary = "test 예시", 
            description = "예시 데이터 입니다.",
            responses = {
                @ApiResponse(
                    responseCode = "200", 
                    description = "", 
                    content = @Content(schema = @Schema(implementation = TestWrapper.class))
                )
            }
        )
        public ResponseEntity<CommonResponse<Test>> test() {
            Test test = new Test();
            CommonResponse<Test> response = new CommonResponse<Test> ("SUCCESS", "성공", test);
            return new ResponseEntity<CommonResponse<Test>>(response, HttpStatus.OK);
        }
    }

    class Test {
        String data1;
        String data2;
    }
```

 5. 위와 같이 Wrapper 클래스를 생성해 implementation에 선언시 아래와 같이 data 상세내용을 알 수 있으나, 불필요한 wrapper클래스가 많이 생성되는게 단점이 아닐까 싶다..

 ```json
    {
        "code" : string,
        "message" : string,
        "data" : {
            "data1" : string,
            "data2" : string
        }
    }
 ```


