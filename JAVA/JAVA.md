## 1. Garbage Collection(가비지 컬렉션)이란?

###  [ Garbage Collection(가비지 컬렉션)이란? ]

- 프로그램을 개발 하다 보면 유효하지 않은 메모리인 가바지(Garbage)가 발생하게 된다. 
- C언어를 이용하면 free()라는 함수를 통해 직접 메모리를 해제해주어야 한다. 
- 하지만 Java나 Kotlin을 이용해 개발을 하다 보면 개발자가 메모리를 직접 해제해주는 일이 없다. 
- 그 이유는 JVM의 가비지 컬렉터가 불필요한 메모리를 알아서 정리해주기 때문이다. 
- 대신 Java에서 명시적으로 불필요한 데이터를 표현하기 위해서 일반적으로 null을 선언해준다.



예를 들어 아래와 같은 코드가 있다고 가정하자.

```
Person person = new Person();
person.setName("Mang");
person = null;

// 가비지 발생
person = new Person();
person.setName("MangKyu");
```

기존의 Mang으로 생성된 person 객체는 더이상 참조를 하지 않고 사용이 되지 않아서 Garbage(가비지)가 되었다. Java나 Kotlin에서는 이러한 메모리 누수를 방지하기 위해 가비지 컬렉터(Garbage Collector, GC)가 주기적으

로 검사하여 메모리를 청소해준다.

(물론 Java에서도 **System.gc()**를 이용해 호출할 수 있지만, 해당 메소드를 호출하는 것은 **시스템의 성능에 매우 큰 영향**을 미치므로 절대 호출해서는 안된다.)

 
 

 

### [ Minor GC와 Major GC ]

JVM의 **Heap영역**은 처음 설계될 때 다음의 2가지를 전제(Weak Generational Hypothesis)로 설계되었다.

대부분의 객체는 **금방 접근 불가능한 상태(Unreachable)**가 된다.
오래된 객체에서 **새로운 객체로의 참조는 아주 적게** 존재한다.

- 즉, 객체는 대부분 **일회성**되며, 메모리에 오랫동안 남아있는 경우는 드물다는 것이다. 

그렇기 때문에 객체의 생존 기간에 따라 물리적인 Heap 영역을 나누게 되었는데, 이에 따라 **Young, Old 총 2가지** 영역으로 설계되었다. (초기에는 Perm 영역이 존재하였지만 Java8부터 제거되었다.)

 

#### GC 영역 및 흐름



#####  Young 영역(Young Generation)

> 새롭게 생성된 객체가 **할당(Allocation)**되는 영역
> 대부분의 객체가 금방 Unreachable 상태가 되기 때문에, 많은 객체가 Young 영역에 생성되었다가 사라진다.
> **Young 영역에 대한 가비지 컬렉션**(Garbage Collection)을 **Minor GC**라고 부른다.

##### Old 영역(Old Generation)

> Young영역에서 **Reachable 상태**를 유지하여 살아남은 **객체가 복사되는 영역**
> 복사되는 과정에서 대부분 Young 영역보다 크게 할당되며, 크기가 큰 만큼 가비지는 적게 발생한다.
> **Old 영역에 대한 가비지 컬렉션**(Garbage Collection)을 **Major GC 또는 Full GC**라고 부른다.

- 예외적인 상황으로 Old 영역에 있는 객체가 Young 영역의 객체를 참조하는 경우도 존재할 것이다. 

- 이러한 경우를 대비하여 Old 영역에는 512 bytes의 덩어리(Chunk)로 되어 있는 카드 테이블(Card Table)이 존재한다.

 ![card](https://user-images.githubusercontent.com/77487962/127621494-8fec53e5-411e-4d97-9032-7fbe4b7d5ea0.PNG)


- **카드 테이블**에는 Old 영역에 있는 객체가 Young 영역의 **객체를 참조할 때 마다 그에 대한 정보가 표시**된다. 
- 카드 테이블이 도입된 이유는 간단한다. 
- Young 영역에서 가비지 컬렉션(Minor GC)가 실행될 때 모든 Old 영역에 존재하는 객체를 검사하여 참조되지 않는 Young 영역의 객체를 식별하는 것이 비효율적이기 때문이다. 
- 그렇기 때문에 Young 영역에서 가비지 컬렉션이 진행될 때 카드 테이블만 조회하여 GC의 대상인지 식별할 수 있도록 하고 있다.

#### [Enum Class]
> 열거형
> 상수
##### Enum의 특징
* 상수를 정의 하기 위한 class
* 네이밍 규칙은 대문자
* 생성자는 디폴트가 private 접근제한자
  * Enum은 서로 연관된 상수의 집합이기 때문에 생성자를 통해 값을 초기화 하거나 동적으로 변환하지 못하게 막는다.
* 자주 사용하는 상수들을 Enum을 통해 관리 할 수 있다.
##### Enum의 장점

* 코드가 단순해지고 가독성이 좋다.
* enum class를 사용해 타입을 정의함으로 정의한 타입이외의 타입을 가진 데이터값을 컴파일시 체크한다.
* 키워드 enum을 사용하기 때문에 구현의 의도가 열거임을 분명하게 알 수 있다.

```java
public class Constant {
    private static final String C = "c";
    private static final String JAVA = "java";
    private static final String PYTHON = "python";
}
public enum Type {
    C("c"),
    JAVA("java"),
    PYTHON("python");
    
    private String value;

    Type(String value) {
        this.value = value;
    }

    public String getValue() {
        return value;
    }

    public static Type getType(String arg) {
        for (Type type : Type.values()) {
            if (type.getValue().equals(arg)) {
                return type;
            }
        }
        throw new IllegalArgumentException();
    }

}
```
##### Enum의 메소드
* toString() : (default)상수 이름을 String type으로 return
* name() : 상수 이름을 String type으로 return
* values() : 모든 원소를 배열에 담아 순서대로 return
* valueOf(arg) : arg와 같은 이름을 가진 원소를 반환
```java
public class EnumTest {
    public static void main(String[] args) {
        System.out.println("Type.JAVA : " + Type.JAVA);
        System.out.println("Type.JAVA.toString() : " + Type.JAVA.toString());
        System.out.println("Type.JAVA.name() : " + Type.JAVA.name());
        System.out.println("Type.JAVA.getValue() : " + Type.JAVA.getValue());

        System.out.println("Type.valueof(\"JAVA\") : " + Type.valueOf("JAVA"));
        for (Type t : Type.values()) {
            System.out.println("foreach values() Test: " + t.getValue());
        }
    }
}
```
![image](https://user-images.githubusercontent.com/58085920/129336088-c9657ef5-9e94-46da-b34e-09c3dbdbc116.png)

# 제네릭 (Generic)

+ #### 제네릭이란

  + 클래스 내부에서 사용할 데이터 타입을 외부에서 지정하는 기법을 의미

+ #### 제네릭의 장점

  1. 제네릭을 사용하면 잘못된 타입이 들어올 수 있는 것을 컴파일 단계에서 방지
  2. 클래스 외부에서 타입을 지정하기 때문에 타입을 체크, 변환해줄 필요가 없다.
  3. 비슷한 기능을 지원하는 경우 코드의 재사용성이 높아진다.

+ #### 제네릭 사용방법
 ![](https://images.velog.io/images/qjatn1009/post/c39e2284-7d3d-4b04-8821-766e7d361aa6/image.png)
  + 클래스 및 인터페이스 선언
    ```java
    public class ClassName <T> { ... }
    public interface InterfaceName <T> { ... }
    ```
    기본적으로 클래스나 인터페이스는 위와 같이 선언 T 타입은 { ... } 안에서까지 유효하다.
    ```java
    public class ClassName <K, V> { ... }
    ```
    이렇게 타입 인자를 두 개 받아 선언도 가능하다. 자바의 HashMap도 이러한 형식이다.

  + 제네릭 메소드

    ```java
    public <T> T genericMethod(T o) { ... } 
    [접근 제어자] <제네릭 타입> [반환타입] [메소드 명]([제네릭 타입][파라미터])
    ```

  + 제한된 제네릭과 와일드 카드

    + 위의 예시는 타입을 T라고 하고 외부에서 Integer을 파라미터로 보내면 T는 Integer가 되고 String을 보내면 T는 String이 되고, Student라는 클래스를 보내면 T는 Student가 된다. 이와 달리 특정 범위 내로 제한하는 방법이다.

    + extends, super, ?가 있다. 

      > `<K extends T>`  : T와 T의 자손 타입만 가능
      >
      > `<K super T> ` : T와 T 부모(조상) 타입만 가능
      >
      > `<? extends T >` : T와 T의 자손 타입만 가능
      >
      > `<? super T>` : T와 T 부모(조상) 타입만 가능
      >
      > `<?>` : 모든 타입 가능, `<? extends Object>`와 같은 의미

      + `extends T` : 상한 경계
      + `? super T` : 하한 경계
      + `<?>` : 와일드 카드(Wild card)

    + `K extends T`와 `? extends T`와 비슷한 구조이지만 차이점이 있다. K는 특정 타입으로 지정되지만, ? 는 타입이 지정되지 않는다는 의미이다.

    + `PriorityQueue`에서의 사용 예시
      ```java
      public static class SoltClass <E extends Comparable<E>>{ }
      	
      	public static class SoltClass1 <E extends Comparable<? super E>>{}
      	
      	public static class Person {
      		int age;
      	}
      	
      	public static class Student extends Person implements Comparable<Person>{
      
      		@Override
      		public int compareTo(Person o) {
      			return Integer.compare(this.age, o.age);
      		}
      		
      	}

      	public static void main(String[] args) {
      		SoltClass<Student> a = new SoltClass<Student>();
      		SoltClass1<Student> b = new SoltClass1<Student>();
      	}
      ```

      + 사용시 SoltClass<Student> a = new SoltClass<Student>();는 에러가 발생
        + Person 객체로 Comparable를 선언했기 때문에 SoltClass에선 `Comparable<Student>`로 인식하기 때문인듯 하다. `Student`클래스에서 `Comparable<Student>`로 변환하면 둘다 작동을 하는 것을 볼 수 있다.

  > 참고사항 : https://st-lab.tistory.com/153
 
 # 자바 8버전
> 자바는 8버전에서 많은 사항들이 추가되었고 많이 사용되는 버전이기도 하다.
람다,스트림등 여러 기능이 추가 되었다.
이번에는 자바 8에서 어떤 기능들이 추가되었는지 알아보자.

# 람다 표현식
> 람다 표현식이란?

* 함수형 프로그래밍

식별자 없이 실행할 수 있는 함수표현식을 의미하며 익명함수라고 부른다.
람다표현식은 불필요한 코드의 작성을 줄여주고 가독성을 높여준다.
가장 크게 스레드의 생성 방식에서 그 차이를 알 수 있다.
```java
new Thread(new Runnable() {
    public void run() {
        System.out.println("람다가 아닌 기존 익명함수를 이용한 스레드 생성");
    }
}).start();

new Thread(()->{
    System.out.println("람다를 이용한 스레드 생성");
}).start();
```

# 스트림 API

* 데이터를 추상화하여  다양한 방식으로 저장된 데이터를 읽고 쓰는 방법을 제공하는 API
* 배열이나 컬렉션뿐 아니라 파일에 저장된 데이터도 스트림을 통해 제어가능
* 반복문이나 반복자를 매번사용하지 않아도 됨

```java
private static final int BEST_SCORE = 100;
List<Node> nodes = new ArrayList<>();
List<Node> list = new ArrayList<>();

//기존의 반복문을 이용한 방식
for(Node node : nodes){
	if(node.getScore() == BEST_SCORE){
    	pickedList.add(node);
    }
}
//stream을 이용한 방식
list.stream().filter(node -> node.getScore() == BEST_SCORE).collect(toList());
```

# Interface Default Method
* 인터페이스에서 구현체를 인터페이스 자체에서 기본으로 제공가능
```java
public interface Sized{
	int size();//기존의 인터페이스 처럼 선언 해놓고 오버라이딩
    
	default boolean isEmpty() {  // Default Method
		return size() == 0;
	}
}
```
# Java.time
* 기존에 Calendar클래스를 사용했지만 아래와 같은 문제점 발생

>
* Calendar 인스턴스는 immutable object가 아니라서 값이 수정될 수 있다.
* 윤초와 같은 특별한 상황을 고려하지 않습니다.
* Calendar 클래스에서는 월을 나타낼 때 1~12가 아닌 0~11로 표현해야한다.

* LocalDateTime, LocalDate라는 클래스를 사용하게 됨
```java
LocalDate today = LocalDate.now();
System.out.println("올해는" + today.getYear() + "년입니다.");

LocalDateTime time = LocalDateTime.now();
System.out.println(time.plusMinutes(60));
```

# Optional Class
* Optional<T>로 캡슐화를 하여 NullPointerException을 막는다
* 값이 존재한다면 값을 Optional클래스가 감싼다.
* 값이 존재하지 않는다면 Optional.empty메소드로 리턴함

# 영속성 컨텍스트
> 엔티티를 영구적으로 저장하는 환경이라는 뜻(논리적 개념)

* 엔티티 매니저를 통해 영속성 컨텍스트에 접근
* JPA는 쓰레드 생성마다(요청 생성) EntityManagerFactory에서 EntityManager를 생성함
* 엔티티 매니저를 통해 영속성 컨텍스트에 접근하고 관리할 수 있다.

# 엔티티의 생명주기
* **비영속(new)**
  * 영속성 컨텍스트와 전혀 관계가 없는 새로운 상태
  * 객체를 생성만함
  ```java
   Member member = new Member();
  ```
* **영속(managed)**
  * 영속성 컨텍스트에 관리 되는 상태
  ```java
   em.persist(member);
  ```
* **준영속(detached)**
  * 영속성 컨텍스트에 저장되었다가 분리된 상태
  ```java
   em.detach(member);
   em.clear();
   em.close();
  ```
* **삭제(removed)**
  * 삭제된 상태
  ```java
   em.remove(member);
  ```
  
![](https://images.velog.io/images/dbtlwns/post/bb4bef62-ab62-4051-ab7b-624941c63e4d/image.png)

# 영속성 컨텍스트를 왜 사용할까?

### 1차캐시
 * 영속성 컨텍스트 내부의 캐시
``` java
    Member member = new Member();
    member.setId("simba");
    em.persist(member);
    Member findMember1 = em.find(Member.class,"simba"); //1차 캐시 조회
    Member findMember2 = em.find(Member.class,"sijun");
    //1차캐시 조회 -> DB조회 -> 1차 캐시 갱신 -> 반환
```
 
###  동일성 보장
* 엔티티의 동일성을 보장함
``` java
    Member findMember1 = em.find(Member.class,"simba"); 
    Member findMember2 = em.find(Member.class,"simba");
    if(findMember1 == findMember2){ // true
    	System.out.println("같은 객체입니다.");
    }
```

### 트랜잭션을 지원하는 쓰기 지연
* 말그대로 (데이터베이스에)쓰기를 지연
``` java
    transaction.begin();
    em.persist(member);
    //insert 쿼리가 날라가지 않음
    //로직
    //로직끝
    transaction.commit();
    //insert 쿼리가 날라감
```
### 변경 감지
* 엔티티 수정을 감지
* 영속상태의 엔티티만 적용
``` java
    transaction.begin(); 
    Member member = em.find(Member.class, "member");
    // 영속 엔티티 데이터 수정
    member.setUsername("helloworld");
    //em.update(member); 이런코드 없음
    transaction.commit();
```

# 플러시
> 영속성 컨텍스트의 변경내용을 데이터베이스에 반영

### 플러시 발생
* 변경감지

* 수정된 엔티티 쓰기 지연 SQL저장소에 등록

* 쓰기지연 SQL 저장소의 쿼리를 데이터베이스에 전송

### 플러시가 하는 법

* em.flush();

* ransaction.commit();

* JPQL 쿼리 실행시 자동 호출

# 참고한 곳

[김영한님의 자바 ORM 표준 JPA프로그래밍](https://www.inflearn.com/course/ORM-JPA-Basic/dashboard)

	
# 의존성 주입
> 스프링을 사용하는 큰 이유중 하나인 의존성주입. 스프링에서는 Ioc컨테이너에 빈으로 등록된다면 @Autowired 어노테이션을 통해 의존성 주입이 가능하다. 생성자,setter,필드 총 3가지로 의존성 주입이 가능하다. 

# 필드 주입
> 필드를 통해 의존성을 주입함

```java
@Controller
public class MemberController{
	@Autowired
	private MemberService memberService;
}
```

* 장점
  * 그중에서도 가장 간단하다.

* 단점
  * 의존 관계가 눈에 잘 보이지 않아 추상적이며, 의존관계가 과도하게 복잡해질 수 있음
  * 외부에서 변경이 불가능함 -> 테스트가 용이하지 않음
  * DI Container와 강한 결합을 가짐 -> 단위테스트가 용이하지 않음
  * 의존성 주입 대상 필드가 final 선언 불가함

# Setter 주입
> setter메소드를 통해 의존성을 주입함

```java
@Controller
public class MemberController{
	private MemberService memberService;
    
    @Autowired
    public void setMemberService(MemberService memberService){
    	this.memberService = memberService;
    }
}
```

* 장점
  * 의존성이 선택적으로 필요한 경우 사용
  * 생성자 주입에 비해 복잡하지 않음

* 단점
  * 의존성 주입 대상 필드가 final 선언 불가함
  * NullPointerException의 위험이 있고 런타임시점에 알수있다.
  
```java
@Service
public class MemberService{
	@Autowired
	private MemberRepository memberRepository;
    
    @Override
    public void register(Member member){
    	memberRepository.insertMember(member);
    }
}

public class MemberServiceTest {
	@Test
    public void addTest() { 
    	MemberService memberService = new MemberServiceImpl();
        memberService.register(new Member("dbtlwns",1234)); 
    } 
}
```
>위 코드에서 테스트코드 순수자바코드이다. 그렇기에 DI프레임워크 위에서 동작하지 않기때문에 의존관계는 주입이 되지 않는다. 그래서 memberRepository는 null이라 에러가 발생할 것 이고 Setter를 통해 해결한다면 OCP를 위반한다. 하지만 생성자를 주입하여 사용하면 컴파일 시점에 객체를 주입받아 테스트코드 작성이 가능하며 주입하는 객체가 누락된 경우 컴파일시점에 오류를 발견할 수 있다.

# 생성자 주입
> 클래스의 생성자를 통해 의존성을 주입함

```java
@Controller
public class MemberController{
	private MemberService memberService;
    
    @Autowired
    public MemberController(MemberService memberService){
    	this.memberService = memberService;
    }
}
```

* 장점
  * 필수적으로 사용해야 하는 레퍼런스 없이는 인스턴스를 만들지 못하도록 강제함
  * Spring 4.3 이상부터는 생성자가 하나인 경우 @Autowired를 사용하지 않아도 됨
  * 순환참조 의존성을 알아 차릴 수 있음 
  * NullPointerException을 방지할 수 있다.
  * 의존성 주입 대상 필드를 final로 불변 객체 선언할 수 있음


* **lombok을 이용한 생성자 주입**
* final 혹은 @NonNull이 붙은 필드에 대해 생성자를 생성해줌
```java
@RequiredArgsConstructor
public class MemberController{
	private final MemberService memberService;
}
```

# 순환참조?

> A가 B를 참조하고 B가 A를 참조하는 상황
	
	# 객체지향 5대원칙

* SOLID원칙
> 
SRP(단일 책임 원칙)
OCP(개방-폐쇄 원칙)
LSP(리스코프 치환 원칙)
DIP(의존 역전 원칙)
ISP(인터페이스 분리 원칙)

# Single Responsiblity Principle(단일 책임 원칙)
* **소프트웨어의 설계 부품(클래스, 함수 등)은 단 하나의 책임만을 가져야 한다.**
* **클래스나 함수등은 관련된 책임만 줘야한다.**
```java
class UserAction{
    private Long id;
    private String name;
    private Integer age;
    public void sleep(){};
    public void sing(){};
    public void cook(){};
}
```
>
위 클래스는 유저를 정의하고 유저의 행위들을 메소드로 표현한 것 이다.
하지만 정말 한곳에 때려박았기 때문에 SRP를 위배한다.
즉 클래스는 목적과 취지에 맞는 속성과 메소드로 구성을 해야한다.

# Open Closed Principle(개방-폐쇄 원칙)
* **기존의 코드를 변경하지 않고(Closed)기능을 수정하거나 추가할 수 있도록 설계해야 한다.**
```java
//수정전
class SoundPlayer{
	void play(){
    	System.out.println("play wav");
    }
}
public class Client{
	public static void main(String[] args){
    	SoundPlayer sp = new SoundPlayer();
        sp.play();
    }
}
```
wav를 실행하는 코드라고 할 때 mp3를 실행하는 코드를 만들기 위해서는 play메소드를 수정해야한다. 이것은 OCP원칙에 위배됨
```java
interface playAlgorithm{
	void play();
}
class Wav implements playAlgorithm{
	@Override
    public void play(){
    	System.out.println("play wav");
    }
}
class Mp3 implements playAlgorithm{
	@Override
    public void play(){
    	System.out.println("play mp3");
    }
}
```
상위클래스의 수정은 필요없고 play만 재정의 하여 OCP를 지킨다.
# Liskov Substitution Principle(리스코프 치환 원칙)
* **하위클래스는 상위클래스에서 가능한 행위를 수행할 수 있어야 한다.**
* **객체 지향은 인간이 실세계를 보면서 느끼고 논리적으로 이해한 것과 똑같이 프로그래밍하는 게 목적이기 때문에 논리적으로 맞아 떨어져한다.**

```java
class Parent{
    
}
class Child extends Parent{
    
}

class Animal{
    
}
class Tiger extends Animal{
    
}
```

>
부모와 자식 -> 자식또한 부모가 될 수 있고 부모또한 자식이 될 수 있기 때문에 올바르지 않음
동물과 호랑이 -> 호랑이는 동물의 한 종류이다. 동물을 호랑이로 확장시키기 때문에 LSP성립

# ISP(인터페이스 분리 원칙)
* **자신이 사용하지 않는 인터페이스는 구현하지 말아야 한다.**
* **하나의 일반적인 인터페이스 보다 여러개의 구체적인 인터페이스가 낫다.**
```java
public interface Action(){
    void drive();
    void eat();
    void go();
    void back();
    void develop();
    void sing();
}
```
>
특별한 행위에 대한 인터페이스를 정의하고 메소드들을 떡칠해놨다.
하지만 Action인터페이스를 구현하는 구현체가 저 각각 다른 느낌의 행위의 메소드들을 사용을 하지 않는다면 ISP원칙을 위배한다.

# DIP(의존 역전 원칙)
* **추상화된 것은 구체적인 것에 의존하면 안 된다. 구체적인 것이 추상화된 것에 의존해야 한다.**
* **추상클래스 또는 상위클래스는 구체적인 구현**
```java
class Benz {
	SnowTire snowTire = new SnowTire();
}
```
>벤츠가 SnowTire를 장착하고 있다. SnowTire는 계절에 영향을 받아 벤츠라는 클래스보다 더 변화에 민감한 SnowTire를 의존하고 있다. 이걸 역전하려면 다음과 같다.

```java
class Benz {
	Tire tire = new SnowTire();
}
public interface Tire{
}
public class SnowTire implements Tire{
}
public class CommonTire implements Tire{
}
```
>
변하기 쉬운것에 의존하던 것을 추상화된 인터페이스를 두어 영향을 받지 않게 의존방향을 역전시킴.
