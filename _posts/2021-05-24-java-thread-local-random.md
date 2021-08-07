---
title: "Java ThreadLocalRandom"
date: 2021-05-24 12:00:00 +0900
categories: java
comments: true
---

## ThreadLocalRandom
#### 난수생성시 사용되는 Random vs ThreadLocalRandom

* java 7버전부터는 Random보다는 ThreadLocalRandom사용을 권장한다.
* Random보다 더 고품질의 무작위 수를 생성하며 성능도 빠르다.
* ints(10, 0, 100)를 사용시 0 - 100 사이의 10개의 랜덤 숫자 생성이 가능하다.

```java
  int intNum = ThreadLocalRandom.current().nextInt(100);
  long longNum = ThreadLocalRandom.current().nextLong();
  ...
  ThreadLocalRandom.current().ints(10, 0, 100).forEach(i -> System.out.println(i));
```

[이펙티브 자바(Effective Java 3/E)](https://book.naver.com/bookdb/book_detail.nhn?bid=14097515)
