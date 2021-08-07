---
title: "문자열 연결시에는 StringBuilder를 사용하자"
date: 2021-05-21 12:00:00 +0900
categories: java
comments: true
---

### 연산자를 이용해서 String을 연결하는 것보다 StringBuilder를 사용하는게 훨씬 빠르다.
 - 연산자를 이용해 String을 연결한 test1과 StringBuilder를 이용한 test2의 소요시간을 비교하면 test2가 test1에 비해 100배나 빠르다
 - test1은 0.223568초
 - test2는 0.002552초

``` java
	private static void test1() {
		long startTime = System.nanoTime();
		
		String result = "";
		
		for(int i = 0; i < 10000; i ++) {
			result += i + ":";
		}
		
		long endTime = System.nanoTime();
		
		System.out.println(String.format("test1 소요시간 : %f", (double)(endTime - startTime)/1000000000));
	}
	
	private static void test2() {
		long startTime = System.nanoTime();
		
		StringBuilder sb = new StringBuilder();
		
		for(int i = 0; i < 10000; i ++) {
			sb.append(i + ":");
		}
		
		long endTime = System.nanoTime();
		
		System.out.println(String.format("test2 소요시간 : %f", (double)(endTime - startTime)/1000000000));
	}
```
