# 목표
- 자바의 예외 처리에 대해 학습하세요.

# 학습할 것 (필수)
# 자바에서 예외 처리 방법 (try, catch, throw, throws, finally)

- **에러 상태**
    - 발생하면 프로그램 안에서 처리하여 연속된 진행을 할 수 있는 상태
    - 프로그램을 계속하여 사용할 수 있다.

에러에는 크게 두가지 에러가 존재한다.

## Compile Exception
- 개발자가 반드시 try~catch로 처리해야 하는 예외
- bytecode가 제대로 생성되지 않는 상황에 발생하는 예외

## Runtime Exception
- 개발자가 try~catch를 하지 않아도 JVM이 처리해주는 예외
- 저장과 연산이 제대로 수행되지 못하는 상황에 발생하는 예외

- `try~catch`, `throws`, `throw`를 사용하여 예외를 처리
    - `try~catch`: 예외를 잡아서 예외상황을 처리할 때 사용
    - `throw`: 예외를 강제적으로 발생시킬 때
    - `throws`: 발생된 예외를 던질 때 사용

## try~chtch
**try~catch 문법**
```java
    try {
        예외발생 예상 코드 //API를 보고 확인한다.
    }catch(예외처리클래스 객체명){
        예외가 발생했을 때 제공할 코드
    }catch(예외처리클래스 객체명){
    예외가 발생했을 때 제공할 코드
    }finally{
        반드시 실행되어야 할 코드를 정의
    }
```

## throws
- method안에서 발생된 예외를 method밖으로 던질 때 사용
- method를 호출한 곳에서 예외를 처리하도록 만드는 것
- 일처리 코드와 예외처리 코드를 분리할 수 있다.
- throws되는 예외는 method안에서 try~catch로 처리하지 않는다.

**문법**
```java
    접근지정자 반환형 method명(매개변수) throws 예외클래스 , , , {
    }
    
    호출하는 곳에서 예외 처리)
    try{
        method명();
    }catch(예외클래스 객체명){
        예외가 발생했을 때 제공할 코드
    } 
```

## throw
- 예외를 강제로 발생 시킬 때 사용
- 발생된 예외는 try~catch로 또는 throws로 반드시 처리해야 한다.
- 특정상황에서 예외를 발생시켜 처리할 때 사용
- 사용자 정의 예외 처리 클래스와 주로 사용

**throw 문법**
```java
    throw new 예외처리클래스();
    //예외가 발생된 후 바로 처리 : 권장하지 않는다.
    public void test(){
    try{
        throw new Exception();
        }catch(Exception e){

        }
    }
```
```java
//throws 에서는 throw로 발생시킨 예외 또는 부모예외로 예외를 날릴 수 있다.
    public void test() throws Exception{
        throw new Exception();
    }
```

## 사용자정의 예외 처리 클래스
- java에서 제공되는 예외처리 클래스가 현재 업무상황에 맞지 않을 때
- 개발자가 현재 업무상황에 맞는 예외처리 클래스를 만드는 것
- Compile 예외를 만들 때 : Exception 상속
- Runtime 예외를 만들 때 : RuntimeException 상속

# 자바가 제공하는 예외 계층 구조
<img src = "https://user-images.githubusercontent.com/69107255/104744381-273abc80-5790-11eb-8b4a-eddb42688676.png">

[출처](https://reference-m1.tistory.com/246)

# Exception과 Error의 차이는?
- Exception
    - java.lang.Exception
    - checked exception(compile time)
        - 실행하기 이전 예측이 가능하다.
        - ide(인텔리제이,이클립스)등이 컴파일 할 때 체크를 해준다.
    - unchecked exception(runtime)
        - 실행해야 확인이 가능하다.
        - 실행 후 NullPointerExceoption, SqlException 발생할 수 있다.
- Error
    - java.lang.error
    - 핸들링이 불가능하여 복구가 불가능하다.
    - 컴파일시에 발생할 수 없다.
    - OutOfMemoryError, IOError등이 있다.
# RuntimeException과 RE가 아닌 것의 차이는?
Exception은 `Checked Exception`과 `Unchecked Exception`으로 구분할 수 있다.
RuntimeException을 상속한 클래스는 `Unchecked Exception`으로 분류할 수 있다.
RuntimeException을 상속하지 않는 클래스는 `Checked Exception`

|구분|Checked Exception|Unchecked Exception|
|확인시점|컴파일(Compile)시점|런타임(Runtime)시점|
|처리여부|반드시 예외 처리(try-catch, throws)를 해줘야 한다|명시적 처리를 강제하지 않음|
|트랙잭션 처리|예외 발생시 롤백(rollback)하지 않음|예외 발생시 롤백(rollback)해야 함|

# 커스텀한 예외 만드는 방법

1.Exception
```java
    public class UseException extends Exception{
        public UseException(String msg){
            super(msg);
        }
    }
```
```java
    public class UseExceptionTest {
        public static void main(String[] args) throws Exception {
            throw new MyException("사용자 정의 예외");
        }
    }
```