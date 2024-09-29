# spring-tutorial-20th
CEOS 20th BE Study - Spring Tutorial

### 🌱 Spring Initializer로 프로젝트 시작

https://start.spring.io/

- Project : Gradle - Groovy
- Language : [Java 17](https://www.oracle.com/java/technologies/downloads/)
- Spring Boot : 3.1.2
- Project Metadata
    - Group : com.ceos20
    - Artifact : spring-boot
    - Name : spring-boot
    - Description : Demo project for Spring Boot
    - Package name : com.ceos20.spring-boot
    - Packaging : Jar
    - Java version : 17
- Dependencies
    - Spring Web

→ 다운로드 후 파일을 작업하고자 하는 파일에 옮겨넣고, .gitignore 파일을 추가

다운로드한 폴더 안에 있는 파일들 다 밖으로 빼기

- .gitignore
    
    ```
    *#
    *.iml
    *.ipr
    *.iws
    *.jar
    *.sw?
    *~
    .#*
    .*.md.html
    .DS_Store
    .attach_pid*
    .classpath
    .factorypath
    .gradle
    .metadata
    .project
    .recommenders
    .settings
    .springBeans
    .vscode
    /code
    MANIFEST.MF
    _site/
    activemq-data
    bin
    build
    !/**/src/**/bin
    !/**/src/**/build
    build.log
    dependency-reduced-pom.xml
    dump.rdb
    interpolated*.xml
    lib/
    manifest.yml
    out
    overridedb.*
    target
    .flattened-pom.xml
    secrets.yml
    .gradletasknamecache
    .sts4-cache
    
    .idea
    ```
    

### 🌱 Application 실행

로컬 서버를 열기

1. 빌드 > 프로젝트 빌드
    
    build.gradle 파일도 수정할 때마다 build 해줘야됨
    
2. src > main > java > Application.java 파일 실행

### 🌱 서버 동작 확인

[http://localhost:8080](http://localhost:8080/) 에 접속하면 서버가 띄어진 것을 확인할 수 있음

### 🌱 build.gradle 파일 수정

```java
dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-web'

	implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
	compileOnly 'org.projectlombok:lombok'
	annotationProcessor 'org.projectlombok:lombok'
	
	// mysql 연결
	implementation 'mysql:mysql-connector-java:8.0.33'

	// 단위 테스트
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
}
```

<aside>
🤔

**lombok이란?**

자바에서 사용되는 라이브러리

코드 작성 시 반복적으로 작성해야 하는 보일러플레이트 코드를 줄여주는 도구

- `@Getter` `@Setter`
    
    해당 클래스의 필드에 대한 getter와 setter 메서드가 자동으로 생성됨
    
- `@ToString`
    
    클래스의 toString 메서드를 자동으로 생성
    
- `@EqualsAndHashCode`
    
    equals 및 hashCode 메서드 자동 생성
    
- `@NoArgsConstructor` `@AllArgsConstructor`
    
    인자가 없는 기본 생성자 및 모든 필드를 인자로 받는 생성자를 자동으로 생성
    

<aside>
🤔

**보일러플레이트(boilerplate)란?**

반복적인 코드

- getter/setter 메서드
- 로그 설정
- 데이터베이스 연결 설정
</aside>

</aside>

### 🌱 application.yml

파일명 변경: `application.properties`  → `application.yml`

<aside>
🤔

**파일 명을 변경하는 이유**
둘 다 스프링 프레임워크에서 애플리케이션의 설정을 정의하는 데 사용되는 구성 파일

`application.properties` 

- key-value 쌍으로 설정 정의
- `key=value` 형식
- 구문이 단순하고 직관적, 자바 개발자에게 익숙한 형식

```java
spring.datasource.url=jdbc:mysql://localhost:3306/your_database_name
spring.datasource.username=your_username
spring.datasource.password=your_password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

`application.yml`

- YAML 형식
    
    중첩된 구조를 들여쓰기를 통해 표형할 수 있음
    → 설정을 계층적으로 구성할 수 있음
    
- `key: value` 형식
- 복잡한 설정 구조화 가능

```java
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/your_database_name
    username: your_username
    password: your_password
    driver-class-name: com.mysql.cj.jdbc.Driver
```

</aside>

# 🌳 스프링의 이해

## 🪴 Spring이란?

**자바 엔터프라이즈 개발을 편하게 해주는 오픈소스 경량급 애플리케이션 프레임워크**

<aside>
🤔

**경량 컨테이너란?**

스프링은 모든 기능을 한꺼번에 제공하는 것이 아닌, 필요한 기능만 가볍게 추가해서 쓸 수 있는 구조로 되어 있음. 다른 복잡한 서버나 프레임워크처럼 모든 걸 포함하는 거대한 시스템이 아닌, 최소한의 리소스로 작동할 수 있도록 가볍게 설계되어 있음 → 경량

스프링은 애플리케이션의 객체들을 관리하는 역할을 함 → 컨테이너

</aside>

## 🪴 Spring의 특징

자바 객체를 직접 스프링 안에서 관리

객체의 생성 및 소명과 같은 생명 주기를 관리하며, 스프링 컨테이너에서 필요한 객체를 가져와 사용함

### 🌱 POJO

Plain Old Java Object. 오래된 방식의 순수한 자바 객체

- Getter, Setter로 구성된 가장 순수한 형태의 기본 클래스
- 객체지향적인 원리에 충실하면서, 특정 프레임워크나 라이브러리의 특정 기능에 종속되지 않고, 필요에 따라 재활용될 수 있는 방식으로 설계된 오브젝트
- e.g.
    
    ```java
    public class Student {
        private String name;
        private int age;
    
    		public Student(String name, int age) {
    			this.name = name;
    			this.age = age;
    		}
        public String getName() {
        	return name;
        }
        public String getAge() {
        	return age;
        }
    
        public void setName(String name) {
        	this.name = name;
        }
    
        public void setAge(int age) {
        	this.age = age;
        }
    }
    ```
    

**POJO의 장점**

- 특정 프레임워크나 라이브러리의 특정 기능에 의존하지 않는 오브젝트는 그만큼 깔끔한 코드가 될 수 있음
- 환경의 제약이 없다는 점이 자동화된 테스트에 이점이 됨
- 객체지향적 설계를 자유롭게 적용할 수 있음

**POJO 프레임워크**

POJO 프로그램이 가능하도록 기술적인 기반을 제공하는 프레임워크

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/d6cd7a95-d578-4984-bc27-c7e8cb6ebb02/11a4d2eb-f053-4bdb-94d1-7c0201b002c0/image.png)

스프링은 비즈니스 로직의 복잡함과 엔터프라이즈 기술의 복잡함을 분리해서 구성할 수 있게 도와줌

POJO는 비즈니스 로직을 단순하고 명확하게 표현할 수 있게 해줌

스프링은 대표적인 POJO 프레임워크 → 자신을 직접 노출하지 않으면서 어플리케이션을 POJO로 쉽게 개발할 수 있게 지원

즉, 분리됐지만 필요한 서비스 기술을 POJO 방식으로 개발된 애플리케이션 핵심 로직을 담은 코드에 제공 

<aside>
🤔

**비즈니스 로직 vs 엔터프라이즈 기술**

비즈니스 로직

애플리케이션이 해야 할 핵심 기능이나 목적을 수행하는 코드

e.g. 은행 어플에서 돈을 입/출금하는 기능, 병원 관리 시스템에서 환자의 예약을 처리하고 관리하는 로직

→ 개발자가 스프링을 사용하면 비즈니스 로직에만 집중할 수 있음

엔터프라이즈 기술의 복잡함

애플리케이션이 정상적으로 동작하기 위해 필요한 기술적 문제들을 처리

시스템의 안정성, 보안성, 성능, 확장성 등을 보장하기 위해 사용됨

e.g. 데이터베이스 연결, 트랜젝션 관리, 로그 관리, 멀티스레드 처리

→ 스프링에서 제공하는 다양한 자동화 기능이나 설정을 통해 처리할 수 있음

```java
@Service
public class BankService {

    @Autowired
    private AccountRepository accountRepository;

    @Transactional // 트랜잭션 관리 자동 처리
    public void transferMoney(long fromAccountId, long toAccountId, BigDecimal amount) {
        Account fromAccount = accountRepository.findById(fromAccountId);
        Account toAccount = accountRepository.findById(toAccountId);

        fromAccount.withdraw(amount);
        toAccount.deposit(amount);

        accountRepository.save(fromAccount);
        accountRepository.save(toAccount);
    }
}
```

→ 비즈니스 로직인 *돈을 이체하는 로직* 에 집중할 수 있게 되어 있음. 데베 연결이나 트랜젝션 관리는  `@Transactional` 등의 어노테이션을 통해 스프링이 알아서 처리해주기 때문에, 개발자는 그런 복잡한 기술적 문제를 걱정하지 않아도 됨

</aside>

### 🌱 Spring 삼각형

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/d6cd7a95-d578-4984-bc27-c7e8cb6ebb02/46b965f6-ee6c-466a-9586-d7f904662264/image.png)

**의존성이란**

전체는 부분에 의존한다

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/d6cd7a95-d578-4984-bc27-c7e8cb6ebb02/3144c150-45f2-4ff7-a1aa-8e4e9bac2160/image.png)

전체: Car

부분: Tire

Car에는 Tire가 필요하다. 

즉, Car는 Tire에 의존적이다.

**의존성 주입(DI)가 필요한 이유**

```java

public class Car {

	Tire tire;

	public Car() {
		tire = new KoreaTire();
		// tire = new AmericaTire();
	}

}
```

- Car 클래스의 생성자에서 KoreaTire를 생성한다
- 위 코드는 의존성을 외부에서 주입받은 것이 아닌, Car 클래스 내부에서 의존성을 직접 해결한 경우

→ 위 코드의 문제점은?

1. 모든 Car가 같은 Tire를 사용하게 됨
    
    ```java
    Car car1 = new Car();
    Car car2 = new Car();
    
    // car1 과 car2 모두 KoreaTire 로 고정됨
    ```
    
2. Car의 tire를 바꾸고 싶다면 Car 클래스의 생성자를 직접 수정해야 함
    
    ```java
    
    public class Car {
    
    	Tire tire;
    
    	public Car() {
    		// tire = new KoreaTire();
    		tire = new AmericaTire();
    	}
    
    }
    ```
    
    Car 클래스와 Tire 클래스의 결합도가 강해서 코드의 확장성이 떨어짐. Tire 바꾸고 싶을 때마다 매번 코드를 수정해야됨
    

⇒ 의존성 주입으로 위 문제 해결 가능!

**의존성 주입 방법**

생성자 주입

생성자의 인자로 tire를 받기

```java
public class Car {

	Tire tire;

	public Car(Tire tire) {
		this.tire = tire;
	}

}
```

외부에서 Car의 tire 의존성을 주입해줌

```java
Tire tire = new KoreaTire();

Car car = new Car(tire); // 생성자 주입
```

→ Car 입장에서는 어떤 Tire를 장착할 지 고민하지 않아도 됨

→ Car 클래스와 Tire 클래스의 결합이 느슨해짐

setter 주입(속성을 통한 의존성 주입)

setter에서 tire를 받아 tire 필드를 정함

```java
public class Car {

	Tire tire;

	public void setTire(Tire tire) {
		this.tire = tire
	}

}
```

```java
Tire tire = new KoreaTire();

Car car = new Car();

car.setTire(tire); // setter 주입
```

필드 주입

```java
import org.springframework.beans.factory.annotation.Autowired;

public class Car {

	@Autowired
	Tire tire;

}
```

```java
import org.springframework.stereotype.Component;

@Bean
public class KoreaTire implements Tire {
    // ...
}
```

- `@Bean` 같은 어노테이션을 사용하면 Bean에 Tire가 등록됨
- `@Autowired` : 스프링이 해당 필드에 필요한 객체를 자동으로 주입
- 필드 주입은 한 번 주입된 의존성을 변경하지 않고 유지하는 경우에 적합
    
    cf) `@Qualifier` 를 사용하면 직접 Bean을 선택할 수 있긴 함
    
    ```java
    @Service
    public class CreditCardPaymentService implements PaymentService {
        // 구현 내용
    }
    
    @Service
    public class PayPalPaymentService implements PaymentService {
        // 구현 내용
    }
    ```
    
    ```java
    @Service
    public class OrderService {
    
        @Autowired
        @Qualifier("creditCardPaymentService")  // 특정 빈 선택
        private PaymentService paymentService;
    
        public void processOrder() {
            paymentService.processPayment();
        }
    }
    ```
    

**IoC (Inversion of Control / 제어의 역전)**

객체들 간의 관계 및 호출을 개발자가 아니라 스프링 프레임워크에게 맡기는 것

Spring IoC 컨테이너의 역할

- 빈 관리
    
    IoC 컨테이너는 애플리케이션에서 사용되는 객체(빈)를 생성하고 관리
    
    개발자는 객체 생성과 관리에 대한 부분을 신경 쓰지 않아도 됨
    
- 의존성 주입
    
    IoC 컨테이너는 빈 간의 의존성을 관리하고 필요한 의존성을 주입
    
    → 객체 간의 결합도를 낮추고, 코드의 재사용성과 유지보수성을 향상시킴
    
- 라이프사이클 관리
    
    IoC 컨테이너는 빈의 라이프사이클을 관리하며, 초기화와 소멸 시점에서 콜백 메서드를 호출할 수 있음
    
    <aside>
    🤔
    
    **콜백 메서드**
    
    미리 정의해놓고, 나중에 측정 상황이 발생하면 실행되는 메서드
    
    e.g. 버튼 클릭 → 버튼 클릭이라는 이벤트가 발생하면 콜백 메서드가 자동으로 실행
    
    </aside>
    
    e.g. 빈 초기화 시 특정 설정을 수행하거나, 빈 소멸 시 리소스를 정리하기 등
    
- 설정 관리
    
    IoC 컨테이너는 애플리케이션 설정을 관리하고, XML, Java 설정 클래스, 어노테이션 기반의 설정을 지원
    

IoC vs DI

- DI(Dependency Injection / 의존성 주입)
- IoC는 디자인패턴이고, DI는 IoC를 구현한 방식의 하나
- DI는 IoC의 핵심 원칙 중 하나인 “의존성 역전”을 실제로 구현하는 방법 중 하나일 뿐
- DI는 IoC의 하위개념

### 🌱 AOP

**Aspect-Oriented Programming / 관점 지향 프로그래밍**

- DI가 의존성(new)의 주입이라면, AOP는 로직(code)의 주입
- 코드 = 핵심 관심사 + 횡단 관심사
    - 핵심 관심사: 각 모듈 별 핵심 로직
    - 횡단 관심사(cross-cutting concern): 여러 모듈에 공통적으로 나타나는 로직
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/d6cd7a95-d578-4984-bc27-c7e8cb6ebb02/0026e317-0a77-45d7-ac4b-abf152b231c0/image.png)
    
- 메서드에 로직을 주입할 수 있는 곳
    - Around
    - Before
    - After
    - AfterReturning
    - AfterThrowing
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/d6cd7a95-d578-4984-bc27-c7e8cb6ebb02/cea97ce3-50cd-4574-a44c-3c6fc2304a0a/image.png)
    

### 🌱 PSA

**Portable Service Abstraction / 일관성 있는 서비스 추상화**

- 어댑터 패턴을 적용해서 같은 일을 하는 다수의 기술을 공통의 인터페이스로 제어할 수 있게 한 것
    
    <aside>
    🤔
    
    **어댑터 패턴**
    
    디자인 패턴 중 하나로, 서로 호환되지 않는 인터페이스를 가진 클래스들이 함께 작동할 수 있도록 중간에 어댑터를 두어 연결해 주는 방식
    
    e.g. 
    
    기존 인터페이스
    
    ```java
    public interface MediaPlayer {
        void play(String audioType, String fileName);
    }
    ```
    
    새롭게 추가된 클래스 → 기존 인터페이스와 호환되지 않음
    
    ```java
    public class AdvancedMediaPlayer {
        public void playMp4(String fileName) {
            System.out.println("Playing mp4 file. Name: " + fileName);
        }
        
        public void playVlc(String fileName) {
            System.out.println("Playing vlc file. Name: " + fileName);
        }
    }
    ```
    
    어댑터 클래스
    
    ```java
    public class MediaAdapter implements MediaPlayer {
        AdvancedMediaPlayer advancedMediaPlayer;
    
        public MediaAdapter(String audioType) {
            if (audioType.equalsIgnoreCase("vlc")) {
                advancedMediaPlayer = new AdvancedMediaPlayer();
            } else if (audioType.equalsIgnoreCase("mp4")) {
                advancedMediaPlayer = new AdvancedMediaPlayer();
            }
        }
    
        @Override
        public void play(String audioType, String fileName) {
            if (audioType.equalsIgnoreCase("vlc")) {
                advancedMediaPlayer.playVlc(fileName);
            } else if (audioType.equalsIgnoreCase("mp4")) {
                advancedMediaPlayer.playMp4(fileName);
            }
        }
    }
    ```
    
    클라이언트 클래스 (어댑터 사용)
    
    ```java
    public class AudioPlayer implements MediaPlayer {
        MediaAdapter mediaAdapter;
    
        @Override
        public void play(String audioType, String fileName) {
            // mp3 형식은 기본적으로 지원
            if (audioType.equalsIgnoreCase("mp3")) {
                System.out.println("Playing mp3 file. Name: " + fileName);
            }
            // mp4 또는 vlc 형식은 어댑터를 통해 재생
            else if (audioType.equalsIgnoreCase("mp4") || audioType.equalsIgnoreCase("vlc")) {
                mediaAdapter = new MediaAdapter(audioType);
                mediaAdapter.play(audioType, fileName);
            } else {
                System.out.println("Invalid media type: " + audioType);
            }
        }
    }
    ```
    
    사용 예시
    
    ```java
    public class AdapterPatternDemo {
        public static void main(String[] args) {
            AudioPlayer audioPlayer = new AudioPlayer();
    
            audioPlayer.play("mp3", "song.mp3");
            audioPlayer.play("mp4", "video.mp4");
            audioPlayer.play("vlc", "movie.vlc");
            audioPlayer.play("avi", "film.avi");  // 지원되지 않는 형식
        }
    }
    ```
    
    결과
    
    ```java
    Playing mp3 file. Name: song.mp3
    Playing mp4 file. Name: video.mp4
    Playing vlc file. Name: movie.vlc
    Invalid media type: avi
    ```
    
    </aside>
    
- 예를 들어 MySQL, PostgreSQL 등 다른 기술들을 사용하더라도 JDBC 라는 공통의 표준 스펙(인터페이스)을 통해서 공통된 방식으로 코드를 작성할 수 있음
- `@Transactional` 은 JPA, JDBC**를**  사용하든 변경없이 사용 가능함
    
    → 내부 작동을 알 필요 없이 다 사용 가능함
    

## 🪴 Spring Boot

스프링은 알려진 자바 엔터프라이즈 에디션을 경량화하려는 대안으로 시작함. 컴포넌트 코드 작성은 가벼웠으나 개발 구성은 무거웠음. 즉, 프로젝트 시작 시 설정해야할 내용이 많아짐. 이 모든 구성 작업은 개발 저항으로 나타남. → 스프링 부트로 해결

### 🌱 Spring Boot

스프링 기반의 어플리케이션를 빠르게 개발하고 실행하기 위한 프레임워크

**스프링 부트의 특징**

- WAS
    
    Tomcat 같은 웹 서버를 내장해서 별도의 웹 서버를 설치하지 않아도 됨
    
- 라이브러리 관리
    
    손쉬운 빌드 구성을 위한 스타터 종속성 제공 및 라이브러리 버전 관리
    
- 자동 구성
    - 프로젝트 시작에 필요한 스프링과 외부 라이브러리의 빈을 자동 등록
    - 스프링 애플리케이션에 공통으로 필요한 애플리케이션 기능을 자동으로 구성
- 외부 설정
    
    환경에 따라 달라져야 하는 외부 설정 공통화
    
- 프로덕션 준비
    
    모니터링을 위한 메트릭, 상태 확인 기능 제공
    
    - 스프링 애플리케이션 컨텍스트에 구성된 빈
    - 스프링 부트의 자동 구성으로 구성된 것
    - 애플리케이션에서 사용할 수 있는 환경 변수, 시스템 프로퍼티, 구성 프로퍼티, 명령줄 인자
    - 최근에 처리된 HTTP 요청 정보
    - 메모리 사용량, 가비지 컬렉션, 웹 요청, 데이터 소스 사용량 등 다양한 메트릭

# 🌳 Spring Bean

# 🌳 단위 테스트와 통합 테스트

### 단위 테스트 (Unit Test)

- 외부 시스템(DB, 네트워크, 파일 시스템 등)에 의존하지 않고, 독립적으로 실행
- 모킹(Mocking) 기법을 사용해서 외부 의존성 제거

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}

// 단위 테스트 코드
import static org.junit.Assert.assertEquals;
import org.junit.Test;

public class CalculatorTest {
    @Test
    public void testAdd() {
        Calculator calculator = new Calculator();
        int result = calculator.add(2, 3);
        assertEquals(5, result);  // 2 + 3 = 5
    }
}
```

### 통합 테스트 (Integration Test)

- 외부 시스템과의 상호작용

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class UserServiceIntegrationTest {

    @Autowired
    private UserService userService;

    @Test
    public void testCreateUser() {
        User user = new User("John", "Doe");
        User createdUser = userService.createUser(user);

        assertNotNull(createdUser.getId());  // 데이터베이스에서 생성된 사용자의 ID가 존재하는지 확인
        assertEquals("John", createdUser.getFirstName());
        assertEquals("Doe", createdUser.getLastName());
    }
}
```
