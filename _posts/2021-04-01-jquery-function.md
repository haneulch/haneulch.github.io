---
title: "Jquery Function"
date: 2021-04-20 12:00:00 +0900
categories: jquery
comments: true
---


[참조 : Jquery Api Documentation](https://api.jquery.com/)

## 자주 사용하는 Jquery Function

### eq
* index에 해당하는 element
* .eq와 :eq는 동일한 기능을 하며 name이 test인 element중 index가 0인 element

```javascript
$('[name=test]').eq(0);
$('[name=test]:eq(0)');
```

### parent
* element의 부모 element를 찾는다.

#### parent()
* $('#test')의 바로 상위의 element를 찾는다

```javascript
$('#test').parent();
```

#### parents(selector)
* $('#test')의 상위의 element들중 가장 가까운 tr element를 찾는다.

```javascript
$('#test').parents('tr');
```