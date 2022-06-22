---
title: "Github Action 사용하기"
tags:
  - Github Action

permalink: /til/:year/:month/:day/:title/
toc: true
toc_sticky: true
comments: true
---

# 오늘 한 일
회사 일이 갈수록 막장으로 치닫고 있다. 영업 선에서 일정관리가 전혀 되지 않는 문제, 
비용절감을 이유로 신규인력 충원없이 사람을 갈아넣는 문제로부터 또 다른 문제들이 계속 파생되고 있다.
정신적으로 너무 힘들다. 일이 손에 잡히질 않는다. 숨 돌릴 시간도 없다.
마음을 다 잡고 내가 할 일과 공부, 이직 준비에 힘을 쓰자.

# 오늘 배운 것

## Github Action

Github Action은 github에서 공식적으로 제공하는 workflow 자동화 툴이다.

공식문서를 보면 가장 자세히 github action에 대해 알 수 있다.
https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions

Github Action을 사용하기 위해서는 먼저, 프로젝트 디렉토리에서 .github/workflows 디렉토리를 생성하고, 거기에 .yml파일을 만들어서 스크립트를 작성하면 된다.

아래는 내가 springboot를 github action으로 ci를 수행하기 위해 작성한 workflow다.
```yml
name: first-springboot2

on:
  push:
    branches:
      - master # (1) Github Action의 트리거 브랜치를 지정
  workflow_dispatch: # (2) 브랜치 push 이벤트외에, 수동으로 실행하는 것도 가능하게 만드는 옵션

jobs:
  build:
    runs-on: ubuntu-latest # (3) 해당 Github Action 스크립트가 작동될 OS 환경을 지정합니다.

    steps:
      - name: Checkout
        uses: actions/checkout@v2 # (4) 프로젝트 코드를 checkout 합니다.

      - name: Set up JDK 11
        uses: actions/setup-java@v1 # (5) Github Action이 실행될 OS에 Java를 설치합니다.
        with:
          java-version: 11

      - name: Grant execute permission for gradlew
        run: chmod +x ./gradlew # (6) gradle wrapper를 실행할 수 있도록 실행 권한 (+x)을 줍니다.
        shell: bash

      - name: Build with Gradle
        run: ./gradlew clean build # (7) gradle wrapper를 통해 해당 프로젝트를 build 합니다.
        shell: bash

      - name: Get current time
        uses: 1466587594/get-current-time@v2
        id: current-time
        with:
          format: YYYY-MM-DDTHH-mm-ss # (1)
          utcOffset: "+09:00" # 해당 action의 기준이 UTC이기 때문에 한국시간이 KST를 맞추기 위해서는 +9시간이 필요하여 offset을 추가

      - name: Show Current Time # get-current-time 에서 지정한 포맷대로 현재 시간을 노출
        run: echo "CurrentTime=${{steps.current-time.outputs.formattedTime}}" # (2)
        shell: bash

```

# 내일 할 일

- 자바 학습
- 정보처리기사 실기 공부
