---
title: "php 로컬 개발환경 구성을 위한 docker-compose.yml 작성"
tags:
  - php
  - docker-compose

permalink: /til/:year/:month/:day/:title/
toc: true
toc_sticky: true
comments: true
---

# 오늘 한 일
bitnami php 5.6버전을 설치하는데, 자꾸 아파치 에러가 나서 오류를 파고 들면서 시간을 보냈다.
여러모로 마음에 들지 않았던 bitnami로 구성된 로컬 개발환경을 docker로 변경해야겠다고 마음먹게 된 계기가 되었다.



# 오늘 배운 것
사내 로컬 개발환경은 bitnami WAMP 패키지를 설치하고, 그 위에서 작업하는 방식이었다.
하지만 여러 php버전을 넘나들면서 개발해야 할 때, bitnami를 매번 새로 설치하고 또 그 과정에서 여러가지
버그들이 발생하여 낭비되는 시간이 너무 많은 것이 불만이었다.
그래서 이번에는 로컬 개발환경을 docker를 사용하여 구축하기로 마음 먹었다.

일단 docker-compose.yml을 아래와 같이 작성하였다.
```yml
version: "1"

services:
  mariadb:
    image: mariadb:5.5
    volumes:
      - "./data:/var/lib/mysql:rw" # mysql에 생성되는 데이터를 ./data 폴더에 저장
    env_file:
      - .env
    ports: # docker port 는 3306 localhost port 는 3406 사용 하겠다는 의미
      - "3406:3306"
  web:
    build: # Dockerfile을 통해 이미지 생성
      context: .  # 이미지 생성에서 사용할 기본 경로를 지정
      dockerfile: ./Dockerfile
    volumes:
      - ".:/var/www/html"
    depends_on:
      - db
    ports:
      - "80:80" # 앱의 80 포트를 로컬의 80포트와 연결
    depends_on: # maria 실행 후 실행하게끔 한다.
      - mariadb
```
Dockerfile에 대한 것은 다음에 알아보자.

# 내일 할 일

- 자바 기술면접 준비
- 마음챙김
