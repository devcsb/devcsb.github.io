---
title: "[Spring]DI, IOC"
tags:
  - Spring
  - DI(Dependency Injection)
  - IOC(Inversion of Control)

permalink: /til/:year/:month/:day/:title/
toc: true
toc_sticky: true
comments: true
---

# 오늘 한 일
커리어에 대해 많은 고민을 하며 하루를 보냈다. 지난 작년, 그리고 올해의 절반이 지나는 이 시점까지
내가 할 수 있는 만큼의 최선을 다하며 지냈다고 생각하는데, 여전히 아쉬웠던 부분이나 부족한 점들이 많다.
조금만 더 현명하게 시간을 썼더라면... 조금만 더 신중하게 판단했었더라면 더 좋은 상황에 있지 않았을까 하는 생각이 든다.
무너지지말고 조금 더 독하게 마음을 먹자.

# 오늘 배운 것

## DI 와 IOC
### DI(Dependency Injection)
Dependency Injection 이란, 말 그대로 의존성 주입이다. 주입이란, 외부에서 안으로 넣어준다는 뜻이다.
즉, 외부에서 두 객체 간의 의존관계를 결정해주는 디자인 패턴을 말한다. 클래스간의 결합이 아니라, 중간에 인터페이스를 둬서 런타임 시에 관계를 동적으로 주입해주는 기법이다.

### 의존성 주입(DI)이 필요한 이유
예를 들어 연필이라는 상품과 1개의 연필을 판매하는 Store 클래스가 있다고 하자.
```java
public class Store {

    private Pencil pencil;

    public Store() {
        this.pencil = new Pencil();
    }
}
```

위의 예시에서는 크게 두 가지 문제점을 가지고 있다.
* 두 클래스가 강하게 결합되어 있음
* 객체들 간의 관계가 아니라 클래스 간의 관계가 맺어짐

1. 두 클래스가 강하게 결합되어 있음
* 만약 Store에서 Pencil이 아닌 Food를 판매하고자 한다면 Store 클래스의 생성자에 변경이 필요하다. 즉, 유연성이 떨어진다. 이를 해결하기 위해 상속을 떠올릴 수 있지만, 상속은 제약이 많고 확장성이 떨어지므로 피하는 것이 좋다.

<br>

2. 객체들 간의 관계가 아니라 클래스 간의 관계가 맺어짐
* 위의 Store와 Pencil는 객체들 간의 관계가 아니라 클래스들 간의 관계가 맺어져 있다는 문제가 있다. 올바른 객체지향적 설계라면 객체들 간에 관계가 맺어져야 한다. 객체들 간에 관계가 맺어졌다면 다른 객체의 구체 클래스(Pencil인지 Food 인지 등)를 전혀 알지 못하더라도, (해당 클래스가 인터페이스를 구현했다면) 인터페이스의 타입(Product)으로 사용할 수 있다.

<br>
위와 같은 문제점이 발생하는 근본적인 이유는 Store에서 불필요하게 어떤 제품을 판매할 지까지 알고 있기 때문이다. 즉, 관심사가 분리되지 않았기 때문이다.
Spring에서는 DI를 적용하여 이러한 문제를 해결하고자 했다.


###의존성 주입을 통한 문제 해결
위와 같은 문제를 해결하기 위해서는 다형성을 활용해야 한다. Pencil과 Food등 여러가지 제품을 하나로 묶는 공통된 속성을 정의한 Product 라는 인터페이스가 필요하다.
```java
public interface Product {}

public class Pencil implements Product {}
```
<br>

이제 Store와 Pencil이 강하게 결합되어 있는 부분을 제거해주어야 한다.
이를 제거하기 위해서는 아래와 같이 외부에서 상품을 주입(Injection)받아야 한다.
그래야 Store에서 구체 클래스에 의존하기 않기 때문이다.
```java
public class Store {

    private Product product;

    public Store(Product product) {
        this.product = product;
    }
}
```
여기서 Spring이 DI 컨테이너를 필요로 하는 이유를 알 수 있는데, 우선 Store에서 Product 객체를 주입하기 위해서는 애플리케이션 실행 시점에 필요한 객체(빈)를 생성해야 하며, 의존성이 있는 두 객체를 연결하기 위해 한 객체를 다른 객체로 주입시켜야 하기 때문이다.
예를 들어 다음과 같이 Pencil 이라는 객체를 만들고, 그 객체를 Store로 주입시켜주는 역할을 위해 DI 컨테이너가 필요하게 된 것이다.

```java
public class BeanFactory {

    public void store() {
        // Bean의 생성
        Product pencil = new Pencil();
    
        // 의존성 주입
        Store store = new Store(pencil);
    }
}
```
그리고 이러한 개념은 제어의 역전(Inversion of Control, IoC)라고 불리기도 한다. 어떠한 객체를 사용할지에 대한 책임은 프레임워크에게 넘어갔고, 자신은 수동적으로 주입받는 객체를 사용하기 때문이다.


### 의존성주입(Dependency Injection, DI) 정리
한 객체가 어떤 객체(구체 클래스)에 의존할 것인지는 별도의 관심사이다.
Spring은 의존성 주입을 도와주는 DI 컨테이너로써, 강하게 결합된 클래스들을 분리하고, 애플리케이션 실행 시점에 
객체 간의 관계를 결정해 줌으로써 결합도를 낮추고 유연성을 확보해준다. 
이러한 방법은 상속보다 훨씬 유연하다. 단, 한 객체가 다른 객체를 주입받으려면 
반드시 DI 컨테이너에 의해 관리되어야 한다는 것이다.

### DI의 장점
* 두 객체 간의 관계라는 관심사의 분리
* 두 객체 간의 결합도를 낮춤
* 객체의 유연성을 높임
* 테스트 작성을 용이하게 함

참고 : https://mangkyu.tistory.com/150

# 내일 할 일
- 자바 학습
- 정보처리기사 실기 공부
