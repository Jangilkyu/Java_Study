# 목표
자바의 인터페이스에 대해 학습하세요.

# 학습할 것 (필수)
- 인터페이스 정의하는 방법
- 인터페이스 구현하는 방법
- 인터페이스 레퍼런스를 통해 구현체를 사용하는 방법
- 인터페이스 상속
- 인터페이스의 기본 메소드 (Default Method), 자바 8
- 인터페이스의 static 메소드, 자바 8
- 인터페이스의 private 메소드, 자바 9

# 인터페이스란?


# 인터페이스 정의하는 방법
- 인터페이스를 정의할때는 `interface`라는 예약어를 통해서 선언이 가능하다.
- 모든 멤버변수는 `public static final` 이고 생략 가능하다.
- 모든 메소드는 `public abstract` 이고 생략가능하다.

```java
    public interface Person {

    //abstract method: 구현의 강제성을 가지는 method 일을 정의 할 수 없음
    //interface에서는 일반method를 가질 수 없기 때문에 abstract를 붙여도 안붙여도 에러가 나지 않음
        public abstract void eat();
        public abstract void walk();

    }
```

# 인터페이스 구현하는 방법
- 인터페이스를 구현할 때는 `implement`를 사용한다.

```java
    public class Jangilkyu implements Person {
        //Person인터페이스에 선언된 추상메소드를 구현
        @Override
        public void eat(){
            System.out.println("밥을 먹는다.");
        }
    }
```

# 인터페이스 레퍼런스를 통해 구현체를 사용하는 방법
구현부가 없기때문에 인터페이스를 만든다면 반드시 구현하는 클래스를 생성해야한다.

```java
    public interface Person {
        void eat();
        default void sleep();
    }
```
사람이라는 인터페이스를 생성하였고, `먹는`이라는 추상메소드를 생성하고 `자다`라는 default method를 생성하였습니다. 

```java
    public class Jangilkyu implements Person {

        @Override
        public void eat(){
            System.out.println("밥을 먹는다.");
        }

    }
```
Person을 인터페이스를 통해 Jangilkyu를 구현했습니다.
```java
    public class A {
        public static void main(String[] args){
                Person jangik = new Jangilkyu();

                jangik.eat();
        }
    }
```

# 인터페이스 상속
- 인터페이스끼리는 다중상속이 가능하다.
- 기능확장이 쉬어진다. 단, 객체의 크기가 필요 이상으로 커질 수 있다.
- 부모가 모호해질 수 있다.

```java
    접근지정자 interface 인터페이스명 extends 부모인터페이스명, 부모인터페이스명..N개가능 {

    }

    인터페이스명 객체명 = new 구현클래스의 생성자();
```

# 인터페이스의 기본 메소드 (Default Method), 자바 8
> interface에서 업무를 구현할 수 있는 method

- JDK 1.7에서부터 interface에 업무를 구현할 수 있는 defalut method 추가
- 구현하게 되면 추상클래스와 큰 차이가 없어지게 된다.
- 사용은 객체를 생성한 후에 사용(is-a관계에서)

```java
    접근지정자 default 반환형 method명(매개변수,,) {
            
    }
```
# 인터페이스의 static 메소드, 자바 8
default method와 차이점은 구현부 객체에서 재정의가 불가능하다.

```java
    public interface Calculator {

        int add(int x,int y);

        default int mul(int x, int y){
            return x * y;
        }

        static void result(int val){
            System.out.println(val);
        }
    }
```

```java
    public class CalMain {
        
        public static void main(String[] args){
            Calculator.result(150);
        }
    }
```
`interfane이름.메소드`로 호출을 할 수 있다.

# 인터페이스의 private 메소드, 자바 9
구현클래스와 인터페이스가 상속되지 않고, 인터페이스에서 다른 메소드를 호출할 수 있다.
```java
    public interface Calculator {

        int add(int x,int y);

        default int mul(int x, int y){
            return x * y;
        }

        static void result(int val){
            System.out.println(val);
        }

        private static void print(){
            System.out.println("출력");
        }//private method
    }
```