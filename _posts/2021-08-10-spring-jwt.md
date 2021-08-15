---
title: "Spring JWT 적용하기"
date: 2021-08-10 12:00:00 +0900
categories: spring
comments: true
---

## Spring JWT 적용하기
* pom.xml에 dependency 추가

```xml
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt</artifactId>
    <version>0.9.1</version>
</dependency>
```

## token 생성
* setSubject 토큰 제목
* signWith 암호화 방식과 키를 지정
* setExpiration token 유효기간 지정

```java
public String createAccessToken(String username) {
    
    Calendar cale = Calendar.getInstance();
    cale.add(Calendar.SECOND, EXPIRE_SECONDS);
    
    return Jwts
            .builder()
            .setSubject(username)
            .signWith(SignatureAlgorithm.HS256, SECRET)
            .setExpiration(cale.getTime())
            .compact();
}
```