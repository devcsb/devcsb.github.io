---
title: "String, StringBuffer, StringBuilder의 차이와 장단점"
tags:
  - String
  - StringBuffer
  - StringBuilder

permalink: /til/:year/:month/:day/:title/
toc: true
toc_sticky: true
comments: true
---

# 오늘 한 일

너무 바쁜 하루였다. 그리고 정말 중요한 하루였다. 스트레스 관리와 체력관리의 중요성을 새삼 깨닫게 되었다.
나는 충분히 할 수 있다.

# 오늘 배운 것

## String, StringBuffer, StringBuilder

Java에서 문자열을 다루는 대표적인 클래스로 String, StringBuffer, StringBuilder가 있다.
모두 String을 저장하고 관리하는 클래스들이지만, 연산횟수가 많아지거나, 멀티쓰레드,
Race condition(두 개의 스레드가 하나의 자원을 놓고 서로 사용하려고 경쟁하는 상황)이 자주 발생한다면 각 특징에 알맞는 클래스를 사용해야 할 것이다.

### String

String과 StringBuffer/StringBuilder 클래스의 가장 큰 차이점은 String은 불변의 속성을 갖는다는 점이다.
아래 코드에서, "hello" 값을 가지고 있던 String 클래스의 참조변수 str이 가리키는 곳에 저장된 "hello"에 "world" 문자열을 더해
"hello world"로 변경한 것으로 착각할 수 있다.

```java
String str = "hello"  // String str = new String("hello");
str = str + "world"  // [hello world]
```

하지만 기존에 "hello"값이 들어가있던 str이 "hello world"라는 값을 가지고 있는 새로운 메모리영역을 가리키게 변경되고,
처음 선언했던 "hello"로 값이 할당 되어 있던 메모리 영역은 Garbage로 남아있다가 GC(garbage collection)에 의해 사라지게 된다.
String 클래스는 불변하기 때문에 문자열을 수정하는 시점에 새로운 String 인스턴스가 생성된 것이다.

위와같이 String은 불변성을 가지기 때문에, 문자열 추가, 수정, 삭제등의 연산이 빈번하게 발생하는 알고리즘에는 적합하지 않다.
Heap 메모리에 수많은 Garbage가 연산 과정의 찌꺼기로 남아, 힙메모리 부족으로 성능에 영향을 미칠 수 있기 때문이다.

<br>

이를 해결하기 위해 Java에서는 가변성을 가지는 StringBuffer/ StringBuilder 클래스를 도입했다.
StringBuffer/StringBuilder 는 가변성 가지기 때문에 .append() .delete() 등의 API를 이용하여 동일 객체내에서 문자열을 변경하는 것이 가능하다.

```java
StringBuffer sb= new StringBuffer("hello");
sb.append(" world");
```

### StringBuffer VS StringBuilder

그렇다면 동일한 API를 가지고 있는 StringBuffer와 StringBuilder의 차이는 뭘까?
바로 동기화의 유무이다. StringBuffer는 동기화 키워드를 지원하여 멀티쓰레드 환경에서 안전(thread-safe)하다.
참고로 String은 불변성을 가지기에 당연히 thread-safe하다.

반면에, StringBuilder는 동기화를 지원하지 않기 때문에 멀티쓰레드 환경에서 사용하는 것은 적합하지 않지만
동기화를 고려하지 않는 만큼 단일쓰레드에서의 성능은 StringBuffer보다 뛰어나다.

### 정리

단순히 성능만 놓고 본다면 연산이 많은 경우, StringBuilder > StringBuffer >>> String 순으로 빠르다.

#### 선택 고려사항

String : 문자열 연산이 적고 멀티쓰레드 환경일 경우
StringBuffer : 문자열 연산이 많고 멀티쓰레드 환경일 경우
StringBuilder : 문자열 연산이 많고 단일쓰레드이거나 동기화를 고려하지 않아도 되는 경우

# 내일 할 일

- 자바 학습
- 정보처리기사 실기 공부
