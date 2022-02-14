---
title: "Nest.js Module 이란"
date: 2022-02-14 12:00:00 +0900
categories: typescript
comments: true
---

## Nest.js Module
여러 컴포넌트를 조합하여 좀 더 큰 작업을 수행하는 단위
 - MSA 관점에서 모듈이 커지면 하나의 Micro Service로 분리할 수 있음
 - 모듈은 Provider처럼 주입해서 사용하는게 불가능함(모듈간 순환 종속성 발생)
 - Nest의 모듈은 기본적으로는 Singleton객체이다.
 - @Global() 데코레이터를 선언하면 전역모듈로 사용이 가능
   - 전역모듈은 Root모듈이나 Core모듈에서 한번만 등록해야한다.
   - 전역모듈은 어디에나 존재하기 때문에 필수 기능만 전역으로 선언해야함
   
#### * 아래와 같이 전역모듈로 선언된 경우 다른 모듈해서 해당 모듈을 사용하고자 할때 imports에서 선언하지 않아도 된다.
```typescript
@Module({
   imports: [
       ConfigModule.forRoot({
          isGlobal: true,
       }), ...
   ]...
})...
```

### Imports
해당 모듈에서 사용하기 위한 Provider를 가지고 있는 다른 모듈을 가져옵니다.

### Controllers
요청과 응답을 처리하고 가공
 - 들어오는 요청을 받고 처리된 결과를 응답으로 돌려주는 인터페이스 역할

### Providers
비즈니스 로직을 수행
 - 단일책임원칙
 - Service, Repository, Factory, Helper 등 여러가지 형태로 구현

### Exports
해당 모듈에서 제공하는 컴포넌트를 다른 모듈에서 import에 사용하려면 export해야한다.
 - export로 선언하면 어디에서나 가져다 쓸 수 있으므로 public 인터페이스 또는 API로 간주

