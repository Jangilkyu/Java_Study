# 목표
- 자바의 패키지에 대해 학습하세요.

# 학습할 것 (필수)
# package 키워드
# import 키워드
# 클래스패스
# CLASSPATH 환경변수
# -classpath 옵션
# 접근지시자

---


# package 키워드

## 패키지(package)란?
- class 파일(bytecode)의 관리편의성을 높이기 위한 폴더(directory)

## 사용목적
- 관련있는 소스나 bytecode를 폴더로 묶어서 관리하기위해
- 패키지단위로 jar로 묶어서 배포

## 패키지 특징
1. 소스에 가장 첫줄에 있어야한다.
2. 패키지 선언은 소스 하나에 단 한번만 있어야한다.
3. 패키지이름과 위치한 폴더 이름이 같아야한다.
4. 패키지이름을 java로 시작할 수 없다.

## 패키지 선언 방법
- 일반적인 소스파일을 
```java
    package 패키지명; 

    //패키지명은 역방향 도메인(도메인을 거꾸로 기술)사용 
    ex) abc.co.kr -> kr.co.abc
```

## 패키지 이름 지정 규칙

|패키지 시작이름|내용|
|----|----|
|java|자바 기본 패키지(Java vendor 개발)|
|javax|	자바 확장 패키지(Java vendor 개발)|
|org|일반적으로 비영리단체 (오픈소스) 패키지| 
|com|일반적으로 영리단체(회사) 패키지|

## 패키지 이름 명명 규칙
- 자바의 예약어로 사용할 수 없다.
- 패키지 이름은 소문자이여야 한다.


# import 키워드

- 다른 패키지에 있는 클래스를 접근할 때 사용한다.


## import 선언 방법

```java
    //선언된 패키지안의 모든 클래스를 사용하고 싶을 때
    import 패키지명.*;
    //선언된 패키지안의 특정 클래스 하나만 사용할 때
    import 패키지명.class명
```

**import 사용법**
```java
사용법
    package test;

    import java.util.Date;

    class Test{

        Date date;
        Date date1 = new Date();
        
        //- import를 선언하지 않고 외부패키지를 사용하려면 클래스앞에 모든 패키지를 기술하는 full path를 기술해야 한다.
        java.util.Calendar // full path
    }
```
- 주의: 패키지가 다르고 클래스의 이름이 같은 경우에는 하나만 import할 수 있음
```java
    import java.util.Date;
    // import java.sql.Date;

    //위에 경우 처럼 패키지가 다르고 클래스의 이름이 같은 경우는 하나는 full path로 처리하고 하나는 import로 처리
    java.sql.Date d = new java.sql.Date();
    Date d1 = new Date()
```

## static import
- JDK 1.5에서부터 추가된 기능
- 다른 클래스의 static 변수, static 메소드를 클래스명없이 사용할 때

**static import 문법**
```java
    - Constant 사용
        import static 패키지명.클래스명.static변수명;
                                    filed명(Constant:상수)

    - method 사용
        import static 패키지명.클래스명.method명;
```

```java
packge test;
    import static java.lang.Integer.MAX_VALUE;
    import static java.lang.Integer.parseInt

            class Test{
                    MAX_VALUE;
                    parseInt("11"); // 정수의 11
            }
```

# 클래스패스
## 클래패스란?
- JVM이 프로그램을 실행할 때 클래스파일을 찾는데 기준이 되는 파일의 경로이다.
- .class 파일을 찾을 때 classpath에 지정된 경로를 사용한다.

classpath를 지정할 수 있는 `두 가지 방법`이 있다.

- CLASSPATH 환경변수 사용
- java runtime에 -classpath 옵션사용


# CLASSPATH 환경변수

- windows 제어판 - 시스템 - 고급 시스템 설정 - 환경변수에서 설정이 가능하다.
- JVM이 시작될 때 JVM의 클래스 로더는 해당 환경 변수를 호출한다.
<img src = "https://user-images.githubusercontent.com/69107255/103443329-8c2ae880-4ca1-11eb-8f30-7b0e7ae9045c.png">
# -classpath 옵션

# 접근지시자
- public
    - 모든 접근을 허용
- protected
    - 같은 패키지에 있는 객체와 상속 관계
- default
    - 같은 패키지 내에 있는 클래스만 접근을 허용
- private
    - 현재 클래스 내 에서만 접근을 허용
|한정자|같은 클래스|같은 패키지|하위 클래스|전체|
|:----:|:----:|:----:|:----:|:----:|
|public|Yes|Yes|Yes|Yes|
|protected|Yes|Yes|Yes||
|default|Yes|Yes||||
|private|Yes|||||||