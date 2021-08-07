---
title: "Java Optional"
date: 2021-05-14 12:00:00 +0900
categories: java
comments: true
---

## Optional
* Wrapper Class
* Null값으로 인해 발생하는 Exception 예외 처리 가능

### orElse

```java
public static void main(String[] args) {
    Optional<String> test1 = Optional.of("test1");
    optionalValuePrint(test1);
    // -> test

    Optional<String> test2 = Optional.empty();
    optionalValuePrint(test2);
    // -> defaultValue
}

private static void optionalValuePrint(Optional<String> test) {
		System.out.println(test.orElse("defaultValue"));
}
 ```
