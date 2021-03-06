# 학습할 것 (필수)
- 람다식 사용법
- 함수형 인터페이스
- Variable Capture
- 메소드, 생성자 레퍼런스

# 람다식
- 익명함수(Anonymous functions)를 지칭하는 용어
- Java8부터 지원
- 익명객체를 생성하기 위한 표현식

## 람다식 사용법
- 매개 변수를 가진 코드 블록이지만, 런타임 시에는 익명 구현 객체를 생성한다.
- (매개변수) -> {실행코드} 형태로 작성되는데, 함수 정의 형태를 띠고 있지만 런타임 시에 인터페이스의 익명 구현 객체로 생성된다.
- 어떤 인터페이스가 구현되는가는 대입되는 인터페이스에 따라 결정된다.

```java
    (매개변수, ...) -> { 실행문 ... }
```

add함수에서 x와 y를 더하는 함수가 있을 때
```java
    int add(int x, int y){
        return x + y;
    }
```

람다식으로 아래와 같이 표현이 가능하다.
```java
    (int x, int y) -> {return x+y;}
```

람다식은 매개변수 자료형이 생략이 가능하다. **매개변수가 하나인 경우에는 괄호도 생략이 가능하다.**
단, 매개변수가 두 개이상인 경우에는 괄호를 생략할 수가 없다.

```java
    x, y -> {System.out.println(x + y );} //잘못된 형식
```

중괄호 안의 구현되는 부분이 한 문장이라면 중괄호도 생략이 가능하지만, return문은 중괄호 생략 불가
```java
    str -> return str.length() // 잘못된 형식
```

## 함수형 인터페이스(Functional Interface)
- 람다식을 다루는 인터페이스

- @FunctionalInterface 어노테이션을 사용
- @FunctionalInterface가 적용된 인터페이스는 한개의 추상메소드만 선언 가능
- 추상메소드가 1개가 아니면 에러 발생

```java
 @FunctionalInterface
 public interface Adder {
     public abstract double add(double x, double y);
 }
```

### 함수적 인터페이스를 제공하는 표준 API
- java.util.function 패키지
|종류|추상 메소드 특징|
|----|----|
|Consumer|매개값은 있고, 리턴값은 없음|
|Supplier|매개값은 없고, 리턴값은 있음|
|Function|일반적인 함수. 하나의 매개변수를 받아서 결과를 반환|
|Operator|매개값도 있고, 리턴값도 있음|
|Predicate|조건식을 표현하는데 사용. 매개변수는 하나, 반환 타입은 boolean|

##  Variable Capture
람다 시그니처의 파라미터로 넘겨진 변수가 아닌 외부에서 정의된 변수를 자유 변수(Free Variable)**라고 부른다.
또한 람다 바디에서 **자유 변수를 참조하는 행위를 유식한 말로 **람다 캡처링(Lambda Capturing)**이라고 부른다.

### 람다 캡처링의 제약 조건
- 지역 변수를 람다 캡처링 할 때 아래 두 가지 제약조건이 존재한다.

- 지역변수는 final로 선언돼있어야한다.
- final로 선언되지 않은 지역변수는 final처럼 동작해야한다.
    - 즉, 값의 재할당이 일어나면 안 된다.


## 메소드, 생성자 레퍼런스

- 메소드 참조

메서드 참조의 장점은 람다 표현식과는 달리 코드를 여러곳에서 재사용 할수 있고 자바의 기본 제공 메서드 뿐만 아니라 직접 개발한 메서드도 사용할 수 있다는 점이다.

```java

// 람다 표현식
(String name) -> System.out.println(name)
// 한정적 메서드 참조
Calendar.getInstance()::getTime
``` 

- 생성자 참조
메서드는 클래스 혹은 객체 단위로 접근 권하만 있으면 언제든 호출할 수 있지만 생성자는 오직 객체가 생성될 때만 호출할 수 있으며, 객체를 생성할 때 초기화하는 개념을 가진다.

```java
Calendar cal = Calendar.getInstance(); // 객체 생성
cal::getTime; // 메서드 참조 구문. cal 변수를 참조한다.
```

[메소드, 생성자 레퍼런스 출처](https://sungjk.github.io/2020/11/08/practical-modern-java.html)