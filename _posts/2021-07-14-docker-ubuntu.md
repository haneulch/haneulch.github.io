---
title: "Docker Ubuntu 설치"
date: 2021-07-14 12:00:00 +0900
categories: docker
comments: true
---

## Docker Ubuntu 설치
 - Docker 설치후 터미널에서 ubuntu 설치 --name 옵션은 이름을 정하는것으로 생략해도 됨
 
```bash
docker run -it --name=ubuntu_server ubuntu
```
 - 실행
 - docker ps 로 현재 실행중인 컨테이너 확인
 - docker ps -a 옵션을 추가하면 전체 컨테이너를 확인
 - 컨테이너가 실행중이 아닌 경우 docker start 명령으로 실행
 - 확인된 컨테이너 아이디로 docker terminal 실행 가능
 - 컨테이너 아이디는 일부만 입력해도 실행됨
 
```bash
docker ps -a
docker start f0ac
docker exec -it f0ac bash
```
