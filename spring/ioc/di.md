# 스프링의 의존성 주입(DI)

## 의존성 주입(DI, Dependency Injection)이란?
* 의존성(dependency)이란 하나의 객체 A가 다른 객체 B 없이 제대로 된 역할을 할 수 없는 관계를 말한다.
* 이때 객체 A가 객체 B에 의존적이다 라고 표현한다.
* 주입(injection)이란 객체 A가 객체 B를 만들어 사용하는 방식과는 달리, 객체 A가 객체 B를 필요로 한다는 신호를 보내면 제3의 존재(Injector)가 객체 B를 객체 A에 전달해주는 것을 의미한다.
* 따라서 의존성 주입이란, 객체 A가 의존성을 가질 객체 B를 필요로 하는 상황에서 제3의 존재가 객체 B를 찾아 객체 A에 전달해주는 것을 의미한다.
* 여기서 객체 A는 클라이언트를 의미하고, 객체 B는 서비스가 된다.

<img src="https://blog.kakaocdn.net/dn/vUNOi/btqANDRfQM4/rMZxO7DmxWwlj7lhj1lR51/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FvUNOi%2FbtqANDRfQM4%2FrMZxO7DmxWwlj7lhj1lR51%2Fimg.png" data-filename="di.png" data-origin-width="829" data-origin-height="352" width="578" height="245" data-ke-mobilestyle="widthContent">
 
## 의존성 주입이 왜 필요한가?
* 서비스를 사용하는 클라이언트의 입장에서는 서비스가 어떻게 생성되는지 알 필요가 없기 때문에 서비스를 생성하여 제공하는 책임을 외부(제 3의 존재, Injector)에 위임할 수 있다.
* 따라서 의존성 주입은 제어 역전(IoC, Inversion of Control)의 확장된 기법이라고 할 수 있는데, 이러한 책임 전가를 통해 오브젝트의 생성과 사용에 대한 관심사항의 분리(SoC, Seperation of Concerns)를 이루어낸다.
* 간단하게 말하자면 클라이언트가 서비스를 생성하는 방식에서 클라이언트가 생성된 서비스를 주입받는 의존성 주입으로의 전환을 통해 관심사항의 분리가 이루어지는 것이다.
* 그리고 이러한 관심사항의 분리는 코드의 가독성과 재사용성을 향상시킨다.
 
## 스프링에서 의존성 주입은 어떻게 이루어지는가?
* 스프링은 의존성 주입 기법을 사용하기에 적합한 구조로 설계되어있다.
* 스프링에서는 `ApplicationContext`라는 존재가 필요한 객체들을 생성하고, 필요한 객체들을 주입하는 역할을 한다.
* 따라서 스프링을 사용하는 개발자들은 객체와 객체를 분리하여 생성하고, 이러한 객체들을 엮는(wiring) 작업을 하는 형태로 개발을 하게 된다.
* 스프링에서 `ApplicationContext`가 관리하는 객체는 Bean이라고 부른다.
* Bean을 엮는 작업은 XML 설정, 어노테이션 설정, 그리고 Java 설정을 이용할 수 있다.
 

## 스프링이 동작하면서 생기는 일
* 스프링 프레임워크가 시작되면 먼저 스프링이 사용하는 메모리 영역을 만들게 되는데, 이를 컨텍스트(context)라고 한다. 스프링에서는 `ApplicationContext`라는 이름의 객체가 만들어진다.
* 스프링은 자신이 객체를 생성하고 관리해야 하는 객체들에 대한 설정이 필요하다. XML 설정을 사용할 때 이에 대한 설정이 `root-context.xml` 파일이다.
* root context는 웹 애플리케이션이 로드해서 사용하는 최상위 context이다. 하지만 실제로 context는 아니고, context가 수행하는 기능 중 하나이다.
* `root-context.xml`에 설정되어 있는 `<context:component-scan>` 태그에 명시되어 있는 패키지를 스캔한다.
* 해당 패키지에 있는 클래스들 중에서 스프링이 사용하는 `@Component`라는 어노테이션이 존재하는 클래스의 인스턴스(Bean)를 생성한다.
* '`@Autowired` 어노테이션이 있는 요소를 가지고 있는 Bean'에 '해당 요소가 필요한 Bean'의 레퍼런스를 찾아서 주입한다.
* 이 과정을 통해 한 객체가 다른 객체에 대해 의존성을 갖게되는 의존성 주입이 이루어진다.

## 참고한 자료
* 코드로 배우는 스프링 웹 프로젝트 개정판 (구멍가게 코딩단 저, 남가람북스)
* https://en.wikipedia.org/wiki/Dependency_injection
* https://stackoverflow.com/questions/7451325/spring-mvc-what-are-a-context-and-namespace

![equation](http://www.sciweavers.org/tex2img.php?eq=1%2Bsin%28mc%5E2%29&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=)