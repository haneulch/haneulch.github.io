---
title: "Mockito를 이용한 테스트"
date: 2022-01-06 12:00:00 +0900
categories: spring
comments: true
---

 **단위 Test**
 **<br>테스트를 진행할 때 SpringBootTest로 진행시 모든 Bean을 로드하기 때문에 시간이 오래 걸리고 무겁다.**
 **<br>Mockito를 이용하여 각자 객체를 생성해서 단위 테스트를 진행한다.**

```java
@ExtendWith(MockitoExtension.class)
public class ControllerTest {
  ...  
}
```

1. @Mock을 통해 Controller에 필요한 bean을 생성한다.
   1. @InjectMocks를 사용시 @Mock으로 사용한 bean들이 주입된다.
   2. @Mock 어노테이션이 붙은 서비스는 실제로 로직이 수행되지 않아 해당 서비스의 메소드를 실행했을때 리턴값을 직접 지정해줘야한다.

```java
@ExtendWith(MockitoExtension.class)
public class ControllerTest {
  @Mock
  TestService testService;
 
  @Mock
  UserService userService;
 
  @InjectMocks
  TestController testController;
}
```

2. MVC 테스트를 위한 세팅

```java
@ExtendWith(MockitoExtension.class)
public class ControllerTest {
  private MockMvc mockMvc;
  private ObjectMapper objectMapper;
  private MediaType mediaType;
  
  @Mock
  private TestService testService;
 
  @Mock
  private UserService userService;
 
  @InjectMocks
  private TestController testController;
  
  @BeforeEach
  void setUp() {
    this.mockMvc = standaloneSetup(testController).build();
    this.objectMapper = new ObjectMapper();
    this.mediaType = new MediaType(MediaType.APPLICATION_JSON.getType(),
      MediaType.APPLICATION_JSON.getSubType(),
      StandardCharsets.UTF_8);
  }
}
```

3. 테스트 코드 작성
   1. 단위 테스트1의 경우 Service로 요청이 없음
   2. 단위 테스트2의 경우 Service로 요청을 하고 응답을 리턴받아야 하나 Test상의 TestService는 Mock 객체로 실제 로직을 수행할 수 없다. 그래서 Mockito를 이용하여 
      TestService를 호출했을때 어떤 응답을 리턴할지를 지정해준다.
      1. 만약 TestService의 메소드가 void라면 doReturn이 아닌 doNothing을 사용한다.

```java
@ExtendWith(MockitoExtension.class)
public class ControllerTest {
 ...
 
 @Test
 @DisplayName("단위 테스트1")
 void test() throws Exception {
   TestRequest testRequest = new TestRequest("test");
   
   mockMvc.perform(
     post("/test")
       .contentType(mediaType)
       .content(mapper.writeValueAsString(testRequest)))
     .andExpect(status().isOK())
     .andDo(print());
  }

 @Test
 @DisplayName("단위 테스트2")
 void test() throws Exception {
  TestRequest testRequest = new TestRequest("test");
  TestDTO testDTO = new TestDTO("test", "1");
  
  doReturn(testDTO).when(testService).findByName(anyString());

  mockMvc.perform(
    post("/testService")
      .contentType(mediaType)
      .content(mapper.writeValueAsString(testRequest)))
  .andExpect(status().isOK())
  .andDo(print());
 }
}

@RestController
@RequiredArgsConstructor
public class TestController {
  private final TestService testService;
  
  @PostMapping("/test")
  void test(@RequestBody TestRequest testRequest) {
    System.out.println(testRequest.getName());
  }
  
  @PostMapping("testService")
  void testService(@RequestBody TestRequest testRequest) {
    testService.findByName(testRequest.getName());
  }
}
```
