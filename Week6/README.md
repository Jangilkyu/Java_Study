# 목표
자바의 상속에 대해 학습하세요.
## 학습할 것 (필수)
- 자바 상속의 특징
- super 키워드
- 메소드 오버라이딩
- 다이나믹 메소드 디스패치 (Dynamic Method Dispatch)
- 추상 클래스
- final 키워드
- Object 클래스

# 자바 상속의 특징

## 상속(inheritance)
> 부모클래스의 자원을 자식클래스에서 사용하는 것(코드의 재사용성 향상)

- 모든 클래스의 부모 클래스는 `java.lang.Object클래스`이다.
- 단일 상속만 지원(부모가 하나인 상속)(부모클래스가 명확함 단, 기능 확장에 제한적)
- 클래스간의 `계층 생성`(부모자식 관계)
- 부모클래스의 자원 중 private은 자식에서 사용 할 수 없다.

`부모 클래스(super class)`: 기능 제공(모든 자식이 사용하게 될 공통 특징 정의)
`자식 클래스(sub class)`: 기능 사용

`extends키워드`로 `자식클래스`에서 `부모클래스`를 선택(부모 클래스는 자식클래스를 알 수 없음)
`생성자`는 **상속되지 않는다.**
자식 클래스를 생성하면 부모 클래스가 먼저 생성된다.

## is-a 관계
> 부모클래스로 데이터형을 선언하고 자식클래스를 생성해서 할당 하는 것

- 부모클래스의 variable과 method만 호출 가능
- 자식클래스에 부모클래스에 Override한 method가 있으면 그 method를 호출
- 내 클래스에 정의 된 것처럼 사용
```java
    method명();
```

## 상속관계의 객체화(is-a 관계의 객체화)
- 객체 다형성을 사용할 때

```java
부모클래스명 객체명 = new 자식클래스생성자();
```

## has-a 관계
> 객체명을 사용하여 다른 클래스를 사용

```java
    객체명.method명();
```


# super 키워드
> 부모클래스의 자원을 사용할 때

super키워드에는 `method 형식`과 `keyword 형식` 형식이 있다.

### method 형식
> 부모클래스의 생성자를 호출할 때 사용

- 모든 클래스의 생성자의 첫 줄에는 `super();`가 생략되어 있음
- 생성자의 첫번째 줄에서만 사용 가능

```java
    super(); // default 생성자
    super(값); // 매개변수 받는 생성자
```

**부모클래스 Test.java**
```java
    class Test extends Object{
        public Test() {
            super(); // Object생성자 호출
        }
    }
```

**자식클래스 TestSub.java**
```java
    class TestSub extends Test{
        public TestSub(){
            super(); // 생략되더라도 default 부모클래스 생성자가 불림
        }
    }
```
### keyword 형식
- 부모 객체의 시작 주소를 저장하고 있음
- 부모 클래스와 자식클래스가 같은 이름의 변수,method를 가지고 있는 경우 식별하여 사용할 때

**instance영역에서만 사용가능**
```java
    super.변수명;0
    super.메소드명();
```

**부모클래스 Test.java**
```java
    class Test{
        int i;
        int j;

        public void useVar() {
            System.out.println(i + "/" + j);
        }
    }
```

**자식클래스 TestSub.java**
```java
    class TestSub extends Test {
        int i;
        
        public void UseI(){
            super.j= 10;
            super.useVar();
             System.out.println(this.i); // this가 숨어있다.
        }
        public static void main(String[] args) {
            TestSub ts = new TestSub();
	    }
    }
```

# 메소드 오버라이딩
> 상속관계의 클래스에서 같은 이름의 method를 자식클래스에서 재정의 하는 방법

- 상속관계에서 사용
- 부모클래스가 제공하는 method를 사용할 때
- 기능이 자식 클래스와 맞지않는다면 부모클래스의 method를 자식클래스에서 재정의 하는 것
- 최우선적인 호출: 자식의 method가 가장 먼저 호출
- 규칙: 접근지정자는 달라도 되고, 반환형, method명, 매개변수는 같아야 함 
함

# 다이나믹 메소드 디스패치 (Dynamic Method Dispatch)
> 어떤 메소드를 호출할지 결정하여 실제로 실행시키는 과정

## Static Dispatch
> 컴파일 시점에 어떠한 클래스를 사용할지 컴파일러가 알고 있는것

## Dynamic Dispatch
런타임 시점에 실행할 메서드가 결정되는 것

출처 :defacto-standard.tistory.com/413

# 추상 클래스
> 상속관계에서 부모클래스를 만들 때 사용

**추상클래스의 특징**
- 구현에 강제성이 있는 method(자식클래스에서 반드시 Override하여 사용)
- method의 body가 없는 추상 method를 가진다.
- method body가 없어 일을 할 수 없다.(자식 클래스가 구현해야할 일의 목록을 만들 때 사용)
    - 직접호출하면 ERROR 발생(super.method명() => error)
- 객체화가 되지않는 클래스(자식클래스가 객체화될 때에만 객체가 생성됨)

```java
    abstract class 클래스명
    변수: instatnce_Varialbe, static_Varialbe
    method: instance_Method, static_Method
    abstract_method // method의 body가 없는 추상 method를 가진다.
```

**추상클래스 선언**
```
    접근지정자 abstract 반환형 method명(매개변수);
```
**추상클래스 작성법**
```java
    접근지정자 abstract class 클래스명 extends 부모클래스명 implements 구현인터페이스들..
```

# final 키워드
> 상수를 표현하기 위한 `예약어`이다.

- `변수`를 선언과 동시에 `초기화`를 해야하며 초기화 이후에는 값을 수정할 수 없다.

```java
    public class Test{
        public static void main(String[] args){
            final int a = 10;

            a = 20; // 수정 시 에러 발생
        }
    }
```
**fianl로 선언 된 변수에 값할당 시 에러 Msg**
<img src = "https://user-images.githubusercontent.com/69107255/103144853-b5b0b500-4773-11eb-86ab-d7127c386cf8.png">

# Object 클래스
> Object클래스는 모든 자바 클래스의 `최고 조상 클래스`

**Object class 특징**

- `java.lang 패키지`의 클래스들은 import 문을 사용하지 않아도 클래스 이름만으로 바로 사용할 수 있다.
- Object클래스들은 필드를 가지지 않고, 11개의 메소드로만 이루어져 있다.
- 사용자가 클래스를 정의할 때 `extends java.lang.Object`를 지정하지 않아도 자동적으로 상속을 받게 된다.

<img src = "https://user-images.githubusercontent.com/69107255/103144954-5fdd0c80-4775-11eb-888d-6b752085ab6a.png">

출처[출처](http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html)

