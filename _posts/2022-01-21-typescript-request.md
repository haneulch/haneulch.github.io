---
title: "typescript request"
date: 2022-01-21 12:00:00 +0900
categories: typescript
comments: true
---

## typescript Request Param/Query/Body 차이점

### @Param
url parameter를 받아오기 위함

```typescript
@Get('/:id')
getOne(@Param('id') id: string) {
    return id;
}
```
```typescript
@Get('/:id')
getOne(@Req() id: string) {
    return id;
}
```
### @Body == req.body
body 데이터를 받아옴<br>
아래의 예시처럼 @Body 어노테이션을 통해 전달 받거나 req.body를 통해서 받을 수 있습니다.

```typescript
@Post('/user')
createUser(@Body() user: User) {
    return this.userServie.create(user);
}
```
```typescript
@Post('/user')
createUser(@Req() req) {
    return this.userService.create(req.body);
}
```

### @Query == req.query
querystring 데이터를 받아옴<br>
http://localhost/users?id=3과 같이 요청하였을때 쿼리 내용을 받아옵니다.

```typescript
@Get('/user')
getUser(@Query() query) {
    return this.userService.findById(query.id);
}
```
```typescript
@Get()
getUserList(@Req() req) {
    return this.usersService.list(req.query.id);
}
```
