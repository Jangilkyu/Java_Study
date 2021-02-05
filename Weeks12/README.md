# 목표
- 자바의 애노테이션에 대해 학습하세요.

# 학습할 것 (필수)
# 애노테이션 정의하는 방법
애노테이션(annotation)은 자바의 특수한 인터페이스 이며 기본적으로 이름처럼 주석을 다는 역할을 한다.
- Annotation은 프로그램에게 추가적인 정보를 제공해주는 *메타 데이터*(정보)를 프로그램 요소이다.

## 애노테이션 정의

```java
public @interface UseAnnotation { }
```

## 빌트인 애노테이션

- java에서 지원하는 기본 애노테이션

### @Override

- 현재 메소드가 슈퍼클래스의 메소드를 오버라이드한 메소드임을 컴파일러에게 명시함

```java
    @Override int overriddenMethod() { 

    }
```

### @Deprecated

- `@Deprecated`애노테이션은 차후 버전에서는 지원하지않기 때문에 가급적 사용을 자제해달라는 의미로 사용된다.

```java

    @Deprecated static void deprecatedMethod() { 
        
    }

```

### @SupressWarning

- 경고를 제거하는 애노테이션

```java
    @SuppressWarnings("deprecation")
    public void useDeprecated(){

    }


```

### @FuncationalInterface
- 함수형 인터페이스라는 것을 알려준다

# @retention

- 애노테이션이 유지되는 기간을 지정하는 데 사용

- 유지정책

|유지정책|의미|
|----|----|
|SOURCE|  소스파일에만 존재. 클래스파일에는 존재하지 않는다.|
|CLASS|	클래스 파일에 존재. 실행시 사용 불가 . DEFAULT|
|RUNTIME|	클래스 파일에 존재. 실행시 사용 가능|

- 컴파일러에 의해 사용되는 어노테이션의 유지 정책은 SOURCE이다.


# @target

- 애너테이션을 정의할 때 적용가능한 대상을 지정하는데 사용한다.

```java
@Target({ElementType.TYPE, 
         ElementType.FIELD, 
         ElementType.PARAMETER, 
         ElementType.PACKAGE, 
         ElementType.CONSTRUCTOR, 
         ElementType.LOCAL_VARIABLE})
public @interface UseAnnotation {

}
```
|대상 타입|	의미|
|----|----|
|ANNOTATION_TYPE|애노테이션|
|CONSTRUCTOR|생성자|
|FIELD|	필드 (멤버변수, enum 상수)|
|LOCAL_VARIABLE	|지역변수|
|METHOD|메소드|
|PACKAGE|패키지|
|PARAMETER|매개 변수|
|TYPE|타입(class, 인터페이스, enum)|
|TYPE_PARAMETER|타입 매개변수(JDK 1.8)|
|TYPE_USE|타입이 사용되는 모든곳(JDK 1.8)|

# @documented
- @Documented는 메타 데이터 어노테이션이다. Javadoc에 해당 애노테이션 정보를 표시한다.



# 애노테이션 프로세서

- 컴파일 타임에 애노테이션을 분석할 수 있다. 붙여진 애노테이션에 따라서 클래스를 생성한다.

동작 구조

1. 어노테이션 프로세서를 사용한다는 것을 자바 컴파일러가 알고 있는 상태에서 컴파일을 수행

2. 어노테이션 프로세서들이 각자의 역할에 맞게 구현되어 있는 상태에서 실행되지 않은 어노테이션 프로세서를 실행

3. 어노테이션 프로세서 내부에서 어노테이션에 대한 처리

4. 자바 컴파일러가 모든 어노테이션 프로세서가 실행 되었는지 검사하고, 모든 어노테이션 프로세서가 실행되지 않았다면 반복


# references 
출처: https://dev-coco.tistory.com/24