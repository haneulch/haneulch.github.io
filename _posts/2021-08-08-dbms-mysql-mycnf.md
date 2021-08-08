---
title: "Mysql my.cnf 설정"
date: 2021-08-08 12:00:00 +0900
categories: dbms
comments: true
---

## Mysql 설정변경
* 활동 중인 커넥션이 닫히기 전까지 서버가 대기하는 시간  
    **interactive_timeout = 10**  

* 활동하지 않는 커넥션을 끊을 때까지 서버가 대기하는 시간    
    **wait_timeout = 10**

* MySQL 서버 접속 시에 접속 실패를 메시지를 보내기까지 대기하는 시간
    **connect_timeout = 10**

* default 문자 셋
    **character-set-server = utf8**

* default 시간대
    **default-time-zone = '+9:00'**

* 메모리 테이블 최대 크기
    **max_heap_table_size = 128M**

* 허용 가능한 최대 동시 접속수/커넥션 당 최소 thread_stack의 사이즈만큼 메모리 사용
    **max_connections = 151**

* thread 당 스택 사이즈(기본 256K)
    **thread_stack = 256K**

* thread 재사용을 위한 수로 cache에 있는 thread수 보다 접속이 많으면 새로운 thread가 생성됨
    **thread_cache_size = 8**

* max_connections 이상의 커넥션이 몰릴 때 대기가능한 커넥션 수
    **back_log = 100**