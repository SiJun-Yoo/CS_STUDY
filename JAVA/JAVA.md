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
