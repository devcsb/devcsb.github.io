---
title: "gitbub action의 구성도"
tags:
  - github action

permalink: /til/:year/:month/:day/:title/
toc: true
toc_sticky: true
comments: true
---

# 오늘 한 일
새벽에 잠을 거의 못 자서 너무 피곤했다. 비행기를 두 번이나 타고 정말 바쁜 하루였다.
하지만 아주 의미있는 하루였다.
알을 깨고 한 층 더 성숙해지려는 시도, 그 첫걸음을 성공적으로 내딛은 날이다.     ㄴ                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        

# 오늘 배운 것
## github action이란?
GitHub Actions은 빌드, 테스트 및 배포 파이프라인을 자동화할 수 있는 CI/CD 플랫폼이다.
github action은 단순히 CI/CD 파이프라인을 구축할 때 뿐만 아니라,
repository에서 다른 이벤트가 발생할 때 workflow를 실행할 수 있도록 한다.
가령 누군가 저장소에 새로운 이슈를 생성할 때마다 적절한 레이블을 붙인다던지,
머지 리퀘스트를 올릴 때 마다 테스트를 수행한다든지 하는 작업을 자동화 할 수 있다.

## workflows
workflow는 하나 이상의 job으로 구성되고 event에 의해 트리거될 수 있는 자동화된 프로세스이다.
가장 최상위 개념으로 YAML으로 작성되고 Github Repository의 .github/workflows 폴더 아래에 저장한다.
repository에는 여러 workflow를 가질 수 있으며 각 workflow는 서로 다른 작업을 수행할 수 있다.

## events
event는 workflow 실행을 트리거하는 특정 활동이나 규칙이다. 예를 들어,
누군가가 pull request를 생성하거나 issue를 열거나 특정 브랜치로 push하거나
특정 시간대에 반복(cron)하거나 webhook을 사용해 외부 이벤트를 통해 실행될 수 있다.

## jobs
jobs은 여러 step으로 구성되고 가상 환경의 인스턴스에서 실행됩니다. 다른 job에 의존 관계를 가질 수 있고
독립적으로 병렬 실행도 가능하다.
- Workflow는 다양한 Job으로 구성되는데 기본적으로 병렬로 실행

## steps
step은 task들의 집합으로 커맨드를 날리거나 쉘 스크립트 실행하는 것처럼 action을 실행할 수 있다.

## actions
workflow의 가장 작은 블럭으로 job을 만들기 위해 step들을 연결할 수 있다. 
재사용이 가능한 컴포넌트로서 반복적인 코드의 양을 줄일 수 있고 git repository를 가져오거나 
클라우드 공급자에게 인증을 설정할 수도 있다. 또한 개인적으로 만든 action을 작성할 수도 있고 
github marketplace에 있는 공용 action을 사용할 수도 있다.

## runners
runner는 workflow가 트리거될 때 실행하는 서버이다. 
각 runner는 1번에 1개의 job을 실행할 수 있다. 
Github에서 호스팅해주는 Github-hosted runner와 직접 호스팅하는 Self-hosted runner로 나뉜다. 
Github-hosted runner는 Azure의 Standard_DS2_v2로 vCPU 2, 메모리 7GB, 임시 스토리지 14GB이다.


참고: https://docs.github.com/en/actions
https://brownbears.tistory.com/597
https://zzsza.github.io/development/2020/06/06/github-action/
https://meetup.toast.com/posts/286


# 내일 할 일
- 주거지 마련 방법 탐색
- 자바 학습
