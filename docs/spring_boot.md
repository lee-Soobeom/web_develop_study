# 구조

### 프로젝트 설정

<img src="../docs/imgs/springbootsetting.png">

- `Name`: 프로젝트 이름
- `Location`: 프로젝트가 생성될 위치
- `Language`: 프로젝트 개발에 사용할 언어 설정(Java)
- `Type`: 빌더 및 프로젝트 의존성 관리자 종류 지정(Maven)
- `Group`: 프로젝트 그룹(소유한 도메인의 역순 ex `com.lab`)
- `Artifact`: 프로젝트 식별자(특별한 이유가 없다면 `Name`과 동일하게 지정. 단, 케밥 케이스 사용.)
- `JDK`: 프로젝트를 컴파일할 때 사용할 JDK 지정(17)
- `Java`: IDE에서 문법을 검사할 때 사용할 Java 버전 지정(실제 컴파일 할 때 사용하는 JDK와는 무관. 17)
- `Packaging`: 컴파일 방식 지정
    - `jar`: 웹 애플리케이션이 아카이브에 포함된 형태로 컴파일. 독립된 형태로 실행될 수 있도록 한다.
    - `war`: 웹 애플리케이션이 누락된 상태로 컴파일. 실행하기 위해 별도의 웹 애플리케이션이 요구된다.

### 프로젝트 의존성 설정

<img src="../docs/imgs/developertoolssettings.png">

- `Developer Tools`
    - `Lombok`: 어노테이션 기반 코드 자동완성 및 속성 부여를 위한 의존성.
    - `Spring Boot DevTools`: 스프링 부트 개발 보조 및 생산성 향상을 위한 의존성.
- `Web`
    - `Spring Web`: 스프링 부트 웹 개발 확장 의존성.
- `Template Engines`
    - `Thymeleaf`: 스프링 부트를 활용한 동작 HTML 개발을 위한 템플릿 엔진중 하나인 타임 리프를 사용하기 위한 의존성.
- `SQL`
    - `JDBC API`: JDBC(Java Database Connectivity)는 자바와 데이터베이스간의 연결을 위한 인터페이스의 집합인 구조체이며, 스프링 부트 프레임쿼크에서 직접 관리하지 않는 저수준(
      Low-Level)의 의존성.
    - `Spring Boot Data JDBC`: DBCP(Java Database Pool) 스프링 부트 프레임워크에서 관리하는 고수준(High-Level)의 의존성.
    - `MyBatis Framework`: SQL을 직접 작성하는 매퍼(Mapper) 기반의 ORM(Object-Relational Mapping)의 일종인 MyBatis를 위한 의존성.
    - `MariaDB Driver`: JDBC를 구조체를 구현한 MariaDB DBMS에 접속하기 위한 구현체 의존성.

### 프로젝트 구조

- `.idea`: 해당 프로젝트의 Intellij IDEA 관련 설정을 포함하는 디렉토리. 특별한 경우가 아니라면 건드리지 않는다.
- `.mvn`: Maven 빌더/의존성 관리자 관련 설정을 포함하는 디렉토리. 특별한 경우가 아니라면 건드리지 않는다.
- `src`: 프로젝트의 자바 코드와 리소스를 포함하는 디렉토리.
    - `main`: 프로젝트의 **주**가 되는 자바 코드와 리소스를 포함하는 디렉토리.
        - `java`: 프로젝트의 자바 코드를 포함하는 디렉토리. 해당 디렉토리 밑으로는 자바 코드로 인식하고 자바 문법을 적용한다.
        - `resources`: 프로젝트 자바 코드 외의 리소스(HTML, CSS, JS, 이미지, 영상 등)를 담고있다.
            - `mappers`: MyBatis에서 사용할 SQL을 작성할 XML 파일을 포함하기 위한 디렉토리. 설정에 따라 디렉토리 이름을 변경할 수 있다.
            - `static`: 프로젝트에서 사용할 **정적인** 리소스(정적인 HTML, CSS, JS, 이미지, 영상, 파일 등)을 포함하는 디렉토리. 해당 디렉토리는 **루트(`/`)에 매핑**되어
              있다.
            - `templates`: 프로젝트의 템플릿 엔진을 위한 **동적인** HTML 파일을 포함하는 디렉토리이다.
            - `application.properties`: 서버와 스프링 부트, 의존성들의 설정을 담는 파일.
    - `test`: 프로젝트의 단위 테스트(Unit Test)를 위한 자바 코드와 리소스를 포함하는 디렉토리.
- `.gitattributes`: Git VCS 에서 개별 파일이나 디렉토리에 대한 설정을 명시하기 위한 파일.
- `.gitignore`: Git VCS 에서 개별 파일이나 디렉토리를 제외하기 위한 파일.
- `HELP.md`: Spring Boot와 Maven에 관한 가이드를 담고 있는 파일. 삭제하여도 무관하다.
- `mvnw`: Maven 래퍼(Wrapper). mac/linux 계열 운영체제를 위해 존재한다. 특별한 경우가 아니라면 건드리지 않는다.
- `mvnw.cmd`: Maven 래퍼(Wrapper). 윈도우 계열 운영체제를 위해 존재한다. 특별한 경우가 아니라면 건드리지 않는다.
- `pom.xml`: Maven 빌더/의존성 관리자 및 프로젝트에 대한 설정 파일. 의존성을 추가하는 등의 관리를 할 수 있다.

### 프로젝트 초기 설정

### JDBC 설정

- `JDBC API`, `Spring Boot Data JDBC` 등의 의존성을 설정한 경우 아래와 같이 DBMS와 고ㅘㄴ련된 정보를 `application.properties`에 제공해 주어야 한다.

> ```
>   spring.datasource.driver-class-name=[드라이버 클래스 이름]
>   spring.datasource.url=[접속주소]
>   spring.datasource.username=[사용자 이름]
>   spring.datasource.password=[사용자 비밀번호]
> ```
>
> - `드라이버 클래스 이름`은 JDBC 구조체를 구현하는 구현체의 드라이버 클래스 이름이어야 하며 별도의 의존성을 추가하여야 한다. (MariaDB Driver MySQL Driver, Oracle Driver
    등...)
> - `spring.datasource.url`은 JDBC를 통해 DBMS에 접속할 때 주로 `jdbc:[DBMS 종류]://[호스트]:[포트]/ 의 형식을 사용함 가령 `MariaDB`에 `localhost
    `호스트에, `3306`포트를 사용하여 접속한다면 그 `url`은 `jdbc:mariadb://localhost:3306` 과 같다.

### Thymeleaf 설정

-

### MyBatis 설정

- `MyBatis Framework` 의존성을 추가한 경우 아래와 같이 관련된 정보를 `application.properties`에 제공해 주어야 한다.

> ```
> # MyBatis가 XML파일을 찾아야하는 경로를 지정한다.
>   mybatis.mapper-location=classpath:/mappers/**/*.xml
> ```
>
> - `classpath`는 `/src/main/resource/`를 의미한다.
> - 필요에 따라 디렉토리의 이름을 변경할 수도 있다.

# 웹

<img src="../docs/imgs/structure.png">

## MVC

- `MVC(Model-View-Controller)` 패턴은 웹 개발 및 프로그램 개발 시에 사용하는 개발 패턴중 하나이다.
- 원활한 협업 및 향 후의 유지 관리, 보수를 용이하게 하기 위해 MVC 패턴을 지키면서 개발하는 것이 매우 중요하다.

### Controller

- 컨트롤러(Controller)틑 MVC 패턴에서 실질적으로 사용자(클라이언트)의 요청(Request)을 받아 응답(Response)을 되돌려주는 엔드포인트(끝단, End-Point)역할을 하는 클래스이다.
- 요청을 받을 수 있는 주소(경로)에 대한 매핑(Mapping)된 메서드를 가지고 있다.
- 요청에서 전달받은 인자에 대한 유효성 검사 등의 로직을 직접 구현하지 않는 것이 좋다.
- 데이터베이스에 접속하기 위한 로직을 구현하거나, Data Access Layer(DAL)를 의존성으로 가져서는 안된다.

### Model

#### Service Logic

- 서비스(Service)는 MVC 패턴에서 컨트롤러(Controller)가 넘겨준 인자에 대한 유효성 검사(정규화)를 실시한다.
- 그 외 대체적인 로직을 구현하고, 컨트롤러(Controller)와 Data Access Layer(DAL)간의 연결고리 역할을 한다.
- 데이터베이스에 접속하기 위한 로직을 구현할 수 없다.
- Data Access Layer(DAL)을 의존성으로 가질 수 있다.

#### Data Access Layer(DAL)

- Data Access Layer(DAL)는 MVC 패턴에서 데이터 베이스에 직접적으로 접근할 수 있는 **유일한** 구성요소이다.
- 넘겨받는 데이터에 대한 로직을 구현하거나 패턴 내의 다른 구성요소에 대한 의존성을 가지지 않아야 한다.
    - Data Access Object(DAO): JDBC API를 통한 `DriverManager`가 제공하는 기능으로 저수준(Low-Level) 코드로 직접 데이터 베이스에 연결하여 필요한 CRUD 기능을
      구현한다.
    - Repository: JPA(Java Persistence API) 등의 ORM(Object-Relational Mapping)을 사용할 때 사용하는 DAL의 **접미어**이다.
    - Mapper: MyBatis 등의 SQL Mapper를 사용할 때 사용하는 DAL의 **접미어**이다.

#### Data Structure

- Entity: 데이터베이스의 테이블과 **패킹(1:1 매치)** 되는 데이터 구조 클래스이다. 테이블이 가지는 열을 멤버 변수로 가지고, 기본 키(Primary Key)에 대해 동일성을 판별한다.
- Data Transfer Object(DTO): 계층 간의 데이터를 전달하거나 엔티티가 가질 수 없는 데이터를 추가로 가지게 하기 위해 사용한다. 가변적(Mutable)이고, 참조(Reference) 기반으로
  동일성을 판별한다.
- Value Object(VO): 계층 간의 데이터를 전달하거나 엔티티가 가질 수 없는 데이터를 추가로 가지게 하기 위해 사용한다. 불변적(Immutable)이고, 값 기반으로 동일성을 판별한다.

### View

- 뷰(View)는 MVC 패턴에서 사용자에게 보여질 화면을 구현하는 부분이다. 주로 동적인 HTMl 표현을 위해 많이 사용한다.
- 뷰를 처리하기 위한 템플릿 엔진(Template Engine)의 종류가 많은데 대표적인 예는 아래와 같다
    - JSP
    - Thymeleaf
    - FreeMaker

### 의존성 주입

- 의존성 주입(DI, Dependency Injection)은 객체 지향의 프로그래밍(OOP, Object-Oriented Programming)에서 코드를 더 유연하고 테스트 용이하게 만들기 위해 사용하는 디자인 패턴이다.
- 계층(Layer)이나 항목간의 관계를 보다 명확하게 한다. (가령, 컨트롤러-서비스, 서비스-매퍼 계층 간의 관계)
- 의존성을 주입하는 방법은 여러가지가 있다.
  - 생성자를 통한 의존성 주입(Constructor DI)
    - 장점
      - 불변성(Immutability)을 보장한다.
      - 의존성이 명확하다.
    - 단점 
      - 의존성이 많을 경우 생성자의 매개변수 구조가 복잡하다. (미미한 단점)
    - 방법
      - 의존자에게 피의존자 타입의 멤버 변수(상수)를 선언한다.
      - 의존자에게 피의존자 타입의 멤버 변수(상수)를 초기화 할 수 있도록 이를 매개변수로 전달 받는 생성자를 구성한다.
      - 해당 생성자에 `@Autuowired`어노테이션을 부여한다.
    - 가령 `SomeController`가 `SomeService`에 대해 의존적이라면 그 구성은 아래와 같다.
    >```
    >      @Controller
    >      public class SomeController {
    >          private final SomeService someService;
    >   
    >          @Autowired
    >          public SomeController(SomeService someService) {
    >              this.someService = someService;
    >          }
    >      }
    >```
    >
    > - 위 코드에서 `SomeController`는 `SomeService`의 기능을 사용하여야 하고, `SomeController`는 `SomeService`에 대해 의존적이라고 얘기한다.
  - 필드를 통한 의존성 투입(field DI)
     - 장점
       - 쉽다.
     - 단점
       - 불변성이 보장되지 않는다.
       - 의존성이 명확하지 않다.
     - 방법
       - 의존자에게 피의존자 타입의 멤버 변수를 선언하고 `@Autowired` 어노테이션을 부여한다.
     - 가령 `SomeController`가 `SomeService`에 대해 의존적이라면 그 구성은 아래와 같다.
    >```
    >     @Controller
    >     public class SomeController {
    >         @Autowired
    >         private SomeService someService;
    >     }
    >```

# 어노테이션

- 어노테이션(Annotation)은 자바에서 특정 대상(클래스, 메서드, 변수 등)의 상태나 속성을 부여하기 위해 사용한다.

## Spring Boot

- `@Aurowired`(멤버 변수, 생성자): 해당 멤버 변수나 생성자가 가지고 있는 매개 변수를 **스프링 프레임워크가 객체화**하여야 한다는 지정이다. 단, 대상은 프레임워크가 인식할 수 있는 범위 내에 있는 빈(`Bean`)이어야 한다.
- `@Controller`(클래스): 해당 클래스가 컨트롤러임을 알린다.
    - 속성
        - `value`: 해당 컨트롤러의 식별자를 지정한다. 생략시 클래스의 이름을 사용한다. (이름에 경로 사용하면 겹치지 않게 사용가능하다.)
- `@RequestMapping`(클래스, 메서드): 요청을 받아들일 경로 매핑을 지저한다.
    - 해당 어노테이션이 클래스에 부여되어 있을 경우 해당 클래스가 가지는 모든 매핑되어 있는 메서드의 매핑 경로에 대한 접두어로 동작한다.
    - 해당 어노테이션이 메서드에 부여되어 있을 경우 매핑된 경로로 요청이 발생했을 때 해당 메서드를 실행하게 된다.
    - `@Controller`혹은 `@RestController` 어노테이션이 부여된 클래스 스스로 혹은 내부에서 사용되었을 때 유효하다.
    - 속성
        - `method`: 해당 매핑이 받아들일 요청 방식(HTTP Method)을 `RequestMethod`(
          `org.springframework.web.bind.annotation.RequestMethod`)가 가지는 멤버로 지정한다. 별도로 지정하지 않을 경우 모든 방식을 허용한다.
        - `produces`: 해당 매핑에 대한 요청의 응답 결과로 반환된 `Content-Type`을 `MediaType`(`org.springframework.http.MediaType`)이 가지는 멤버로 지정한다. 생략시 프레임워크가 스스로 판단한다.
        - `value` 혹은 `path`: 해당 매핑의 경로를 문자열로 지정한다.
- `@RequestParam`(매개 변수): 클라이언트가 요청과 함께 보낸 데이터를 매개변수에 할당하기 위해 사용한다.
    - `value`: 클라이언트가 전달하는 변수의 이름을 지정한다.
    - `defaultValue`: 클라이언트가 해당 변수를 누락하였을 때 사용할 기본 값을 문자열로 지정한다.
    - `required`: 해당 매개 변수에 할당할 데이터가 반드시 있어야 하는가의 여부를 지정한다. 기본 값은 `true`이며, `true`일 때 해당 값을 누락할 경우 `400`(Bad Request)오류가 발생한다.
- `@ResponseBody`(메서드): 해당 메서드의 반환 타입이 문자열(`String`)일 때,템플릿을 뷰(`View`)로 처리하는 것이 아닌, 문자열 그대로가 응답으로 반환되어야 함을 지정한다.
    - 반환 타입이 문자열일 때 뿐만 아니라 응답 결과가 클라이언트에게 그대로 전달되어야 할 때 해당 어노테이션을 부여한다.
- `@Service`(클래스): 해당 클래스가 서비스임을 알린다.
    - 속성
        - `value`: 해당 서비스의 식별자를 문자열로 지정한다. 생략시 클래스의 이름을 사용한다.

