---
title: "SOLID"
date: 2021-11-17 12:00:00 +0900
categories: java
comments: true
---

## SOLID 원칙이란?
 - 객체지향의 대표 원칙
 - S 단일 책임 원칙
 - O 개방-폐쇄 원칙
 - L 리스코프 치환 원칙
 - I 의존 역전 원칙
 - D 인터페이스 분리 원칙


**SRP(Single Responsibility) 단일 책임 원칙**
 - 모든 클래스는 하나의 책임만 가지며, 클래스는 그 책임을 완전히 [캡슐화](../java-oop/)해야 함을 일컫는다.
 - [단일책임원칙](https://ko.wikipedia.org/wiki/%EB%8B%A8%EC%9D%BC_%EC%B1%85%EC%9E%84_%EC%9B%90%EC%B9%99)

**OCP(Open-Closed) 개방-폐쇄 원칙**
 - 확장에 대해서는 열려있어야 하며, 수정에 대해서는 닫혀있어야 한다.
 - 하나의 모듈을 수정할 때, 그 모듈을 사용하는 모든 모듈을 줄줄이 수정해야한다면 유지보수에 어려움이 있으므로 이러한 수정을 유발하지 않도록 구조를 올바르게 리팩토링 해야한다.
 - [개방-폐쇄 원칙](https://ko.wikipedia.org/wiki/%EA%B0%9C%EB%B0%A9-%ED%8F%90%EC%87%84_%EC%9B%90%EC%B9%99)

**LSP(Liskov Substitution) 리스코프 치환 원칙**

**DIP(Dependency Inversion) 의존 역전 원칙**
 
**ISP(Interface Segregation) 인터페이스 분리 원칙**
